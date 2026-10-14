# 11 — AWS S3 & CloudFront (Part 1 of 3): Buckets, Storage Classes & Access Control

> **Parts:** **Part 1 — Buckets, Classes, Access Control** · [Part 2 — Pre-signed URLs, Multipart, CORS](./11-deployment-aws-s3-part2.md) · [Part 3 — CloudFront, Events, Security, Cost, Interview](./11-deployment-aws-s3-part3.md)
>
> Applies to: **general-purpose S3 buckets**, **AWS SDK for JavaScript v3** (`@aws-sdk/client-s3`, `@aws-sdk/s3-request-presigner`, `@aws-sdk/lib-storage`), CloudFront **Origin Access Control (OAC)** — OAI is legacy. New buckets default to **Block Public Access on** and **Object Ownership = Bucket owner enforced** (ACLs disabled). Strong consistency since December 2020. Console labels change — verify on [docs.aws.amazon.com/AmazonS3](https://docs.aws.amazon.com/AmazonS3) and [docs.aws.amazon.com/AmazonCloudFront](https://docs.aws.amazon.com/AmazonCloudFront). Instance-profile IAM is in [10 §3.4](./10-deployment-aws-ec2-part1.md#34-iam-users-roles-policies-instance-profiles). Upload *design* is in [09 §3.15](./09-system-design-part4.md#315-design-file-upload--storage). R2 (S3-compatible, no egress) is [12](./12-cloudflare.md). This session did **not** PUT objects in your account.

## Table of Contents

- [1. Overview](#1-overview)
- [2. Topic Map](#2-topic-map)
- [3. Detailed Explanations (Part 1)](#3-detailed-explanations-part-1)
  - [3.1 Buckets, Objects, Keys, Consistency](#31-buckets-objects-keys-consistency)
  - [3.2 Storage Classes](#32-storage-classes)
  - [3.3 Access Control: Policies, ACLs, Block Public Access](#33-access-control-policies-acls-block-public-access)
- [Next: Part 2](#next-part-2)

---

## 1. Overview

**What this file covers.** How a mid-to-senior full-stack developer uses S3 as the blob store and CloudFront as the public door: keys and consistency, storage classes, **who is allowed to `GetObject`**, browser uploads that never touch Node, multipart for large files, CORS, versioning/lifecycle, S3→Lambda/SQS, encryption, and a private bucket in front of CloudFront with **OAC**.

**Why interviewers care.** "We store files on S3" is not a design. They want: why the bucket is not public, why the browser PUTs with a pre-signed URL, why CloudFront not the S3 website endpoint, why hashed filenames beat invalidations, why egress — not storage — is the bill.

| Junior answer | Senior answer |
|---------------|---------------|
| "The bucket is public-read" | "Block Public Access stays on. CloudFront OAC is the only `GetObject` principal. Users never see the S3 URL" |
| "Upload goes Express → multer → S3" | "Init API issues a pre-signed PUT; the browser talks to S3. Node never sees the bytes ([09](./09-system-design-part4.md#315-design-file-upload--storage), [10](./10-deployment-aws-ec2.md))" |
| "ACLs on each object" | "Bucket owner enforced; ACLs disabled. IAM + bucket policy only" |
| "S3 is eventually consistent" | "Strong consistency since 2020. I don't design for the old us-east-1 overwrite lag" |
| "OAI" | "OAC. OAI is legacy: no SSE-KMS, no opt-in Regions the same way, no PUT/DELETE through CloudFront" |

> 💡 Interview Tip: If they say "make the bucket public for the static site", the correction is CloudFront + OAC, not `Principal: "*"`.

---

## 2. Topic Map

**Part 1 — Store and who can read**
- [ ] Buckets, keys, strong consistency — [3.1](#31-buckets-objects-keys-consistency)
- [ ] Storage classes (Standard → Glacier / Intelligent-Tiering) — [3.2](#32-storage-classes)
- [ ] IAM vs bucket policy vs ACLs; Block Public Access; Object Ownership — [3.3](#33-access-control-policies-acls-block-public-access)

**[Part 2](./11-deployment-aws-s3-part2.md) — Bytes in**
- [ ] Pre-signed GET/PUT; POST policies
- [ ] Multipart + `@aws-sdk/lib-storage`; abort incomplete
- [ ] CORS for browser PUT

**[Part 3](./11-deployment-aws-s3-part3.md) — Serve, operate, interview**
- [ ] Versioning, lifecycle, replication
- [ ] CloudFront + OAC, cache behaviors, invalidations, static hosting
- [ ] Event notifications; SSE-S3/SSE-KMS; logging
- [ ] Object Lock, Transfer Acceleration, Select (skim); cost (egress)
- [ ] Resources, ~8.5 h path, exercises, 36 questions

---

## 3. Detailed Explanations (Part 1)

### 3.1 Buckets, Objects, Keys, Consistency

A **bucket** is a globally unique name in one Region (`notes-uploads-prod` in `us-east-1`). An **object** is bytes + metadata at a **key** (`uploads/user-42/a1b2c3.png`). Keys are not folders; `uploads/` is a prefix. `LIST` is by prefix + delimiter.

**URL shapes** (don't mix them):

| Endpoint | Example | Use |
|----------|---------|-----|
| REST (path-style, legacy) | `s3.amazonaws.com/bucket/key` | Avoid for new work |
| REST (virtual-hosted) | `bucket.s3.region.amazonaws.com/key` | API, SDK, **CloudFront S3 origin** |
| Website | `bucket.s3-website-region.amazonaws.com` | Index/error docs only. **No OAC.** HTTPS is awkward. Prefer CloudFront on the REST origin |

**Consistency (Dec 2020+).** Strong read-after-write for new PUTs, overwrites, and DELETEs in **all** Regions. After a successful PUT, a GET returns the new bytes (or 404 after DELETE). `LIST` after write is also strongly consistent. You do **not** "wait a second for us-east-1" anymore. If a client still sees old content, it is almost always **CloudFront/browser cache**, not S3.

**Naming.** Bucket names are DNS-compatible, globally unique. Account-level: Block Public Access and encryption defaults apply to new buckets — keep them.

```bash
aws s3api create-bucket --bucket notes-uploads-prod --region us-east-1
# us-east-1: no LocationConstraint. Other Regions: --create-bucket-configuration LocationConstraint=eu-west-1
aws s3 ls s3://notes-uploads-prod
```

**Keys.** Include a uniqueness token (`ulid` / `uuidv7` — [09](./09-system-design-part4.md#321-distributed-ids)), never `user-provided-filename.jpg` as the sole key (overwrites, path traversal). Store the canonical key in Postgres; the user's filename is metadata.

> ⚠️ Pitfall: Using the **website endpoint** as a CloudFront origin. OAC does not apply there; people "fix" it by making the bucket public. Use the REST origin + OAC ([Part 3](./11-deployment-aws-s3-part3.md)).

### 3.2 Storage Classes

Class is a **per-object** (or lifecycle) choice. Do not quote prices — [aws.amazon.com/s3/pricing](https://aws.amazon.com/s3/pricing) the morning of.

| Class | When | Watch |
|-------|------|--------|
| **S3 Standard** | Hot user uploads, website assets at origin | Default |
| **Intelligent-Tiering** | Unknown or changing access | Monitoring fee per object; great default when you cannot predict |
| **Standard-IA** | Infrequent, still millisecond GET | **Minimum billable object size and minimum storage duration** (check current); retrieval fee |
| **One Zone-IA** | Recreatable, one AZ OK | AZ failure = data gone |
| **Glacier Instant Retrieval** | Archive you might GET now | Higher GET cost |
| **Glacier Flexible Retrieval** | Hours OK | Restore job before read |
| **Glacier Deep Archive** | Compliance years | Cheapest storage, slowest restore |
| **S3 Express One Zone** (directory buckets) | Extremely hot, single AZ | Different bucket type/API; don't pretend it's a general bucket |

**Lifecycle** (Part 3) is how objects *move* between classes. Interview: "user avatars stay Standard; originals older than 90 days go IA; logs go Glacier after 30."

Minimum duration charges mean "transition to IA after 1 day" can **cost more** than leaving them in Standard. Read the current minimums before you write the rule.

### 3.3 Access Control: Policies, ACLs, Block Public Access

Three layers, in the order you should think:

1. **Block Public Access** (account and/or bucket). Four switches; **all on** for new buckets. They **override** a bucket policy that tries to go public. Turning them off is a deliberate, logged event — not a CORS fix.
2. **Object Ownership = Bucket owner enforced** (default). **ACLs are disabled.** `PutObjectAcl` fails. You manage access with **IAM identity policies** and **bucket policies** only. Keep it.
3. **IAM vs bucket policy.** IAM: "what can this role do?" Bucket policy: "what can anyone (including CloudFront) do to *this* bucket?" Both must allow (and nothing deny). Same evaluation idea as [10](./10-deployment-aws-ec2-part1.md#34-iam-users-roles-policies-instance-profiles).

**App uploads** — IAM on the **instance/task role**, prefix-scoped (from 10):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListUploadsPrefix",
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:ListBucketMultipartUploads"],
      "Resource": "arn:aws:s3:::notes-uploads-prod",
      "Condition": { "StringLike": { "s3:prefix": ["uploads/*"] } }
    },
    {
      "Sid": "WriteUploadsPrefix",
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject", "s3:AbortMultipartUpload"],
      "Resource": "arn:aws:s3:::notes-uploads-prod/uploads/*"
    }
  ]
}
```

`ListBucket` / `ListBucketMultipartUploads` need the **bucket** ARN; object actions need `bucket/key`. Mixing them on one `Resource` array is the classic `AccessDenied` on `ListObjects`.

**CloudFront reads** — **bucket policy**, not an ACL, with the CloudFront service principal and **this distribution's ARN** (OAC). Full JSON in [Part 3](./11-deployment-aws-s3-part3.md).

**Don't.** `Principal: "*"` + `s3:GetObject` on `/*` (public bucket). Don't "temporarily" disable Block Public Access to debug CORS — CORS is a **browser** header problem, not a public-ACL problem ([Part 2](./11-deployment-aws-s3-part2.md)).

**Cross-account.** Bucket policy (resource-based) is the usual grant; the other account still needs IAM allow. ACLs were the old cross-account object-writer story — that's why Bucket owner enforced exists (you own what they PUT).

> 💡 Interview Tip: "Bucket policy vs IAM policy?" — identity vs resource. For CloudFront, the principal is `cloudfront.amazonaws.com` with `AWS:SourceArn` of the distribution. For the Node app, the principal is the instance role.

---

## Next: Part 2

➡️ [Part 2 — Pre-signed URLs, Multipart, CORS](./11-deployment-aws-s3-part2.md): SDK v3 `getSignedUrl`, POST policies, `@aws-sdk/lib-storage`, and the CORS JSON that actually matches a browser PUT.
