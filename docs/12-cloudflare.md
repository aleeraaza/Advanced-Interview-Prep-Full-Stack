# 12 — Cloudflare

> This topic is split into three parts. Start with Part 1 and follow the "Next" links. Product names, plan quotas, Worker CPU limits, and [IP ranges](https://www.cloudflare.com/ips/) change — verify on [developers.cloudflare.com](https://developers.cloudflare.com) the morning you use them. CDN *theory*: [09 §3.6](./09-system-design-part2.md#36-cdns-and-edge-caching). Origin box / ALB: [10](./10-deployment-aws-ec2.md). CloudFront OAC / S3: [11](./11-deployment-aws-s3.md). This writing session did **not** change your zones, Workers, or AWS security groups — the Part 2 walkthrough is yours to run.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — DNS, CDN, TLS](./12-cloudflare-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.3 | Nameservers, orange vs grey, cache keys / Cache Rules / purge, Flexible vs Full (strict), Origin CA, Authenticated Origin Pulls |
| [Part 2 — Origin Lock, WAF, Rules](./12-cloudflare-part2.md) | 3.4–3.7 | Domain in front of EC2/ALB, Cloudflare IP SG, WAF + DDoS, rate limit `/api/login`, Page Rules → modern Rulesets |
| [Part 3 — Workers, R2, Tunnel, Interview](./12-cloudflare-part3.md) | 3.8–3.14 · 4–11 | V8 isolates, Pages, R2 SDK v3, KV vs D1 vs Durable Objects, `cloudflared`, Access, vs CloudFront, ~9.25 h path, 10 exercises, 36 questions |

> 💡 Interview Tip: "We use Cloudflare" is DNS trivia. The senior sentence is: "Orange-cloud, Full (strict), origin locked (Tunnel or IPs+AOP), `/api` bypass cache, Workers for flags, Durable Objects if it must be correct."

## Related Files

- L4 vs L7, CDN in a design → [09-system-design](./09-system-design.md)
- Nginx, ALB, `trust proxy`, SSM → [10-deployment-aws-ec2](./10-deployment-aws-ec2.md)
- S3, pre-signed PUT, CloudFront OAC → [11-deployment-aws-s3](./11-deployment-aws-s3.md)
- CORS / CSRF as browser gates → [08-engineering-practices](./08-engineering-practices-part4.md#321-csrf-and-cors)
- Redis per-user rate limits → [06-nodejs](./06-nodejs-part2.md#315-rate-limiting-with-redis)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./12-cloudflare-part1.md), then continue to [13-coding-round-practice.md](./13-coding-round-practice.md).
