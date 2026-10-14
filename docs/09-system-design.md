# 09 — System Design

> This topic is split into five parts. Start with Part 1 and follow the "Next" links. This is the **45-minute interview shape**, not a vendor tutorial. Postgres replication/partitioning: [07 Part 2 §3.14](./07-databases-and-apis-part2.md#314-replication-partitioning-and-sharding). CAP/PACELC: [07 Part 3 §3.17](./07-databases-and-apis-part3.md#317-sql-vs-nosql-cap-and-pacelc). Redis cache-aside, Lua limiters, WebSocket backplane, BullMQ: [06](./06-nodejs.md). SLOs: [08](./08-engineering-practices-part4.md#328-slis-slos-and-sentry). ALB/Nginx: [10](./10-deployment-aws-ec2.md). S3 uploads: [11](./11-deployment-aws-s3.md). CDN products: [12](./12-cloudflare.md). Consistent hashing (10k keys, ratio 1.23), token-bucket burst (10/20), and a circuit breaker were run on **Node 24.21** in October 2026.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Framework, Estimation, Scale, Load Balancing](./09-system-design-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.4 | 45-minute spine, Fermi math, stateless apps, L4 vs L7 |
| [Part 2 — Cache, CDN, Databases, Queues, Consistency](./09-system-design-part2.md) | 3.5–3.9 | Cache-aside and stampedes, edge keys, replica→shard ladder + hash ring, Kafka vs Rabbit vs SQS, PACELC in a design |
| [Part 3 — Rate Limiter, URL Shortener, Chat, Notifications](./09-system-design-part3.md) | 3.10–3.13 | Four full designs: Redis limiter, short codes, WS fan-out, multi-channel notifications |
| [Part 4 — Feed, Files, Typeahead, Frontend, Reliability](./09-system-design-part4.md) | 3.14–3.22 · 4. Full Example · 5. Diagrams Index | Hybrid feed, pre-signed uploads, trie top-k, FE design, breakers, monolith vs services, sagas, IDs, geo/video skim |
| [Part 5 — Resources, Practice, Interview Questions & Revision](./09-system-design-part5.md) | 6–11 | Curated resources, a ~39 h path, 10 exercises, 36 questions with model answers, red flags, one-page recap |

> 💡 Interview Tip: Narrate assumptions (`DAU=10M`, `eventual OK on the feed`). The timer is measuring how you think, not whether Kafka appears in minute two. Most full-stack prompts fit on **one primary + replicas + Redis + a queue**.

## Related Files

- Redis cache, rate limits, WebSockets, jobs, outbox relay → [06-nodejs](./06-nodejs.md)
- Replication, partitioning, when to shard, CAP/PACELC, idempotency keys → [07-databases-and-apis](./07-databases-and-apis.md)
- SLOs, feature flags, CI budgets → [08-engineering-practices](./08-engineering-practices.md)
- ALB, Nginx, Auto Scaling → [10-deployment-aws-ec2.md](./10-deployment-aws-ec2.md)
- Pre-signed URLs, multipart, CloudFront → [11-deployment-aws-s3.md](./11-deployment-aws-s3.md)
- CDN, cache keys, Workers at the edge → [12-cloudflare.md](./12-cloudflare.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./09-system-design-part1.md), then continue to [10-deployment-aws-ec2.md](./10-deployment-aws-ec2.md).
