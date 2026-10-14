# 11 — AWS S3 & CloudFront

> This topic is split into three parts. Start with Part 1 and follow the "Next" links. Applies to **general-purpose S3 buckets**, **AWS SDK for JavaScript v3** (`@aws-sdk/client-s3`, `@aws-sdk/s3-request-presigner`, `@aws-sdk/s3-presigned-post`, `@aws-sdk/lib-storage`), and CloudFront **Origin Access Control (OAC)** — OAI is legacy. New buckets: **Block Public Access on**, **Object Ownership = Bucket owner enforced**, **SSE-S3 default** (January 2023+). Strong consistency since December 2020. S3 Select is closed to new customers (July 2024). Console labels and prices change — verify on docs.aws.amazon.com/AmazonS3, docs.aws.amazon.com/AmazonCloudFront, and the pricing pages the morning you use them. Upload *design*: [09](./09-system-design-part4.md#315-design-file-upload--storage). Instance-profile IAM: [10](./10-deployment-aws-ec2-part1.md#34-iam-users-roles-policies-instance-profiles). R2: [12](./12-cloudflare.md). This writing session did **not** create buckets or distributions in your account.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Buckets, Classes, Access Control](./11-deployment-aws-s3-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.3 | Keys, consistency, endpoints, storage classes, BPA, Bucket owner enforced, IAM vs bucket policy |
| [Part 2 — Pre-signed URLs, Multipart, CORS](./11-deployment-aws-s3-part2.md) | 3.4–3.7 | `getSignedUrl`, POST policies, `@aws-sdk/lib-storage`, abort incomplete, CORS that matches a signed PUT |
| [Part 3 — CloudFront, Events, Security, Cost, Interview](./11-deployment-aws-s3-part3.md) | 3.8–3.14 · 4–11 | Versioning/lifecycle, OAC, cache/invalidations, events, SSE, skim Lock/TA/Select, egress, ~8.5 h path, 10 exercises, 36 questions |

> 💡 Interview Tip: "Public bucket for the static site" is the junior answer. The senior sentence is: "Private bucket, CloudFront OAC, hashed filenames, pre-signed browser PUT so Node never sees the bytes."

## Related Files

- File-upload *design* (init API, status machine) → [09-system-design](./09-system-design-part4.md#315-design-file-upload--storage)
- Instance/task roles, OIDC deploys, ALB timeouts → [10-deployment-aws-ec2](./10-deployment-aws-ec2.md)
- CORS as a browser gate (not S3 auth) → [08-engineering-practices](./08-engineering-practices-part4.md#321-csrf-and-cors)
- DNS, WAF, R2 (S3-compatible, no egress) → [12-cloudflare.md](./12-cloudflare.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./11-deployment-aws-s3-part1.md), then continue to [12-cloudflare.md](./12-cloudflare.md).
