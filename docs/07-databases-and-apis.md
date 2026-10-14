# 07 — Databases & APIs

> This topic is split into five parts. Start with Part 1 and follow the "Next" links. Applies to **PostgreSQL 18** (verified on 18.6; 19 is still beta). **MongoDB 9.0** is current; the Mongo examples were run on **8.3.13** (`mongo:8`). Also **Redis 8.10**, **Prisma ORM 7.10** (Prisma 8 is a release candidate as of October 2026 — pin `prisma@7`), **Drizzle 0.45**, **Kysely 0.29**, **Mongoose 9**, **tRPC 11**, **GraphQL Yoga 5**. Node stays on **24 LTS**. Check postgresql.org/support/versioning and each project's changelog before you quote a default.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — SQL, Indexes & Query Performance](./07-databases-and-apis-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.6 | Heap vs indexes, TOAST, SQL interviewers ask (joins, `NOT IN`/`EXISTS`, CTEs, windows), B-tree design (composite order, covering, partial, skip scan, GIN/GiST/BRIN), `EXPLAIN ANALYZE` with measured plans on 1M orders, N+1 and keyset pagination from Node, normalization |
| [Part 2 — Transactions, MVCC & Running Postgres](./07-databases-and-apis-part2.md) | 3.7–3.14 | ACID and WAL, isolation anomalies reproduced, lost updates and `SKIP LOCKED`, deadlocks, MVCC/`VACUUM`/bloat, JSONB, full-text search, pgvector, PgBouncer, expand/contract migrations, replication, partitioning, sharding |
| [Part 3 — MongoDB, Redis, Choosing a Database & ORMs](./07-databases-and-apis-part3.md) | 3.15–3.18 | Embed vs reference, ESR indexes, aggregation, replica-set transactions; Redis types, persistence, eviction; CAP and PACELC; Prisma 7 vs Drizzle vs Kysely (generated SQL) |
| [Part 4 — API Design](./07-databases-and-apis-part4.md) | 3.19–3.28 · 4. Full Example · 5. Diagrams Index | REST safe vs idempotent, HTTP caching/CORS/versions, cursor pagination as a contract, idempotency keys, versioning and OpenAPI, GraphQL + DataLoader, tRPC, gRPC, webhooks, choosing a style |
| [Part 5 — Resources, Practice, Interview Questions & Revision](./07-databases-and-apis-part5.md) | 6–11 | Curated resources, a ~42.5 h learning path, 10 graded exercises, 36 interview questions with model answers, red flags, one-page recap and last-day checklist |

> 💡 Interview Tip: SQL plans and isolation anomalies in Parts 1–2 were measured on a seeded shop database (100k users, 1M orders) in Postgres 18. Mongo ESR (20 vs 1,901 docs examined), Redis structures (including `JSON.SET` on Redis 8), Prisma `include` (two `SELECT`s, not a join), GraphQL DataLoader (3 queries → 2), and idempotent payments (one row after retry + 409) were re-run on Node 24 in October 2026. If a number matters in an interview, re-measure it on your machine.

## Related Files

- Parameterized queries, `pg` pooling, keyset notes repo, Redis as cache/lock/rate-limit, auth, webhooks-as-jobs → [06-nodejs](./06-nodejs.md)
- Zod at the HTTP edge, typed env → [03-typescript](./03-typescript.md)
- Next.js Route Handlers, Server Actions, cache tags → [05-nextjs](./05-nextjs.md)
- Testing pyramid, Docker, CI running migrations → [08-engineering-practices.md](./08-engineering-practices.md)
- Replication, sharding, queues at system-design granularity → [09-system-design.md](./09-system-design.md)
- S3 for blobs you shouldn't put in Postgres/Mongo → [11-deployment-aws-s3.md](./11-deployment-aws-s3.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./07-databases-and-apis-part1.md), then continue to [08-engineering-practices.md](./08-engineering-practices.md).
