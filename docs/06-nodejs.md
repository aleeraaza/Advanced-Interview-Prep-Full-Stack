# 06 — Node.js

> This topic is split into four parts. Start with Part 1 and follow the "Next" links. Applies to **Node.js 24 LTS** (notes call out differences in 22 LTS), with **Express 5**, **Fastify 5**, **NestJS 12**, **BullMQ 6**, **ioredis 6**, **Pino 10** and **OpenTelemetry JS**. Node 24 enters Maintenance LTS on 2026-10-20 and Node 26 becomes Active LTS on 2026-10-28 — check the schedule at github.com/nodejs/Release.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Runtime, Event Loop, Streams & Concurrency](./06-nodejs-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.7 Detailed Explanations | V8, libuv and the bindings; event loop phases, nextTick vs microtasks (ESM vs CJS), the libuv 1.45 timer change; the thread pool with benchmarks; Buffers, streams and backpressure (measured); cluster vs `worker_threads` vs `child_process` with a worker pool; typed `EventEmitter` and `AsyncLocalStorage`; modern built-ins |
| [Part 2 — Express, Fastify, NestJS, Auth, Rate Limiting, Uploads & Real-time](./06-nodejs-part2.md) | 3.8–3.17 Detailed Explanations | Express 5 internals and behavior changes; error hierarchy and process handlers; Zod validation and config; a production-shaped Express app; Fastify and NestJS 12; passwords (argon2), EdDSA access tokens, rotating refresh tokens with reuse detection, OAuth2 + PKCE; Redis rate limiters in Lua; streamed uploads to S3; SSE and WebSockets across instances |
| [Part 3 — Redis Caching, Queues, Observability, Shutdown, Security, Testing & Profiling](./06-nodejs-part3.md) | 3.18–3.25 Detailed Explanations · 4. Full Example · 5. Diagrams Index | Cache-aside with stampede protection; BullMQ jobs, retries and schedulers; Pino with request context; OpenTelemetry in ESM, Prometheus metrics, health checks; graceful shutdown; OWASP API risks, SSRF, prototype pollution, ReDoS; Supertest + Testcontainers; heap-snapshot leak hunting; the full notes service in Docker |
| [Part 4 — Resources, Practice, Interview Questions & Revision](./06-nodejs-part4.md) | 6. Resources · 7. How to Learn It · 8. Hands-on Practice · 9. Interview Questions · 10. Common Mistakes · 11. Quick Revision | 30 curated resources, a ~37.5 h learning path, 10 graded exercises, 36 interview questions with model answers, red flags, one-page recap and last-day checklist |

> 💡 Interview Tip: All path-labelled code in Parts 1–3 was type-checked together (`strict`, TypeScript 7) and run on Node 24.21 against real Redis 8, PostgreSQL 18 and S3-compatible containers. The full notes service was built into a Docker image and exercised end to end: login, CRUD, caching, rate limiting, jobs, metrics and `docker stop`. Numbers in the text (memory, timings, orderings) are from those runs. Several "Pitfall" callouts are bugs found during verification — including the SSRF blocklist that blocked every IPv4 address, metrics labels that changed on errors, and a 137 exit code caused by a 1-second stop timeout.

## Related Files

- Promises, the microtask queue, closures and `this` → [02-javascript](./02-javascript.md)
- Typing Express, env validation with Zod, generics → [03-typescript](./03-typescript.md)
- Server-side React and Next.js on Node (Route Handlers, self-hosting) → [05-nextjs](./05-nextjs.md)
- SQL, PostgreSQL, Redis data structures, ORMs, API styles, pagination, idempotency → [07-databases-and-apis.md](./07-databases-and-apis.md)
- Testing pyramid, CI/CD, Docker, monorepos, security practices → [08-engineering-practices.md](./08-engineering-practices.md)
- Rate limiter, chat, notifications and file upload designs → [09-system-design.md](./09-system-design.md)
- Running Node on EC2 with Nginx and PM2 → [10-deployment-aws-ec2.md](./10-deployment-aws-ec2.md); S3 pre-signed and multipart uploads → [11-deployment-aws-s3.md](./11-deployment-aws-s3.md)
- Event-loop output puzzles and EventEmitter/LRU implementations → [14-js-logical-interview-questions.md](./14-js-logical-interview-questions.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./06-nodejs-part1.md), then continue to [07-databases-and-apis.md](./07-databases-and-apis.md).
