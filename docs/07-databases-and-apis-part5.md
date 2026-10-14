# 07 — Databases & APIs (Part 5 of 5): Resources, Practice, Interview Questions & Revision

> **Parts:** [Part 1 — Overview, Topic Map, SQL, Indexes, EXPLAIN, N+1 & Normalization](./07-databases-and-apis-part1.md) · [Part 2 — Transactions, Isolation, MVCC, Locking & Running Postgres](./07-databases-and-apis-part2.md) · [Part 3 — MongoDB, Redis, Choosing a Database & ORMs](./07-databases-and-apis-part3.md) · [Part 4 — API Design](./07-databases-and-apis-part4.md) · **Part 5 — Resources, Practice, Interview Questions & Revision**
>
> Applies to: PostgreSQL 18, MongoDB 8, Redis 8, Prisma 7, Drizzle 0.45, tRPC 11 — as of October 2026. Verify version-specific claims on the official docs.

## Table of Contents

- [6. Resources](#6-resources)
- [7. How to Learn It](#7-how-to-learn-it)
- [8. Hands-on Practice](#8-hands-on-practice)
- [9. Interview Questions](#9-interview-questions)
  - [Basic](#basic)
  - [Intermediate](#intermediate)
  - [Advanced](#advanced)
  - [Tricky](#tricky)
- [10. Common Mistakes & Red Flags](#10-common-mistakes--red-flags)
- [11. Quick Revision Summary](#11-quick-revision-summary)
- [Next Steps](#next-steps)

---

## 6. Resources

| Subtopic | Resource | Type | Where to find it | Free/Paid | Why it's good |
|----------|----------|------|------------------|:---------:|---------------|
| Postgres, all of it | PostgreSQL 18 docs | docs | postgresql.org/docs/18 | Free | Isolation, MVCC, indexes, `EXPLAIN`, partitioning — the source of truth |
| Versioning | PostgreSQL versioning policy | docs | postgresql.org/support/versioning | Free | Which majors are still supported (14 EOL November 2026 — verify) |
| Indexes | *Use The Index, Luke* | book/site | use-the-index-luke.com | Free | Composite order, covering, paging — DBMS-agnostic with SQL examples |
| SQL practice | PostgreSQL Exercises | exercises | pgexercises.com | Free | Joins, window functions, CTEs on a real schema |
| SQL practice | SQLBolt; LeetCode "SQL 50" | exercises | sqlbolt.com; leetcode.com | Free | Drills; don't stop at these for interviews |
| Isolation | Postgres "Concurrency Control" (ch. 13) | docs | postgresql.org/docs/18/mvcc.html | Free | What each level actually allows in Postgres (RR ≠ the SQL standard) |
| Deep theory | *Designing Data-Intensive Applications* (Kleppmann), ch. 2, 5–9 | book | O'Reilly | Paid | Replication, partitioning, transactions, CAP — the senior vocabulary |
| Planner | "Using EXPLAIN" | docs | postgresql.org/docs/18/using-explain.html | Free | How to read the node types this file measures |
| JSONB / FTS / uuidv7 | Postgres 18 functions + JSON docs | docs | postgresql.org/docs/18 | Free | `uuidv7()`, `JSON_TABLE`, `tsvector` |
| pgvector | pgvector README | repo | github.com/pgvector/pgvector | Free | Operators, HNSW vs IVFFlat, iterative scans |
| PgBouncer | PgBouncer docs: pooling modes | docs | pgbouncer.org/usage.html | Free | Session vs transaction vs statement; prepared statements gotcha |
| MongoDB modeling | "Data Modeling" + ESR index rule | docs | mongodb.com/docs | Free | Embed vs reference; compound index order |
| MongoDB courses | MongoDB University | course | learn.mongodb.com | Free | Aggregation and indexes with labs |
| Redis types | Redis "Data types" + persistence | docs | redis.io/docs | Free | Structures, RDB/AOF, eviction policies |
| Prisma 7 | Prisma ORM v7 docs + upgrade guide | docs | prisma.io/docs/orm/v7; prisma.io/docs/orm/more/upgrade-guides | Free | Adapter requirement, `prisma.config.ts`, what 8 RC changes |
| Drizzle | Drizzle ORM docs | docs | orm.drizzle.team | Free | SQL-in-TS; relational queries |
| Kysely | Kysely docs | docs | kysely.dev | Free | Typed SQL when you outgrow the ORM |
| REST | MDN HTTP methods & status codes; Zalando RESTful guidelines | docs | MDN; opensource.zalando.com/restful-api-guidelines | Free | Safe vs idempotent; pragmatic REST |
| Pagination | Use The Index, Luke "Paging"; Slack engineering on cursors | article | use-the-index-luke.com; slack.engineering | Free | Why OFFSET dies; cursor design |
| Idempotency | Stripe "Idempotent requests" + Stripe blog on idempotency | docs/blog | docs.stripe.com; stripe.com/blog | Free | The key/hash/response contract we implemented |
| GraphQL | graphql.org/learn; DataLoader README | docs/repo | graphql.org; github.com/graphql/dataloader | Free | Resolver model; batch+cache |
| tRPC | tRPC v11 docs | docs | trpc.io | Free | Procedures, context, TanStack Query adapter |
| gRPC | grpc.io docs | docs | grpc.io/docs | Free | Stubs, deadlines, streaming |
| OpenAPI | OpenAPI Specification 3.1 | spec | spec.openapis.org | Free | The contract language |
| Webhooks | Stripe webhooks docs | docs | docs.stripe.com/webhooks | Free | Signatures, retries, ordering |
| HTTP internals | Hussein Nasser HTTP videos | video | YouTube | Free | 1.1 vs 2 vs 3, HOL blocking — check the date |
| CAP/PACELC | Abadi's PACELC post; DDIA ch. 9 | article/book | dbmsmusings.blogspot.com; O'Reilly | Free/Paid | The model that fixes "Mongo is AP" |
| Migrations | Stripe engineering posts on online migrations | blog | stripe.com/blog | Free | Expand/contract in production language |

> 💡 Interview Tip: Database blog posts age. A 2018 article that says "Mongo has no transactions" is wrong (they shipped in 4.0). Check the version the author was on.

---

## 7. How to Learn It

Total: **~42.5 hours** (matches the [syllabus](./01-fullstack-syllabus.md#6-databases) Databases 28 h + [APIs 14.5 h](./01-fullstack-syllabus.md#7-apis)). Prerequisites: [06-nodejs](./06-nodejs.md) (the service around the queries) and [03-typescript](./03-typescript.md).

| Step | What to do | Time |
|------|-----------|:----:|
| **0. Self-assess** | Tick the [Topic Map](./07-databases-and-apis-part1.md#2-topic-map). Answer the [Tricky](#tricky) questions cold. | 1 h |
| **1. SQL & indexes** | [Part 1 §3.1–3.4](./07-databases-and-apis-part1.md). Seed the shop DB. Predict five `EXPLAIN ANALYZE` plans, then run them. Flip a composite index's column order and watch the buffers. | 7 h |
| **2. Transactions** | [Part 2 §3.7–3.10](./07-databases-and-apis-part2.md). Reproduce lost update, write skew, `SKIP LOCKED`, a deadlock. Draw MVCC versions for an `UPDATE`. | 5 h |
| **3. Running Postgres** | [Part 2 §3.11–3.14](./07-databases-and-apis-part2.md). JSONB GIN vs expression index; PgBouncer transaction mode; an expand/contract rename; one partitioned table. | 5.5 h |
| **4. MongoDB** | [Part 3 §3.15](./07-databases-and-apis-part3.md#315-mongodb-modeling-indexes-aggregation-transactions). Model a blog both ways; `explain` an ESR query; a 4-stage aggregation; a replica-set transaction. | 3 h |
| **5. Redis structures** | [Part 3 §3.16](./07-databases-and-apis-part3.md#316-redis-data-structures-persistence-and-eviction). Leaderboard, stream consumer group, JSON path. Write down persistence + eviction for "cache" vs "session store". | 2 h |
| **6. Choice & ORMs** | [Part 3 §3.17–3.18](./07-databases-and-apis-part3.md#317-sql-vs-nosql-cap-and-pacelc). Same schema in Prisma 7 and Drizzle; log SQL. Justify a DB for three products. | 3 h |
| **7. REST/HTTP contract** | [Part 4 §3.19–3.23](./07-databases-and-apis-part4.md). ETags, CORS preflight, keyset cursor, idempotent payments, OpenAPI snippet. | 6 h |
| **8. Other styles** | [Part 4 §3.24–3.28](./07-databases-and-apis-part4.md). GraphQL + DataLoader (prove query count); skim tRPC and gRPC; verify a webhook HMAC. | 5.5 h |
| **9. Interview questions** | Answer every [question](#9-interview-questions) out loud in ≤ 2 minutes. | 3 h |
| **10. Revise** | [Quick Revision Summary](#11-quick-revision-summary) at +1 day, +1 week, the day before. | 1.5 h |

```mermaid
flowchart LR
    A[Self-assess 1 h] --> B[SQL & indexes 7 h] --> C[Transactions 5 h] --> D[Running Postgres 5.5 h]
    D --> E[Mongo 3 h] --> F[Redis 2 h] --> G[Choice & ORMs 3 h]
    G --> H[REST/HTTP 6 h] --> I[Other styles 5.5 h] --> J[Interview Qs 3 h] --> K[Revise 1.5 h]
```

> 💡 Interview Tip: Steps 1–2 are the discriminator. Everyone has used Prisma. Few candidates can read `Buffers: shared read=1851` and say "wrong leading column".

---

## 8. Hands-on Practice

| # | Exercise | Level | Acceptance criteria |
|---|----------|:-----:|---------------------|
| 1 | **Window-function report** — per user: last order at, running spend, rank in their country | 🟢 Easy | One SQL statement with `PARTITION BY`; no application loop; `EXPLAIN` shows no nested-loop-per-user |
| 2 | **Index lab** — the Part 1 shop queries: user orders, case-insensitive email, pending queue | 🟢 Easy | You write the predicted plan *before* `EXPLAIN ANALYZE`; composite order is equality-then-sort; a function on a column is rewritten *or* indexed; `CREATE INDEX CONCURRENTLY` used on a live table |
| 3 | **Isolation lab** — lost update, non-repeatable read, write skew | 🟡 Medium | Two `psql` sessions (or two `pg.Client`s) reproduce each anomaly; you fix lost update two ways (`UPDATE … WHERE version` and `SELECT FOR UPDATE`); write skew only disappears under `SERIALIZABLE` with a retry on `40001` |
| 4 | **Job queue in SQL** — `SKIP LOCKED` workers | 🟡 Medium | Two workers cannot take the same row; a crash mid-job returns it after a timeout; `EXPLAIN` uses the skip-locked index |
| 5 | **Expand/contract rename** of `users.name` → `display_name` | 🟡 Medium | Three deploys: add column + backfill in batches with `FOR UPDATE SKIP LOCKED` or keyset, dual-write, drop old column. No exclusive lock held for more than a fraction of a second on the 100k-row table |
| 6 | **Mongo blog** — posts, comments, tags | 🟡 Medium | You embed *or* reference with a written reason; ESR index proven with `explain` (docs examined = limit); a 4-stage aggregation; `$jsonSchema` rejects a bad insert |
| 7 | **Prisma vs Drizzle vs SQL** — same "users with posts" feature | 🟡 Medium | Logged SQL committed next to the code; Prisma `include` shown as two queries; a join written in Kysely or `pg`; N+1 test fails the PR if query count > 2 |
| 8 | **Idempotent payments API** | 🔴 Hard | Concurrent retries (two clients, same key) create **one** payment; different body → 409; key claim and insert in one transaction; Testcontainers Postgres |
| 9 | **GraphQL + DataLoader** | 🔴 Hard | `{ users { posts { title } } }` is 2 SQL statements, not 1+N; a third user doesn't leak via a global loader (test two overlapping requests); depth limit rejects a 10-level query |
| 10 | **Incident: p99 list endpoint is 900 ms** | 🔴 Hard | You get there with `pg_stat_statements` + `EXPLAIN ANALYZE` only (no guessing). Write a one-page note: symptom, plan, fix (index / keyset / query rewrite), before/after times, what you'd monitor |

---

## 9. Interview Questions

### Basic

#### Q1. Clustered vs secondary indexes — does Postgres have a clustered index?

**Model answer.** InnoDB's primary key *is* the table (a clustered B-tree). Postgres heaps are unordered files of pages; **every** index, including the primary key, is secondary and stores a `ctid` (page + tuple) pointing at the heap. `CLUSTER` can rewrite a table in index order once; it doesn't stay that way. Index-only scans work when the visibility map says the page is all-visible.

**Follow-ups:** What's a covering index? Why can HOT updates skip index maintenance?

**Great answer includes:** Heap + ctid vs clustered PK; `INCLUDE`; visibility map; HOT.

#### Q2. Why is `SELECT * FROM t OFFSET 1000000 LIMIT 20` slow, and what do you do instead?

**Model answer.** `OFFSET` still walks and discards a million index (or heap) entries. On the Part 1 dataset, `OFFSET 500000 LIMIT 20` was ~65 ms; a keyset `WHERE (created_at, id) < (?, ?) ORDER BY created_at DESC, id DESC LIMIT 20` was ~0.1 ms. The API returns an opaque `nextCursor`, not a page number.

**Follow-ups:** What if the client wants page 847? What goes in the cursor?

**Great answer includes:** Measured cost; keyset tuple; opaque cursor; offset OK for small stable admin lists; uuidv7 / microsecond pitfall.

#### Q3. `NOT IN (SELECT nullable_col …)` returned no rows. Why?

**Model answer.** Three-valued logic: if the subquery produces a `NULL`, `x NOT IN (…, NULL)` is `UNKNOWN` for every `x`, so `WHERE` filters everything out. Use `NOT EXISTS` (or `<> ALL` after excluding nulls).

**Follow-ups:** `WHERE col = NULL`? (`IS NULL`.) `COUNT(*)` vs `COUNT(col)`?

**Great answer includes:** `UNKNOWN` ≠ `FALSE`; `NOT EXISTS`; `COUNT(*)` counts rows, `COUNT(col)` skips nulls.

#### Q4. What does ACID mean in Postgres?

**Model answer.** Atomicity: commit all or none, via MVCC + abort. Consistency: constraints you declared (`PRIMARY KEY`, `CHECK`, FKs) — not business rules you didn't. Isolation: snapshots and locks, level-dependent. Durability: WAL fsync at commit (`synchronous_commit`).

**Follow-ups:** What if you also send an email? (Outbox.) Can you turn durability down? (`synchronous_commit = off` — don't, except maybe for bulk load.)

**Great answer includes:** WAL vs data pages; constraints vs app invariants; outbox for side effects.

#### Q5. Embed vs reference in MongoDB?

**Model answer.** Embed when the child is bounded, always read with the parent, and has no independent lifecycle (address on a user). Reference when it's unbounded or queried on its own (comments). 16 MiB is the ceiling. Measured: 20 comments embedded fetched in 2.7 ms vs 19.9 ms as a second query — but that ratio flips when comments are paginated.

**Follow-ups:** Many-to-many? Schema validation?

**Great answer includes:** Access pattern first; 16 MiB; `$jsonSchema`; subset pattern (latest N embedded).

#### Q6. Which Redis type for a leaderboard? For a job that must not be lost?

**Model answer.** Leaderboard: **sorted set** (`ZADD` score, `ZREVRANGE`). Job that must not be lost: **stream** with a consumer group (`XADD` / `XREADGROUP` / `XACK`) plus AOF or another durable log — a list `BRPOP` has no replay, pub/sub has no persistence.

**Follow-ups:** Equal scores? Persistence defaults?

**Great answer includes:** ZSET ties; PEL; default RDB can lose minutes; `noeviction` vs `allkeys-lru`.

#### Q7. Safe vs idempotent HTTP methods?

**Model answer.** Safe: no state change (GET/HEAD/OPTIONS). Idempotent: N duplicates = 1 request (safe + PUT + DELETE). POST is neither; clients must not retry it without an Idempotency-Key. PATCH isn't inherently idempotent.

**Follow-ups:** Why never `GET /createOrder`?

**Great answer includes:** Caches and prefetch; 201+Location; DELETE's second call.

#### Q8. Why is CORS not "security"?

**Model answer.** CORS is enforced by browsers. `curl` doesn't care. Server authorization (authn + authz on every request) is the security boundary. CORS is a way to *relax* the same-origin policy for a specific browser origin.

**Follow-ups:** `*` and cookies? Preflight triggers?

**Great answer includes:** Credentials + `*`; JSON POST preflights; Network panel vs `fetch` error.

#### Q9. Prisma vs Drizzle vs raw SQL — when?

**Model answer.** Prisma 7: productive CRUD, schema file, *but* `include` generated two `SELECT`s (users, then posts `IN`), not a join, and you must pass a driver adapter. Drizzle: SQL-shaped TS. Raw/`pg`/Kysely: plans you care about (`FOR UPDATE SKIP LOCKED`, recursive CTEs). Log queries either way.

**Follow-ups:** Prisma 7 vs 8? Migrations at startup?

**Great answer includes:** Adapter + `prisma.config.ts`; pin `@7`; migrations in CI; N+1.

### Intermediate

#### Q10. Composite index column order?

**Model answer.** Equality columns first, then the range or `ORDER BY` column. `(user_id, created_at)` served `WHERE user_id = ? ORDER BY created_at DESC LIMIT 5` in 0.08 ms; `(created_at, user_id)` did 14.8 ms on the same 1M-row table (190×). An index on `(a,b)` also serves `a` alone. Postgres 18 skip scan can use a later column when the leader has few distinct values — a bonus, not a reason to reverse the design.

**Follow-ups:** Partial indexes? `INCLUDE`?

**Great answer includes:** ESR; skip scan caveat; write cost of extra indexes (3.8× inserts in Part 1).

#### Q11. Walk through `EXPLAIN ANALYZE` for a slow query.

**Model answer.** Look at actual time and buffers at the **top node**, then find the node whose actual rows ≫ estimate (bad stats / missing correlation) or a Seq Scan on a selective filter. `shared read` vs `hit` tells you if you're I/O bound. In 18, buffers are on by default. Fix: sargable predicate, right composite index, `CREATE STATISTICS`, rewrite `OFFSET`, kill N+1 in the app.

**Follow-ups:** Nested Loop vs Hash Join vs Merge Join?

**Great answer includes:** Nested loop good for few outer rows; hash for large unordered; merge for pre-sorted; never wrap DML in `EXPLAIN ANALYZE` without a transaction.

#### Q12. Isolation levels in Postgres — which anomalies still happen at the default?

**Model answer.** Default `READ COMMITTED`: snapshot per **statement**. No dirty reads. **Non-repeatable reads, phantoms, lost updates, write skew** all happen. `REPEATABLE READ` takes one snapshot for the transaction, blocks non-repeatable reads and phantoms (stricter than the SQL standard), and the second writer of a lost-update pair gets `40001`. **Write skew** still happens at RR; only `SERIALIZABLE` (SSI) detects it, also with `40001`. App must retry serialization failures.

**Follow-ups:** MySQL RR? Read-your-own-writes on a replica?

**Great answer includes:** Postgres RR ≠ standard RR; `40001`; don't hold RR transactions open.

#### Q13. Four ways to fix a lost update.

**Model answer.** (1) `SELECT … FOR UPDATE` then write, same transaction. (2) Atomic `UPDATE balances SET n = n + $1`. (3) Optimistic `version` column / `If-Match` ETag, 412 on mismatch. (4) `SERIALIZABLE` + retry. Pick (2) when the write is an increment; (3) when the user stared at a form; (1) when you must read then decide.

**Follow-ups:** `SKIP LOCKED`? Deadlocks?

**Great answer includes:** `SKIP LOCKED` for queues, not for "this row must be processed"; deadlocks → consistent lock order + retry.

#### Q14. What does `VACUUM` do, and why does a long transaction hurt?

**Model answer.** MVCC leaves dead tuple versions. `VACUUM` (usually autovacuum) reclaims those that no snapshot still needs, updates the visibility map (needed for index-only scans), and freezes xids to delay wraparound. A transaction held open — idle in transaction, or a forgotten `BEGIN` — pins an old snapshot, so vacuum cannot reclaim anything newer than that xid. Tables bloat, index-only scans start heap-fetching, `pg_stat_activity` shows `idle in transaction`.

**Follow-ups:** Wraparound? `VACUUM FULL`?

**Great answer includes:** Freeze; wraparound is an emergency; `FULL` rewrites and locks; fix the snapshot, don't just vacuum more.

#### Q15. Connection pooling: why PgBouncer, and which mode?

**Model answer.** Each Postgres backend is a process (~few MB). 500 Node connections will OOM or hit `max_connections` long before CPU is done. PgBouncer sits in front. **Transaction mode** returns the server connection at `COMMIT` — right for short transactions, **wrong** for `SET` / temp tables / named prepared statements that must stick to a backend (session mode). Serverless functions that open a process per request *must* pool (PgBouncer, RDS Proxy, Prisma Accelerate-style — check what's still offered).

**Follow-ups:** Pool size vs `max_connections`? Prepared statements in transaction mode?

**Great answer includes:** `default_pool_size` per database/user; protocol-level prepared statements vs SQL `PREPARE`; don't pool inside the app *and* 500 app pools of 10.

#### Q16. Zero-downtime column rename?

**Model answer.** Expand/contract: add `display_name`, backfill in batches, dual-write, deploy readers, drop `name`. `RENAME` is instant in the catalog but old app instances still `SELECT name` during the rolling deploy. `CREATE INDEX CONCURRENTLY` cannot run in a transaction. Set `lock_timeout` so a migration fails instead of queuing behind a long `SELECT`.

**Follow-ups:** Adding a column with a default on PG 11+? (Fast for constant defaults.)

**Great answer includes:** Dual-write window; not running migrations from every pod; `NOT VALID` FKs then `VALIDATE`.

#### Q17. GraphQL N+1 — prove you fixed it.

**Model answer.** Naive resolvers: 1 query for users + 1 per user for posts (3 on a 2-user dataset). DataLoader batches to `WHERE authorId = ANY($1)` — 2 queries. Loaders are **per request**. Prisma `include` is the same batching pattern, still not a SQL join.

**Follow-ups:** Caching across requests? Auth?

**Great answer includes:** Per-request cache; depth/complexity; auth on nested fields.

#### Q18. Design `POST /payments` so retries are safe.

**Model answer.** Require `Idempotency-Key`. Claim the key with `INSERT … ON CONFLICT DO NOTHING` in the same transaction as the payment. Same key + same body hash → replay stored JSON (200). Same key + different hash → 409. Concurrent first requests: one claims, the other `FOR UPDATE`s and replays. TTL the keys. Verified: two successful calls + one conflict still inserted **one** payment.

**Follow-ups:** In-flight first request? GET idempotency?

**Great answer includes:** Body hash; `FOR UPDATE`; don't key GETs.

### Advanced

#### Q19. Write skew with an example.

**Model answer.** Two doctors on call. Constraint: at least one must remain. Both read "on_call count = 2", both set themselves off, both commit. Each transaction's writes don't touch the other's rows, so `REPEATABLE READ` is happy. The invariant is gone. `SERIALIZABLE` aborts one with `40001`. Alternative: lock the relevant rows (`SELECT … FOR UPDATE` of all on-call doctors) or an atomic constraint the database can enforce.

**Follow-ups:** Materialize a `on_call_count` row and update it?

**Great answer includes:** SSI; retry loop; "if it can be a constraint, make it a constraint".

#### Q20. Replication lag and read-your-own-writes.

**Model answer.** Async replica is behind `replay_lag`. User saves, next GET hits the replica, data "vanished". Fixes: primary for a window after writes; session sticky to primary; wait for `pg_last_wal_replay_lsn()` ≥ commit LSN. Don't "fix" it by making every read `SERIALIZABLE` on the primary.

**Follow-ups:** Sync replication cost? Logical vs physical?

**Great answer includes:** `synchronous_commit` levels; logical for upgrades and selective tables.

#### Q21. When do you partition, when do you shard?

**Model answer.** Partition (one server, child tables) when a large table is queried with a time (or tenant) key and you want cheap drops. Shard (several servers) only after indexes, pooling, cache, replicas, and archival. Cross-shard joins/transactions are the cost. Citus / app-level tenant routing / distributed SQL — details in [09](./09-system-design.md).

**Follow-ups:** Partition key in the primary key?

**Great answer includes:** Unique keys must include the partition key; default partition; don't partition small tables.

#### Q22. How does a GIN index on JSONB fail you?

**Model answer.** GIN (`jsonb_path_ops`) accelerates **containment** `@>` (tags, nested objects) — 6.5 ms vs 45–64 ms on 500k docs. Equality on `data->'user'->>'id'` **did not use** that GIN; it needed an expression B-tree (0.10 ms). Updating JSONB rewrites the whole value. If you filter on a key in every row, it's a column.

**Follow-ups:** `jsonb_ops` vs `jsonb_path_ops`?

**Great answer includes:** Expression must match; TOAST; weak stats inside JSON.

#### Q23. MongoDB transactions vs single-document atomicity.

**Model answer.** One document's `updateOne` with `$inc`/`$push` is already atomic. Multi-document transactions need a replica set, are slower, and forbid commands like `drop`. Prefer embedding so the invariant lives in one document; use transactions when you truly update two collections.

**Follow-ups:** Standalone Docker?

**Great answer includes:** `--replSet`; advertised host vs `directConnection`; WiredTiger snapshot cost.

#### Q24. CAP vs PACELC in one minute.

**Model answer.** CAP: during a **partition**, Consistency vs Availability. PACELC: else (no partition) Latency vs Consistency — async replicas, caches, `w:1`. I don't label products AP/CA; I name the write concern and what a failover can lose.

**Follow-ups:** Where does Postgres + async replica sit?

**Great answer includes:** Primary is the consistency boundary; replica reads are ELC=L.

#### Q25. HTTP caching for an authenticated `GET /v1/orders/{id}`.

**Model answer.** `Cache-Control: private, must-revalidate` + strong `ETag`. `If-None-Match` → 304. Never `public` (CDN would mix users). Mutations send `If-Match` → 412 on conflict (same as optimistic `version`).

**Follow-ups:** `no-cache` vs `no-store`?

**Great answer includes:** `no-cache` still stores; `no-store` doesn't; `Vary: Authorization` is not a substitute for `private`.

#### Q26. gRPC vs tRPC vs REST for a new service.

**Model answer.** Browser + partners → REST/OpenAPI. TS monorepo UI → tRPC. Internal streaming / many languages / deadlines → gRPC. Payments create → REST (or any) **plus** idempotency keys; the style doesn't make POST safe.

**Follow-ups:** Can tRPC talk to a Kotlin app?

**Great answer includes:** Publish OpenAPI if you outgrow TS; gRPC-Web for browsers.

#### Q27. Webhook receiver checklist.

**Model answer.** Verify HMAC + timestamp window with `timingSafeEqual`. Unique index on `event.id`. 2xx after persist, work in a queue. Handlers tolerate out-of-order events. Retries are expected.

**Follow-ups:** Why not 500 after you've charged?

**Great answer includes:** At-least-once; sender backoff; secret rotation.

#### Q28. How do you stop an ORM from destroying production?

**Model answer.** Query log in staging; budget queries per endpoint in tests; `pg_stat_statements` top-N weekly; raw SQL for hot paths; `EXPLAIN` in code review for new list endpoints; never `findMany` in a loop. Prisma `include` is two queries — know that before you add a third level of include.

**Follow-ups:** Generated migrations wrapping `CONCURRENTLY`?

**Great answer includes:** Opt out of the transaction; `lock_timeout`.

#### Q29. `pgvector` recall vs latency.

**Model answer.** HNSW is approximate. On 50k random 128-d vectors, `ef_search=40` was 1.3 ms and **2/10** recall — random vectors are a worst case. `ef_search=200` → 3.9 ms / 7/10; 1000 → 10.9 ms / 10/10. Measure on *your* embeddings. Filters apply after candidates unless iterative scans are on.

**Follow-ups:** When to leave Postgres?

**Great answer includes:** Keep pgvector until QPS/size force a dedicated store.

#### Q30. Design cursor pagination for a feed that can insert at the top.

**Model answer.** Keyset on `(created_at DESC, id DESC)`. New inserts have a larger cursor key so they don't appear in a page you're paging *older* through (they show on refresh of the first page). Don't use `OFFSET`. Don't decode JS `Date` milliseconds against `timestamptz`. Tie-break with `uuidv7` or `id`.

**Follow-ups:** Realtime new items?

**Great answer includes:** SSE/WebSocket for the head of the feed; cursor for history.

### Tricky

#### Q31. Postgres `READ UNCOMMITTED` — can you dirty-read?

**Model answer.** **No.** Postgres maps it to `READ COMMITTED`. MVCC never exposes uncommitted tuples. An interviewer quoting the SQL standard table is testing whether you've read the Postgres chapter.

**Follow-ups:** Which standard anomaly does PG RR still allow? (Write skew.)

**Great answer includes:** "Internally three levels"; SSI.

#### Q32. `WHERE created_at::date = '2025-03-10'` is slow despite an index on `created_at`.

**Model answer.** The cast is a **function on the column** → not sargable; the planner can't turn it into a range. It also depends on `TimeZone`. Rewrite as `created_at >= date AND created_at < date+1`. Part 1: 68 ms vs 0.18 ms.

**Follow-ups:** `lower(email) = `?

**Great answer includes:** Expression index if you can't rewrite; collation/`text_pattern_ops` for `LIKE 'prefix%'`.

#### Q33. Two Fastify instances, `SELECT FOR UPDATE` job queue, still double-process a job. Why?

**Model answer.** Usual causes: (1) each instance used a connection pool and the `SELECT` and `UPDATE` ran on **different clients** (not one transaction). (2) After taking the row they committed, then crashed before side effects — no lease/timeout, another worker takes it. (3) They used `FOR UPDATE` but then processed **outside** the transaction, so the lock was gone. Fix: one client per job, `UPDATE … SET locked_at, locked_by WHERE id = … AND locked_at IS NULL RETURNING *` or `SKIP LOCKED` **inside** the same transaction as the state change, idempotent workers, lease timeout.

**Follow-ups:** Why `SKIP LOCKED` vs `NOWAIT`?

**Great answer includes:** `NOWAIT` errors; `SKIP LOCKED` skips; outbox for the side effect.

#### Q34. Prisma `include` looks like a join in TypeScript. Is it?

**Model answer.** **No** — verified on 7.10: `SELECT` users, then `SELECT` posts `WHERE authorId IN ($1,$2)`. It's DataLoader batching. Nested `include` trees can explode into many queries. `$queryRaw` or Kysely when you need one join.

**Follow-ups:** `relationJoins` preview / Prisma 8?

**Great answer includes:** "I log the SQL"; don't guess from the TS shape. (Prisma 8 is RC — verify before claiming joins.)

#### Q35. Redis `KEYS *` in production?

**Model answer.** O(N) on the keyspace, **blocks the single thread**, stalls every command. Use `SCAN`. Also: `KEYS` in a cluster only sees one slot's view depending on where you sent it. Monitoring that uses `KEYS` is an outage waiting to happen.

**Follow-ups:** `SMEMBERS` on a million-member set?

**Great answer includes:** `SSCAN`; `HGETALL` vs `HSCAN`; Redis is single-threaded for command execution.

#### Q36. Client sends `Idempotency-Key` on a GET. Harmless?

**Model answer.** Harmless if you ignore it. Harmful if you cache GET responses *by that key* across users or mix it with a POST store — GETs are already idempotent and cacheable by URL+auth. Keys are for **unsafe non-idempotent** requests. Also harmful: generating the key server-side per attempt (defeats the point — the *client* must reuse it).

**Follow-ups:** Should DELETE send a key?

**Great answer includes:** DELETE is idempotent; keys still help if DELETE has side effects that aren't (webhook out). Prefer making the handler truly idempotent.

---

## 10. Common Mistakes & Red Flags

| Red flag | Why it hurts | Say/do instead |
|----------|--------------|----------------|
| "Add an index on every `WHERE` column" | Write amplification; unused indexes; still Seq Scans on low-selectivity cols | Composite order, partial indexes, `pg_stat_user_indexes`, measure |
| `OFFSET` for infinite scroll | Slow + duplicates | Keyset cursor |
| `NOT IN` subquery | NULL wipes the result | `NOT EXISTS` |
| "We're `SERIALIZABLE` so we're safe" without retry | `40001` surfaces as 500s | Retry loop with jitter |
| Open transaction while calling HTTP | Held locks, vacuum freeze, pool exhaustion | Short transactions; outbox |
| Migrations at app boot | Race across replicas | CI/CD migrate job |
| `CREATE INDEX` on 50M rows in a txn | Hours of blocked writes | `CONCURRENTLY` + `lock_timeout` |
| Prisma/Mongoose without query logs | Silent N+1 | Log SQL; budget queries in tests |
| "Mongo is schemaless, so we skip validation" | Garbage documents | `$jsonSchema` + app schema |
| Redis as source of truth, default RDB, `noeviction` | Data loss / OOM | Name the job: cache vs store; AOF + `maxmemory` |
| "Mongo is AP" | CAP as a brand | Write concern, PACELC |
| `GET` that creates data | Cached, prefetched, retried | POST + idempotency key |
| `Access-Control-Allow-Origin: *` with cookies | Browser rejects or you over-permit | Explicit origin; authz still on server |
| Global DataLoader | Cross-user cache | Per request |
| Webhook 200 after a throw | Lost event / double work | Persist then 2xx; queue; unique event id |
| Page numbers in a public API | Offset | Opaque cursor |

---

## 11. Quick Revision Summary

### One-page recap

**Postgres**
- Heap + secondary B-trees (ctid). Index-only scans need the visibility map. Composite: **equality, then sort/range**. PG 18 skip scan is a bonus. Function on a column kills the index. `LIKE 'x%'` needs `C` collation or `text_pattern_ops`.
- `EXPLAIN ANALYZE` (buffers default in 18): estimates vs actuals, `shared read`. Nested loop / hash / merge.
- Default `READ COMMITTED`: lost updates & write skew live here. RR: one snapshot, still write skew. Serializable: SSI, retry `40001`.
- MVCC → dead tuples → `VACUUM`. Long `idle in transaction` pins snapshots. WAL is durability.
- JSONB: GIN for `@>`, expression B-tree for `->>`. FTS: `tsvector` + GIN. `uuidv7()`. pgvector HNSW: measure recall.
- Pool via PgBouncer **transaction** mode for short txns. Expand/contract deploys. Partition before shard. Async replica: read-your-writes.

**Mongo / Redis / ORMs**
- Embed bounded 1:few; reference unbounded. ESR indexes. Aggregation: `$match` first. Transactions need a replica set; prefer one-document atomicity.
- Redis: STRING/HASH/LIST/SET/ZSET/STREAM/JSON. Streams for at-least-once; pub/sub is fire-and-forget. RDB vs AOF; `maxmemory-policy`.
- CAP during partitions; PACELC otherwise. Don't brand products.
- Prisma 7: adapter required, `include` = two SELECTs. Drizzle/Kysely closer to SQL. Pin Prisma 7; 8 is RC. Mongo ≠ Prisma 7.

**APIs**
- Safe vs idempotent; POST needs Idempotency-Key (claim row + hash + replay). Keyset cursors. ETag / If-Match. CORS is a browser relaxation.
- GraphQL N+1 → DataLoader per request. tRPC for TS monorepos. gRPC for internal streaming. Webhooks: HMAC, timestamp, unique event id, 2xx then queue.
- HTTP/2 multiplexes; HTTP/3 is QUIC. Don't 0-RTT a POST.

### Last-day checklist

- [ ] I can draw a B-tree lookup and say why `(user_id, created_at)` beats `(created_at, user_id)`.
- [ ] I can read an `EXPLAIN ANALYZE` cold and name the join type.
- [ ] I can reproduce a lost update and a write skew, and name the fix for each.
- [ ] I can explain what `VACUUM` cannot remove while a transaction is open.
- [ ] I can pick embed vs reference and an ESR index for a Mongo collection.
- [ ] I can choose a Redis type + persistence + eviction for cache vs sessions vs jobs.
- [ ] I can describe Prisma `include` SQL without lying that it's a join.
- [ ] I can design keyset pagination and idempotent POST.
- [ ] I can fix GraphQL N+1 with a per-request DataLoader.
- [ ] I can answer Q31–Q36 cold.

---

## Next Steps

- Update your Databases & APIs rows in the [Progress Tracker](./00-README.md#progress-tracker).
- Keep the shop database from Part 1 as a sandbox: every new index or query, `EXPLAIN ANALYZE` first.
- ➡️ Continue to [08-engineering-practices.md](./08-engineering-practices.md) — SOLID, testing, Git, CI/CD, Docker, monorepos, security and monitoring. SQL injection and XSS belong there; this file stopped at parameterized queries and webhook signatures.
