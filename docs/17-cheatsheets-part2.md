# 17 — Cheatsheets (Part 2 of 3): Node, Data, Practices, Design

> **Parts:** [Part 1 — JS / TS / React / Next](./17-cheatsheets-part1.md) · **Part 2 — Node / Data / Practices / Design** · [Part 3 — Cloud, Coding, Behavioral, 48 h](./17-cheatsheets-part3.md)
>
> Canonical: [06](./06-nodejs.md)–[09](./09-system-design.md). Do **not** re-derive Redis Lua, CAP internals, Pino/OTel, or OWASP essays here — those files own them. Do **not** start the user's Postgres/Redis containers.

## Table of Contents

- [8. Node.js](#8-nodejs)
- [9. Databases & APIs](#9-databases--apis)
- [10. Engineering Practices](#10-engineering-practices)
- [11. System Design](#11-system-design)
- [Next: Part 3](#next-part-3)

---

## 8. Node.js

Canonical: [06](./06-nodejs.md). Browser loop: [02](./02-javascript.md). Security internals (SSRF, ReDoS, pollution): **06 only**.

| Topic | Recite |
|-------|--------|
| Split | V8 one thread; libuv loop + pool (**4** default: `fs`, `dns.lookup`, crypto, zlib). `UV_THREADPOOL_SIZE` at **launch**. |
| Phases | timers → pending → poll → check (`setImmediate`) → close. After each callback: **nextTick then microtasks**. |
| Puzzle | Inside I/O: nextTick > promise > immediate > timeout. CJS top-level: nextTick before promises; **ESM**: promises first. |
| Streams | `write()` false → `'drain'`. `pipeline()` > `.pipe()`. |
| CPU vs I/O | `worker_threads` pool vs `child_process` vs one process/container (cluster often obsolete). |
| Express 5 | Async rejections forwarded; still **misses** errors outside the promise chain. `req.body` undefined without parser. |
| Errors | Typed `AppError` → one handler → problem+json. Zod env + body. |
| Auth | argon2id; short access JWT; **opaque rotating refresh** + family reuse detection; `HttpOnly`; PKCE. |
| Tokens | Access: memory/short cookie. Refresh: HttpOnly, rotate, reuse = steal. Revoke JWT = denylist or short TTL honesty. |
| Limit | Redis **Lua** token bucket; `429` + `Retry-After`; `trust proxy`. Fail-open vs closed **per route**. |
| Upload | Presign first ([11](./11-deployment-aws-s3.md)); else stream + magic bytes + abort. |
| Cache | Aside, delete-on-write, single-flight + lock + jitter + negative. Redis down → miss. |
| Jobs | BullMQ at-least-once → **idempotent**; DLQ; `worker.close()`. |
| Ops | Liveness ≠ readiness. SIGTERM: fail ready → drain → `server.close()` → pools/OTel → exit. **137** SIGKILL, **143** SIGTERM. |
| Observe | Pino JSON + redaction; OTel ESM loader + `shutdown()`; histograms on **route templates**. |

**Talk 4 min:** access vs refresh location + rotation. **Talk 2 min:** SIGTERM order.

---

## 9. Databases & APIs

Canonical: [07](./07-databases-and-apis.md). CAP path language also [09](./09-system-design.md).

| Topic | Recite |
|-------|--------|
| Index | B-tree secondary; composite **equality then range/sort**. Function on column kills it. `LIKE 'x%'` + `text_pattern_ops` / `C`. |
| Plan | `EXPLAIN ANALYZE`: estimate vs actual, join type (nested/hash/merge). |
| Isolation | Default RC: lost update + write skew. RR: snapshot, still write skew. Serializable: SSI, retry `40001`. |
| MVCC | Dead tuples → `VACUUM`. Idle-in-tx pins snapshots. WAL = durability. |
| JSONB | GIN `@>`; expression B-tree `->>`. |
| Pool | PgBouncer **transaction** mode for short txns. Async replica: read-your-writes issue. |
| Mongo | Embed bounded; reference unbounded. ESR. `$match` first. Txns need replica set. |
| Redis | STRING/HASH/LIST/SET/ZSET/STREAM. Pub/sub ≠ durable. Streams at-least-once. |
| ORM | Prisma `include` = **two SELECTs**, not a SQL join. Pin major. |
| HTTP | Safe vs idempotent. POST: Idempotency-Key + hash + replay. **Keyset** cursors. ETag. CORS ≠ authz. |
| GraphQL | N+1 → DataLoader **per request**. |
| Webhooks | HMAC + timestamp + unique id + 2xx then queue. |
| HTTP/3 | QUIC. Don't 0-RTT a POST. |

**Board:** `(user_id, created_at)` vs reverse for "my recent orders."

---

## 10. Engineering Practices

Canonical: [08](./08-engineering-practices.md). Node security deep: [06](./06-nodejs.md). CWV: [05](./05-nextjs.md). A11y tests: [04](./04-react.md).

| Topic | Recite |
|-------|--------|
| SOLID | Axes of change; DIP = `createApp({ repo })`. Singleton = process resources only. |
| Trophy | Static + some unit + **many integration** + few E2E. Don't mock the thing you're proving. |
| Vitest 5 | Node 22.12+; `clearMocks` on. Fake timers for debounce. |
| Git | Trunk + flags. Squash to `main`. Bisect, reflog, `--force-with-lease`. |
| GHA | `checkout@v7` / `setup-node@v7`. v7 blocks fork checkout on `pull_request_target`. OIDC not long-lived keys. |
| Docker | Layer order, multi-stage, non-root, exec-form CMD. |
| XSS | Encode + CSP. CSRF if **cookies**; Bearer header ≠ CSRF. |
| OWASP 2025 | A03 supply chain · A05 injection · A10 fail-closed. API1 BOLA → 404. `$ne` demo + Zod. |
| SLO | SLI → SLO → error budget. Budget gone → reliability work, not features. |
| a11y | AA + axe CI + RTL **roles**. |

> 💡 Interview Tip: CORS is a **browser** relaxation. Servers still need authz.

---

## 11. System Design

Canonical: [09](./09-system-design.md). OAC/presign: [11](./11-deployment-aws-s3.md). CDN theory vs Cloudflare product: [09](./09-system-design.md) vs [12](./12-cloudflare.md).

**45-min spine**

1. Scale, staleness, failure (2 min)
2. Functional + non-functional (5)
3. Fermi: day/8.6e4 ≈ /s, peak ×5 (3)
4. API + keys (5)
5. Boxes (10)
6. One deep dive (12)
7. Failures + trade-offs (8)

| Lever | Recite |
|-------|--------|
| App | Stateless: sessions/files/crons **out**. Sticky = smell. L7 + `/readyz`. |
| Cache | Aside + delete-on-write + TTL. Stampede: lock/single-flight. Don't cache money. |
| Data | Replica → partition → shard. Consistent hash ~**1/N** moves; vnodes; hot keys remain. CAP **on the path**. |
| Queue | At-least-once + idempotency + DLQ. Outbox not dual-write. SQS vs Kafka = replay + consumer groups. |
| Limiter | Token bucket + Redis Lua ([06](./06-nodejs.md)). |
| Shortener | 302 (not 301), 7-char base62, cache read. |
| Chat | Persist **then** pub/sub. |
| Feed | Hybrid fan-out. |
| Files | Presigned PUT/GET ([11](./11-deployment-aws-s3.md)). |
| Reliability | Timeout → retry (idempotent only) → breaker → bulkhead. |
| Tx | Saga + outbox, not 2PC. UUIDv7 vs Snowflake. |
| Team | Modular monolith first for ~10 people. |

> ⚠️ Pitfall: `% N` for sharding. Ring + vnodes; still pin hot keys.

---

## Next: Part 3

➡️ [Part 3](./17-cheatsheets-part3.md) — AWS, Cloudflare, DSA, puzzles, behavioral, 48-hour script, interview flashcards.
