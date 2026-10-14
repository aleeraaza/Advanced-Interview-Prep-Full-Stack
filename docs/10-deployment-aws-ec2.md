# 10 — AWS EC2 & Deployment

> This topic is split into four parts. Start with Part 1 and follow the "Next" links. Applies to **Amazon Linux 2023**, **Node.js 24** (`dnf install nodejs24`; Amazon lists security support through April 2028), **IMDSv2 required** on AL2023 AMIs, and the Well-Architected **six pillars**. Console labels, Free Tier, and action majors change — verify on docs.aws.amazon.com, aws.amazon.com/free, and github.com/aws-actions the morning you use them. L4 vs L7: [09](./09-system-design-part1.md#34-load-balancing). GitHub Actions / OIDC primer: [08](./08-engineering-practices-part3.md#315-github-actions). S3 IAM and pre-signed uploads: [11](./11-deployment-aws-s3.md). Cloudflare DNS: [12](./12-cloudflare.md). This writing session did **not** launch a billed instance in your account — the Part 2 walkthrough is yours to run.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — VPC, EC2, IAM, Security Groups](./10-deployment-aws-ec2-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.4 | Custom VPC, SG vs NACL, families/AMIs/user data/IMDSv2, instance profiles |
| [Part 2 — Nginx, PM2, Certbot Walkthrough](./10-deployment-aws-ec2-part2.md) | 3.5–3.11 | AL2023 + Node 24 lab: env files, PM2 cluster, reverse proxy, Let's Encrypt, deliberate 502, SELinux |
| [Part 3 — ALB, Auto Scaling, CI/CD, Hardening & Ops](./10-deployment-aws-ec2-part3.md) | 3.12–3.22 · 4. Full Example · 5. Diagrams Index | EIP/EBS, ALB+ACM, ASG, CloudWatch, OIDC/CodeDeploy, SSM, cost, 502/504, Fargate/Lambda, Route 53, six pillars |
| [Part 4 — Resources, Practice, Interview Questions & Revision](./10-deployment-aws-ec2-part4.md) | 6–11 | Curated resources, a ~16.5 h path, 10 exercises, 36 questions, red flags, recap |

> 💡 Interview Tip: The 2019 blog (public `t2.micro`, open 22, Certbot, Elastic IP) is the **lab**. The senior sentence is: "Private ASG behind an ALB, ACM, instance profile, SSM, `/readyz`."

## Related Files

- Graceful shutdown, `trust proxy`, `/readyz` vs `/healthz` → [06-nodejs](./06-nodejs.md)
- GitHub Actions, OIDC, secrets → [08-engineering-practices](./08-engineering-practices.md)
- L4 vs L7, sticky sessions, scale ladder → [09-system-design](./09-system-design.md)
- S3, pre-signed, CloudFront → [11-deployment-aws-s3.md](./11-deployment-aws-s3.md)
- DNS, CDN, WAF in front of the ALB → [12-cloudflare.md](./12-cloudflare.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./10-deployment-aws-ec2-part1.md), then continue to [11-deployment-aws-s3.md](./11-deployment-aws-s3.md).
