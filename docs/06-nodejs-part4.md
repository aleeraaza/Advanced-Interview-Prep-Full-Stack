# 06 — Node.js (Part 4 of 4): Resources, Practice, Interview Questions & Revision

> **Parts:** [Part 1 — Overview, Topic Map, Runtime, Event Loop, Streams & Concurrency](./06-nodejs-part1.md) · [Part 2 — Express, Fastify, NestJS, Auth, Rate Limiting, Uploads & Real-time](./06-nodejs-part2.md) · [Part 3 — Redis Caching, Queues, Observability, Shutdown, Security, Testing & Profiling](./06-nodejs-part3.md) · **Part 4 — Resources, Practice, Interview Questions & Revision**
>
> Applies to: Node.js 24 LTS (and 22 LTS unless noted), Express 5, Fastify 5, NestJS 12. Outputs quoted in answers were measured on Node 24.21 (October 2026). Version-specific details: verify in the release notes on nodejs.org and in each library's changelog.

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
| Everything (official) | Node.js API docs, read for **your** major version | docs | nodejs.org/api (version switcher at the top) | Free | The source of truth. Each API shows its stability index and the version it was added in — check both before you quote a feature |
| Event loop | "The Node.js Event Loop" and "Don't Block the Event Loop" guides | docs | nodejs.org/en/learn | Free | The phase model and the official advice on partitioning and offloading work |
| Event loop (talk) | Bert Belder, "Everything You Need to Know About Node.js Event Loop" | video | YouTube (Node Interactive) | Free | From a libuv author. It corrects the common wrong diagrams. Note that it predates the libuv 1.45 timer change ([Part 1 §3.2](./06-nodejs-part1.md#32-the-event-loop-in-depth)) |
| libuv | libuv "Design overview" | docs | docs.libuv.org | Free | Which work runs on the thread pool and which uses OS async I/O, straight from the library |
| Streams | "Backpressuring in Streams" guide + the `stream` API page | docs | nodejs.org/en/learn; nodejs.org/api/stream.html | Free | `highWaterMark`, `write()` returning `false`, and how `pipeline` handles errors |
| Release status | Node.js Release Working Group schedule | repo | github.com/nodejs/Release | Free | Which lines are Current, Active LTS, Maintenance or EOL. Check it before you answer "which version would you run?" |
| Patterns & architecture | *Node.js Design Patterns* (Casciaro & Mammino) | book | Packt; bookstores | Paid | The best book-length treatment of async patterns, streams and scaling. Use the latest edition |
| Best practices | Node.js Best Practices | repo | github.com/goldbergyoni/nodebestpractices | Free | Short, opinionated entries on error handling, security, production and testing, with reasons |
| Express 5 | Express docs + "Migrating to Express 5" guide | docs | expressjs.com | Free | Exactly what changed in 5 (path syntax, async errors, `req.query`, removed methods) |
| Fastify | Fastify docs: "Lifecycle", "Encapsulation", "Validation and Serialization" | docs | fastify.dev/docs | Free | Explains the hooks, plugin scope and Ajv defaults that interviewers ask about |
| NestJS | NestJS docs: "Fundamentals" (providers, scopes, lifecycle) and "Techniques" | docs | docs.nestjs.com | Free | DI scopes, guards, interceptors and pipes — read the request lifecycle page twice |
| Auth | OWASP cheat sheets: "Authentication", "Password Storage", "Session Management" | docs | cheatsheetseries.owasp.org | Free | Current recommendations for hashing parameters, session handling and error messages |
| OAuth 2.0 | RFC 9700 "Best Current Practice for OAuth 2.0 Security"; RFC 7636 (PKCE) | spec | rfc-editor.org; oauth.net/2 | Free | Why implicit flow is gone, PKCE for every client, refresh token rotation and sender-constraining |
| JWT in Node | `jose` README and docs | repo | github.com/panva/jose | Free | Algorithm and key handling done right; pins algorithms and validates claims |
| API security | OWASP API Security Top 10 (2023) | docs | owasp.org | Free | BOLA, broken auth, SSRF and resource consumption — the vocabulary for "how would you secure this API?" |
| Node security | Node.js "Security Best Practices" guide; OWASP "Node.js Security Cheat Sheet" | docs | nodejs.org/en/learn; cheatsheetseries.owasp.org | Free | Threat-model-based list: prototype pollution, ReDoS, HTTP request smuggling, supply chain |
| Rate limiting | Stripe "Scaling your API with rate limiters"; Cloudflare's rate-limiting architecture posts | blog | stripe.com/blog; blog.cloudflare.com | Free | Real production designs: token bucket, concurrency limiters, load shedding |
| Redis | Redis docs: data types, "Scripting with Lua", "Distributed locks" | docs | redis.io/docs | Free | Atomicity of scripts, `SET NX PX`, and what the official lock page says (and doesn't) guarantee |
| Locking caveats | Martin Kleppmann, "How to do distributed locking" | blog | martin.kleppmann.com | Free | Why locks without fencing tokens aren't safe for correctness — the source of the classic follow-up question |
| Queues | BullMQ docs: "Retrying failing jobs", "Job Schedulers", "Deduplication", "Graceful shutdown" | docs | docs.bullmq.io | Free | The 6.x APIs used in [Part 3](./06-nodejs-part3.md#319-background-jobs-with-bullmq) |
| Logging | Pino docs + `pino-http` README | docs | getpino.io; github.com/pinojs/pino-http | Free | Redaction, serializers, transports, and why logging should happen off the main thread |
| Tracing | OpenTelemetry JS docs: "Getting Started — Node.js", "ESM support" | docs | opentelemetry.io/docs/languages/js | Free | The SDK setup and the ESM loader-hook requirement that trips everyone up |
| Metrics | Prometheus docs: "Metric and label naming", "Histograms and summaries" | docs | prometheus.io/docs/practices | Free | Cardinality, buckets and why you aggregate histograms instead of averaging percentiles |
| Operations | Google SRE book, "Monitoring Distributed Systems" chapter | book | sre.google/books | Free | The four golden signals and alerting on symptoms |
| Shutdown | Kubernetes docs "Pod Lifecycle" → "Termination of Pods" | docs | kubernetes.io/docs | Free | The exact SIGTERM → grace period → SIGKILL sequence and how endpoints are removed |
| Testing | Node test runner docs; Supertest README; Testcontainers for Node | docs | nodejs.org/api/test.html; github.com/ladjs/supertest; node.testcontainers.org | Free | Everything used in [Part 3 §3.24](./06-nodejs-part3.md#324-testing-node-apis) |
| Profiling | Node.js "Diagnostics" guides (memory, CPU profiling, flame graphs) | docs | nodejs.org/en/learn | Free | Step-by-step `--cpu-prof`, `--heapsnapshot-signal` and `--inspect` workflows |
| Heap snapshots | Chrome DevTools "Fix memory problems" + "Memory terminology" | docs | developer.chrome.com/docs/devtools | Free | Retainers, shallow vs retained size, comparison view — the same UI you use for Node |
| Profiling tools | Clinic.js (Doctor, Flame, Bubbleprof) | tool | clinicjs.org | Free | Quick diagnosis of loop blocking vs I/O vs GC. Check that it supports your Node version before you rely on it |
| Structured course | API and Node courses on Frontend Masters (e.g. Scott Moss's API design course) | course | frontendmasters.com | Paid | Guided builds with exercises. Check the recording date: many predate Express 5 |

> 💡 Interview Tip: Node.js answers age in specific ways. Pre-2023 material says Express doesn't catch async errors, that you need `node-fetch`/`dotenv`/`nodemon`/`ts-node`, and that `require` can't load ESM. On Node 22–24 with Express 5, all of that is outdated. Mention the version you're describing.

---

## 7. How to Learn It

Total: **~37.5 hours** (matches the [syllabus](./01-fullstack-syllabus.md#5-nodejs)). Prerequisites: [02-javascript](./02-javascript.md) (promises, the microtask queue, closures) and [03-typescript](./03-typescript.md).

| Step | What to do | Time |
|------|-----------|:----:|
| **0. Self-assess** | Tick the [Topic Map](./06-nodejs-part1.md#2-topic-map). Answer the [Tricky](#tricky) questions cold and write down your misses. | 1 h |
| **1. Runtime internals** | [Part 1 §3.1–3.3](./06-nodejs-part1.md#31-architecture-v8-libuv-and-the-bindings). Run the ordering script and *predict before you run*. Run the thread-pool benchmark with sizes 4 and 8. Block the loop on purpose and watch `monitorEventLoopDelay`. | 5 h |
| **2. Streams, concurrency, context** | [Part 1 §3.4–3.7](./06-nodejs-part1.md#34-buffers--streams). Reproduce the bad-vs-good backpressure memory numbers; build the CSV pipeline; build the worker pool and measure loop delay with and without it. | 5 h |
| **3. Frameworks & errors** | [Part 2 §3.8–3.13](./06-nodejs-part2.md#38-express-5-how-it-works-inside). Build the notes API in Express 5, then port it to Fastify and NestJS. Write down three behaviors that differ (validation, error shape, DI). | 5 h |
| **4. Auth & rate limiting** | [Part 2 §3.14–3.15](./06-nodejs-part2.md#314-authentication--authorization) + the OWASP Password Storage and Session cheat sheets. Implement refresh rotation with reuse detection; attack it by replaying an old token. | 5 h |
| **5. Uploads & real-time** | [Part 2 §3.16–3.17](./06-nodejs-part2.md#316-file-uploads). Stream an upload to S3-compatible storage with limits; run two chat nodes behind Redis pub/sub. | 3.5 h |
| **6. Redis caching & queues** | [Part 3 §3.18–3.19](./06-nodejs-part3.md#318-caching-with-redis). Reproduce the stampede (100 callers → 1 load); make a job fail twice and succeed on attempt 3. | 3.5 h |
| **7. Production operations** | [Part 3 §3.20–3.22](./06-nodejs-part3.md#320-structured-logging-with-pino). Add logs, traces, metrics and health checks; run the service in Docker and test `docker stop` (check the exit code). | 3 h |
| **8. Security, testing, profiling** | [Part 3 §3.23–3.25](./06-nodejs-part3.md#323-security). Run the SSRF and ReDoS demos; write the Testcontainers suite; find the planted leak with a heap diff. | 3.5 h |
| **9. Interview questions** | Answer every [question](#9-interview-questions) out loud in ≤ 2 minutes, then compare with the model answer. | 2 h |
| **10. Revise** | [Quick Revision Summary](#11-quick-revision-summary) at +1 day, +1 week and the day before. | 1 h |

```mermaid
flowchart LR
    A[Self-assess<br/>1 h] --> B[Runtime internals<br/>5 h] --> C[Streams & concurrency<br/>5 h] --> D[Frameworks & errors<br/>5 h]
    D --> E[Auth & rate limits<br/>5 h] --> F[Uploads & real-time<br/>3.5 h] --> G[Cache & queues<br/>3.5 h]
    G --> H[Operations<br/>3 h] --> I[Security, tests, profiling<br/>3.5 h] --> J[Interview Qs<br/>2 h] --> K[Revise<br/>1 h]
```

> 💡 Interview Tip: Steps 1 and 7 decide senior interviews. Everyone can build CRUD. Few candidates can explain *why* p99 latency spiked (loop blocked, thread pool saturated, connection pool exhausted, GC) or what happens between SIGTERM and exit. Get those two stories fluent, with numbers you measured yourself.

---

## 8. Hands-on Practice

| # | Exercise | Level | Acceptance criteria |
|---|----------|:-----:|---------------------|
| 1 | **Event-loop predictor** — write 5 ordering puzzles (top-level ESM, top-level CJS, inside an I/O callback, inside a timer, with `await`) | 🟢 Easy | You write the predicted output *before* running each one, then explain every miss in terms of phases, the tick queue and the microtask queue. At least one puzzle shows the ESM vs CJS difference for `nextTick` vs promises. |
| 2 | **Streaming CSV report** — 2 GB CSV → parse → filter → gzip → file | 🟢 Easy | Uses `stream/promises` `pipeline` with async generators; peak RSS stays roughly flat as you go from 200 MB to 2 GB input (log `process.memoryUsage().rss` every second); an error in any stage rejects the pipeline and deletes the partial output file. |
| 3 | **Same API, three frameworks** — notes CRUD in Express 5, Fastify 5 and NestJS 12 | 🟡 Medium | Identical routes, status codes and RFC 9457 problem+json errors; one shared Supertest suite runs against all three; you document 3 behavior differences you hit (e.g. Ajv stripping extra properties, Nest pipes, Express async errors). |
| 4 | **Auth service** — login, access tokens (EdDSA), rotating refresh tokens in Redis, logout | 🟡 Medium | Passwords hashed with scrypt or argon2id; unknown emails take the same time as wrong passwords (measured); replaying a used refresh token revokes the whole family (test proves it); refresh cookie is `HttpOnly`, `Secure`, `SameSite`, path-scoped; access tokens expire in ≤ 15 min. |
| 5 | **Distributed rate limiter** — token bucket in Redis Lua, applied per user and per IP | 🟡 Medium | Atomic (one script call per request); `RateLimit`/`Retry-After` headers set; a load test with two app instances shows the limit is global, not per instance; you document and test fail-open vs fail-closed when Redis is down. |
| 6 | **Upload pipeline** — multipart upload streamed to S3-compatible storage | 🟡 Medium | Never buffers the whole file (memory flat for a 1 GB upload); size limit returns 413 and aborts the S3 upload; content type checked by magic bytes, not the header; a client disconnect mid-upload leaves no orphaned multipart upload. |
| 7 | **Cache + queue** — cache-aside on a slow endpoint and a welcome-email queue | 🟡 Medium | 100 concurrent requests for a cold key cause 1 database load across 2 instances; Redis down degrades to direct DB reads with no extra latency; the email job is idempotent (same `jobId` twice → one email) and permanent failures don't retry. |
| 8 | **Observable service** — Pino + OpenTelemetry + Prometheus + health checks | 🔴 Hard | Every log line inside a request carries `requestId`; traces show `GET /v1/notes/:id` with Express and `pg` child spans in Jaeger; `/metrics` labels use route templates (a failed and a successful request to the same route share a label); `/readyz` fails when Postgres is down and `/livez` doesn't. |
| 9 | **Zero-downtime shutdown** — run 2 containers behind a proxy and redeploy under load | 🔴 Hard | A load test (e.g. `autocannon` or k6) during a rolling restart shows **0 failed requests**; logs show drain → server closed → hooks closed; the container exits with code 0 (not 137) within the grace period; an in-flight BullMQ job finishes before exit. |
| 10 | **Production incident drill** — a teammate plants one of: a sync CPU loop, an unbounded `Map`, a pool-size bottleneck or a ReDoS-prone regex | 🔴 Hard | You find it with tools only (event-loop delay metric, `--cpu-prof` flame graph, heap snapshot diff, pool metrics), write a 1-page postmortem (symptom → evidence → root cause → fix → prevention), and add a regression test or alert. |

---

## 9. Interview Questions

### Basic

#### Q1. Is Node.js single-threaded?

**Model answer.** Your JavaScript runs on one thread: one V8 isolate, one call stack, one event loop. The process isn't single-threaded, though:

- **libuv's thread pool** (4 threads by default) runs work that has no good async OS API: file system calls, `dns.lookup`, and CPU-heavy crypto and zlib calls such as `pbkdf2`, `scrypt` and async compression.
- **Network I/O** uses the OS's async mechanisms (epoll, kqueue, IOCP), not the pool.
- **V8** has its own background threads for GC and compilation.
- **`worker_threads`** give you more JavaScript threads, each with its own isolate and event loop.

So "single-threaded" is true of your code's execution model, which is why one blocking loop stalls every request.

**Follow-ups:** What happens to other requests while one handler runs a 2-second loop? Which APIs use the thread pool?

**Great answer includes:** The JS thread vs the libuv pool vs OS async I/O; the consequence (a blocked loop blocks everyone); workers as the escape hatch for CPU-bound work.

#### Q2. Walk me through the event loop phases. When does `setImmediate` run before `setTimeout(fn, 0)`?

**Model answer.** Each loop iteration runs these phases in order:

1. **timers** — expired `setTimeout`/`setInterval` callbacks;
2. **pending callbacks** — some deferred system callbacks;
3. **poll** — wait for and run I/O callbacks;
4. **check** — `setImmediate` callbacks;
5. **close callbacks** — such as `'close'` events.

Between every callback, Node drains `process.nextTick` callbacks and then promise microtasks.

**Inside an I/O callback**, `setImmediate` always runs first, because the check phase comes right after poll and the timers phase comes only in the next iteration. **At the top level of the main module**, the order isn't deterministic: it depends on whether the 1 ms timer threshold has passed when the loop starts.

**Follow-ups:** What changed in libuv 1.45 (Node 20)? Where do microtasks run?

**Great answer includes:** Phase order with check right after poll; "inside I/O, immediate wins; at top level, it varies"; microtask and tick draining between callbacks; the libuv 1.45 change (timers run only after poll) — [Part 1 §3.2](./06-nodejs-part1.md#32-the-event-loop-in-depth).

#### Q3. `process.nextTick` vs `queueMicrotask`/promises — what's the difference, and why does it differ between ESM and CommonJS?

**Model answer.** Both run before the event loop continues. After each callback, Node drains the **nextTick queue** first, then V8's **microtask queue**, and it repeats until both are empty. So a nextTick scheduled from a callback normally runs before promise reactions.

The surprise is the **top level of an ES module**. Module evaluation is itself driven by promises, so when the synchronous code finishes, Node is *already draining microtasks*. Promise callbacks run first, and nextTicks after them. In CommonJS, the top level is a plain function call, so it's `nextTick` and then promises. Measured on Node 24: CJS gives `sync > nextTick > promise`, and ESM gives `sync > promise > … > nextTick`.

Recursive `nextTick` calls can starve I/O, which is why the docs recommend `queueMicrotask` for most new code.

**Follow-ups:** Can promises starve the loop too? (Yes — any queue that refills itself forever.) When is `nextTick` still useful? (Emitting an event after the constructor returns, so listeners can be attached.)

**Great answer includes:** The ordering rule; the ESM/CJS difference *with the reason*; starvation; a legitimate `nextTick` use.

#### Q4. Which operations use the libuv thread pool, and when would you change `UV_THREADPOOL_SIZE`?

**Model answer.** The thread pool runs:

- asynchronous `fs` calls (except `fs.watch`);
- `dns.lookup` (which is also what `http.get('host')` uses by default);
- async `crypto` work (`pbkdf2`, `scrypt`, `randomBytes`, `generateKeyPair`);
- async `zlib`.

TCP and UDP sockets don't use it.

The default is 4 threads. With 8 concurrent `pbkdf2` calls on 4 threads, I measured two waves (~0.7 s and ~1.4 s). With 8 threads, all of them finished at ~0.8 s. I'd raise it for services that hash passwords or touch the disk heavily, sized to the number of cores, and I'd set it in the environment at launch (Dockerfile `ENV`, systemd unit), not in code, because the pool is created on first use.

**Follow-ups:** Why might HTTP calls to many hostnames get slow under load? (`dns.lookup` saturating the pool.) What's the maximum? (1024.)

**Great answer includes:** The specific API list; "network sockets don't use it"; the `dns.lookup` gotcha; setting it at launch; measuring rather than guessing.

#### Q5. What is backpressure, and how do you handle it in Node streams?

**Model answer.** Backpressure happens when a producer is faster than a consumer. A writable stream buffers up to `highWaterMark` (16 KiB by default, 64 KiB for `fs` streams). `write()` returns `false` when the buffer is full, and the producer should stop until `'drain'`.

Code that ignores the return value keeps buffering in memory. In my test, copying a file while ignoring backpressure peaked at ~565 MB of RSS, and the correct version stayed around 63 MB.

In practice, I use `pipeline()` from `node:stream/promises`. It respects backpressure, propagates errors from any stage, and destroys every stream on failure. `.pipe()` respects backpressure too, but it doesn't forward errors or clean up, so a failure can leak file descriptors.

**Follow-ups:** How do async generators fit into `pipeline`? What does object mode change? (`highWaterMark` counts objects: 16.)

**Great answer includes:** `write()` returning `false` and `'drain'`; `pipeline` over `.pipe`; error propagation and cleanup; a memory number.

#### Q6. How does Express middleware work, and what changed in Express 5?

**Model answer.** Express keeps an ordered stack of layers. Each request walks the stack. A layer runs if its path and method match, and it either responds or calls `next()`. Calling `next(err)` skips to the next **error middleware**, the one with four parameters `(err, req, res, next)`. Routers are just nested stacks mounted on a path prefix.

Express 5 changes I'd mention:

- A **rejected promise from an async handler is forwarded to the error handler** automatically, so `express-async-errors` isn't needed.
- Path syntax moved to `path-to-regexp` 8: wildcards must be named (`/*splat`), optional segments use braces (`{/:id}`), and an old-style `/old/*` route throws at startup.
- `req.query` is a getter, so middleware can't reassign it.
- `req.body` is `undefined` (not `{}`) when no body parser ran.
- Invalid status codes throw (`res.status(1000)` is a `RangeError`).
- Deprecated methods such as `res.send(status, body)` were removed.

**Follow-ups:** Where does the error handler go? (Last.) What does Express do with an error thrown inside a `setTimeout` in a handler? (Nothing — it's outside the promise chain, so it's an uncaught exception.)

**Great answer includes:** The layer/stack model; `next(err)` and 4-arity error handlers; concrete Express 5 changes; the limit of async error forwarding.

#### Q7. Operational vs programmer errors — how do you handle each, and what does Node do with an unhandled rejection?

**Model answer.** **Operational errors** are expected failures in correct code: a timeout, a 404 from a dependency, invalid input, a refused connection. You handle them by retrying, falling back or returning a 4xx or 5xx.

**Programmer errors** are bugs: reading a property of `undefined`, a wrong argument type. The process state may be inconsistent, so you log them, return a 500 and, for truly uncaught ones, **crash and let the supervisor restart the process**.

Since Node 15, an unhandled rejection is treated like an uncaught exception (`--unhandled-rejections=throw` is the default). The process exits with code 1. A `process.on('unhandledRejection')` handler should log and start a graceful shutdown, not swallow the error.

**Follow-ups:** Why not just keep running after `uncaughtException`? How do you return safe error messages? (`expose` flag; problem+json.)

**Great answer includes:** The two categories with examples; crash-and-restart for unknown state; the Node 15 default; logging plus graceful exit in the handlers.

#### Q8. Sessions vs JWTs — which would you use?

**Model answer.** **Server-side sessions** use an opaque random ID in an `HttpOnly` cookie, with the session data in Redis or a database. They're easy to revoke instantly, the cookie is small, and the server stays in control. The cost is a lookup per request.

**JWTs** are signed, self-contained claims. Any service can verify them locally with a public key, with no lookup. But you can't revoke one before it expires without adding state back (a denylist, or a session version check), and the payload is readable by anyone.

For a first-party web app, I default to sessions, or a short-lived access JWT plus a rotating refresh token in an `HttpOnly` cookie. JWTs earn their place when several services or third parties verify tokens independently.

**Follow-ups:** Where do you store tokens in a browser? (Not `localStorage` for long-lived tokens — XSS can read it.) How do you revoke a JWT?

**Great answer includes:** Revocation as the core trade-off; storage and XSS; short access + rotating refresh; "JWT is a format, not a session strategy".

#### Q9. CommonJS vs ES modules in Node — what are the practical differences today?

**Model answer.**

- **Loading:** ESM is loaded asynchronously in phases (parse, link, evaluate) and supports top-level `await`. CJS loads synchronously when `require` runs.
- **Bindings:** ESM imports are live bindings; CJS gives you a copy of `module.exports` at the time you read it.
- **Module-scope variables:** ESM has no `__dirname`/`require`; use `import.meta.dirname`/`import.meta.filename` (Node 20.11+) and `createRequire`.
- **File type:** set by `"type"` in `package.json` or by the `.mjs`/`.cjs` extension.

The big change is **`require(esm)`**: it's unflagged since 22.12 and 20.19, so CJS code can `require` an ES module as long as it has no top-level `await`. That's why libraries like NestJS 12 can ship ESM-only.

**Follow-ups:** What's dual-package hazard? Why does top-level `await` block `require(esm)`?

**Great answer includes:** The loading model differences; `import.meta` replacements; `require(esm)` and its version numbers; the TLA limitation.

### Intermediate

#### Q10. cluster vs `worker_threads` vs `child_process` — when do you use each?

**Model answer.**

- **`cluster`** forks whole processes that share a listening port. It scales an HTTP server across cores, and each worker has its own memory and event loop. In containers I usually skip it and run one process per container, letting the orchestrator scale out. PM2's cluster mode is the same idea for VMs.
- **`worker_threads`** run JavaScript on more threads inside one process. They can transfer `ArrayBuffer`s or share them with `SharedArrayBuffer`. Use them for CPU-bound work (image processing, parsing, hashing) behind a **pool**, because each worker costs a V8 isolate (tens of MB, plus startup time). In my test, a CPU job took 2.85 s with the loop stalled throughout on the main thread, and 1.2 s with a maximum loop delay of 31 ms on a pool of 4.
- **`child_process`** runs another program (ffmpeg, a Python script) or isolates untrusted or crash-prone work in a separate process.

**Follow-ups:** Why not create a worker per request? How do you handle a worker crashing mid-task?

**Great answer includes:** The process vs thread vs external-program distinction; pools; memory cost; "one process per container" as the default in Kubernetes/ECS.

#### Q11. A Node service's latency suddenly spikes. How do you tell whether the event loop is blocked?

**Model answer.** Measure the loop directly. `perf_hooks.monitorEventLoopDelay()` exposes p50/p99/max delay (prom-client's default metrics already include it). A healthy service has a p99 of a few milliseconds; hundreds of milliseconds means something synchronous is hogging the thread.

To find the culprit, take a CPU profile (`node --cpu-prof`, or attach `--inspect` and record) and look at the widest frames in the flame graph. The usual suspects are:

- big `JSON.parse`/`JSON.stringify` calls;
- sync `fs` or `crypto`;
- a catastrophic regex;
- huge array sorts;
- template rendering.

If loop delay is *normal* but latency is high, the bottleneck is elsewhere: thread pool queueing, a database pool exhausted (requests waiting for a connection), downstream latency, or GC pauses (check GC metrics or `--trace-gc`).

**Follow-ups:** How do you fix a legitimately CPU-heavy task? (Worker pool, time slicing, or move it to a queue worker.) Why does time slicing cost throughput? (Measured: 2–4× slower wall time.)

**Great answer includes:** A metric first, then a profile; the list of suspects; "loop is fine" leads to pool/downstream/GC; fixes with trade-offs.

#### Q12. Design refresh token rotation with reuse detection.

**Model answer.**

1. On login, issue a short-lived access token (≤ 15 min) and an opaque random refresh token. Store only its **hash** server-side, along with a **family ID** (one family per login session).
2. On refresh, **atomically consume** the presented token (a Redis Lua script or a DB transaction) and issue a new pair in the same family.
3. If a token that was **already used** is presented, someone has a copy. Revoke the entire family and force a new login.

Deliver the refresh token in an `HttpOnly`, `Secure`, `SameSite=Strict` (or `Lax`) cookie scoped to the refresh path, and check `Origin` on the refresh endpoint. Allow a small grace window, or make clients serialize refreshes, so two tabs refreshing at once don't trigger a false reuse alarm.

**Follow-ups:** Why hash refresh tokens at rest? How does logout work? (Delete the family.) Why must consumption be atomic?

**Great answer includes:** Families; atomic consume; revoke-the-family on reuse; hashed storage; cookie attributes; the concurrent-refresh race — [Part 2 §3.14](./06-nodejs-part2.md#314-authentication--authorization).

#### Q13. How should a Node service store passwords?

**Model answer.** Use a slow, memory-hard, salted hash: **argon2id** first, **scrypt** as the built-in fallback (`crypto.scrypt`), and bcrypt where it's already in use. Store the parameters with the hash (a PHC string), so you can raise costs later and **rehash on the next successful login**.

Node 24 added `crypto.argon2` (24.7), so you no longer need a native addon for it; check its stability index in your version's docs. Use the async APIs, because the hashing runs on the thread pool.

Two more details:

- Compare with `timingSafeEqual`.
- When the email doesn't exist, still verify against a **dummy hash**, so response timing doesn't reveal which emails are registered.

Rate-limit login per account and per IP.

**Follow-ups:** Why not SHA-256 with a salt? (Too fast — GPUs try billions per second.) What's a pepper?

**Great answer includes:** argon2id/scrypt/bcrypt ranking; stored parameters and rehash; async on the pool; dummy hash for enumeration; rate limiting.

#### Q14. Implement rate limiting across multiple instances.

**Model answer.** In-process counters don't work: each instance only sees its own share of the traffic. I keep the state in **Redis** and make each check **atomic** with a Lua script (read, compute, write in one step), because a GET-then-SET from Node races under concurrency.

Algorithms:

- **Fixed window** — cheap, but allows bursts of up to 2× the limit at window edges.
- **Sliding log** — a sorted set of timestamps; exact, but memory grows with the limit.
- **Token bucket** — two fields; allows controlled bursts with a steady refill. It's my default.

Return `429` with `Retry-After` (and `RateLimit-*` headers), key by user ID when authenticated and by IP otherwise (with `trust proxy` set correctly, or every request appears to come from the load balancer). Decide **fail-open vs fail-closed** per route: open for general API traffic, closed for login.

**Follow-ups:** Why is `trust proxy` critical? Where else could you rate-limit? (CDN/WAF, API gateway — layered.)

**Great answer includes:** Shared state + atomicity; algorithm trade-offs; headers; client identity behind proxies; fail-open/closed decision.

#### Q15. How would you handle large file uploads?

**Model answer.** Best option: **don't proxy the bytes at all**. The API issues a **pre-signed S3 URL** (or a multipart upload for big files), the browser uploads directly, and the API is notified (S3 event or a confirm call) to validate and record the file ([11](./11-deployment-aws-s3.md)).

When the bytes must pass through Node, **stream** them:

1. Parse multipart with busboy.
2. Pipe into `@aws-sdk/lib-storage`'s `Upload`. Never buffer the whole file in memory or write it to disk.
3. Enforce limits: file size (and return 413), number of files, field sizes.
4. Check the content type from **magic bytes**, not from the client's header.
5. Generate the object key yourself; never use the client's filename as a path.
6. On error or client abort, abort the upload so no multipart parts are left behind (and add a lifecycle rule to clean up incomplete uploads).

**Follow-ups:** How do you scan uploads for malware? (Async job after upload, quarantine bucket.) How do you resume an interrupted upload?

**Great answer includes:** Pre-signed URLs as the default; streaming with limits; magic bytes; server-generated keys; cleanup on abort.

#### Q16. SSE vs WebSockets — and how do you scale either across instances?

**Model answer.** **Server-Sent Events** are one-way (server → client) over plain HTTP. They auto-reconnect with `Last-Event-ID`, work through most proxies, and are perfect for notifications, feeds and progress updates. **WebSockets** are full-duplex over an upgraded connection. Use them for chat, collaboration and games, where clients send frequently.

Scaling problems are the same for both: a client is connected to *one* instance, but events are produced on any instance. So:

- Publish events to a **broker** (Redis pub/sub, Redis streams, NATS) that every instance subscribes to.
- Each instance forwards events to its local connections.
- Track presence in Redis.

Also plan for:

- **heartbeats** (proxies kill idle connections);
- **backpressure** (`ws` `bufferedAmount` — drop or disconnect slow clients);
- **auth at upgrade time** (browsers can't set headers on WebSockets, so use a short-lived ticket);
- **load balancer idle timeouts**;
- **graceful drain** on deploy (close with a code and let clients reconnect elsewhere).

**Follow-ups:** Does SSE work over HTTP/2? (Yes, and HTTP/2 lifts the 6-connections-per-origin limit of HTTP/1.1.) Do you need sticky sessions? (For Socket.IO's polling fallback, yes; for plain WebSockets, no.)

**Great answer includes:** Direction and protocol differences; a broker for fan-out; heartbeats; slow consumers; upgrade-time auth.

#### Q17. Explain cache-aside and how you prevent a cache stampede.

**Model answer.** **Cache-aside:** read from the cache; on a miss, load from the database, write to the cache with a TTL, and return. On writes, update the database and then **delete** the key (deleting is safer than updating it, because two concurrent writers can leave a stale value).

A **stampede** is many requests missing the same hot key at once and all hitting the database. Defenses, in layers:

1. **Single-flight** within a process: share one in-flight promise per key.
2. A short **Redis lock** (`SET NX PX`) so one instance loads while the others briefly poll the cache.
3. **TTL jitter**, so keys don't expire together.
4. Optionally, **stale-while-revalidate** or early refresh.

Also cache "not found" briefly (negative caching), and make sure **Redis being down degrades to a miss**, not an error or a slow path. Measured on my implementation: 100 concurrent callers across two instances caused one database load.

**Follow-ups:** What if the lock holder dies? (TTL on the lock; pollers give up and load.) How do you cache per-user data safely?

**Great answer includes:** Delete-on-write; single-flight + lock + jitter; negative caching; Redis-down behavior — [Part 3 §3.18](./06-nodejs-part3.md#318-caching-with-redis).

#### Q18. How do you make background jobs reliable?

**Model answer.** Queues like BullMQ are **at-least-once**: a job can run twice (a worker crashes after doing the work but before acknowledging it, or its lock expires). So jobs must be **idempotent**:

- a deterministic `jobId` (deduplicates enqueues);
- an idempotency key passed to the downstream system (the email provider, Stripe);
- or a "done" record checked in the same transaction as the side effect.

Configure attempts with **exponential backoff and jitter**, and throw `UnrecoverableError` for permanent failures (an invalid address) so they don't retry. Keep failed jobs for inspection, alert on queue depth and age, set concurrency per worker based on what downstream can take, and call `worker.close()` on shutdown so the active job finishes.

**Follow-ups:** How do you enqueue reliably together with a DB write? (Transactional outbox.) What does a job scheduler replace? (Cron on a single box.)

**Great answer includes:** At-least-once → idempotency; backoff; permanent vs transient errors; observability of the queue; outbox pattern.

#### Q19. How do you get a request ID onto every log line without passing it everywhere?

**Model answer.** Use **`AsyncLocalStorage`**. A middleware creates (or accepts, after validating) a request ID, then calls `als.run({ requestId }, next)`. Every async continuation from that request — promises, timers, database callbacks — sees the same store. The logger reads it in a Pino **`mixin`**, so every line includes `requestId` (and `userId` once known). Return the ID in a response header (`X-Request-Id`) so support can ask users for it.

Use structured JSON logs with Pino (it's fast because it does minimal work on the main thread), redact secrets (authorization headers, cookies, `Set-Cookie`), use a compact `res` serializer, and link logs to traces by including the OpenTelemetry trace ID.

**Follow-ups:** What breaks ALS propagation? (Some callback-based libraries with custom pooling; `AsyncResource` fixes it.) Why not `console.log`? (Synchronous to files and TTYs, unstructured.)

**Great answer includes:** ALS `run` in middleware; logger mixin; response header; redaction; trace correlation.

#### Q20. What should a Node service do on SIGTERM?

**Model answer.**

1. **Fail readiness** immediately (`/readyz` returns 503) so the load balancer stops routing new traffic. Keep serving for a short **drain delay**, because LB deregistration isn't instant.
2. **`server.close()`** to stop accepting connections, and set `Connection: close` on responses, because in-flight keep-alive connections otherwise keep serving new requests.
3. Wait for in-flight requests, then **close resources in order**: queue workers (finish the active job), then database and Redis pools, then flush telemetry.
4. Exit by setting `process.exitCode`, with an **unref'd hard timeout** that forces `exit(1)` if something hangs.

All of this must fit in the orchestrator's **grace period** (Kubernetes and ECS default to 30 s; Docker 10 s). Run `node` directly as PID 1 (exec-form `CMD`), or behind `--init`, so the signal actually arrives.

**Follow-ups:** Why not just `process.exit()` on SIGTERM? What's the difference between liveness and readiness here?

**Great answer includes:** Readiness first; drain delay; keep-alive handling; ordered resource close; hard timeout; grace period and PID 1 — [Part 3 §3.22](./06-nodejs-part3.md#322-graceful-shutdown).

### Advanced

#### Q21. You add OpenTelemetry to an ESM Express app and only see generic `GET` spans. Why?

**Model answer.** Auto-instrumentation works by patching modules **when they're loaded**. In CommonJS, that's done by hooking `require`. ES modules don't go through `require`, so OTel needs a **loader hook** (`import-in-the-middle`), registered with `module.register('@opentelemetry/instrumentation/hook.mjs', import.meta.url)` in a file loaded via `--import` **before** the app's imports.

Without it, the core `http` module still gets instrumented (it's patched differently), so you see `GET` server spans, but Express, and possibly `pg`, aren't patched. You get no route names and no child spans. I verified this: with only the `register` entry point there were no Express spans; with the hook, spans were named `GET /users/:id` with `http.route`.

Also:

- Call `sdk.shutdown()` on exit, or batched spans are lost.
- Use `SimpleSpanProcessor` only for debugging.
- Sample at the head, or the collector's tail.

**Follow-ups:** Head vs tail sampling? How do you propagate context to a queue job? (Inject the `traceparent` into the job data.)

**Great answer includes:** Load-time patching; ESM loader hook and `--import`; flush on shutdown; sampling; context propagation across async boundaries.

#### Q22. Memory grows steadily in production until the container is OOM-killed. How do you investigate?

**Model answer.**

1. **Confirm it's a leak.** Chart heap used after GC (not RSS alone) over hours. Sawtooth with a rising floor means a leak. RSS growing while the heap stays flat points to native memory (Buffers, native addons) or fragmentation.
2. **Capture snapshots.** Take two or three heap snapshots some time apart: `--heapsnapshot-signal=SIGUSR2`, `v8.writeHeapSnapshot()` behind an admin endpoint, or `--inspect` in staging. Snapshots pause the process and need about 2× the heap in memory, so take them from an instance removed from the LB.
3. **Compare.** Use the comparison view: which constructor's count grows? Follow its **retainers** to the root. My planted leak showed +20,000 `RequestTrace` objects held by a module-level `Map`.

Typical causes:

- unbounded caches or maps;
- listeners added per request and never removed;
- closures capturing large objects;
- timers never cleared;
- ALS stores retained by long-lived promises.

Fix with bounded LRU caches (size + TTL), `once`/`AbortSignal` for listeners, and a regression test that checks heap after N requests.

**Follow-ups:** What does `--max-old-space-size` do, and how should it relate to the container limit? What's the difference between shallow and retained size?

**Great answer includes:** Heap-after-GC vs RSS; snapshot diff and retainers; snapshot cost; common causes; prevention.

#### Q23. Express, Fastify or NestJS for a new service — how do you choose?

**Model answer.**

- **Express 5** — the biggest ecosystem and the least structure; fine for small services if the team adds conventions (validation, error handling, layout).
- **Fastify** — faster routing and serialization, schema-based validation and response serialization (Ajv), an encapsulated plugin system, and first-class TypeScript type providers. Watch Ajv's defaults: it removes additional properties and coerces types.
- **NestJS** — an opinionated architecture on top of Express or Fastify: modules, DI, guards, pipes, interceptors. It pays off with large teams and many modules. The cost is decorators, more indirection and a learning curve. Version 12 is ESM-only and needs Node 20.19+/22.12+.

I choose based on team size and the need for consistency, not benchmarks: the framework is rarely the bottleneck, the database is.

**Follow-ups:** How does Fastify's encapsulation differ from Express routers? What do Nest request-scoped providers cost? (They're created per request and bubble up the dependency chain.)

**Great answer includes:** Concrete trade-offs per framework; Fastify defaults; Nest's costs; "the database is the bottleneck".

#### Q24. Your service fetches user-supplied URLs (webhooks, link previews). How do you prevent SSRF?

**Model answer.** Validate the URL first:

- allow only `https:` (and maybe `http:`);
- reject credentials in the URL;
- optionally allowlist ports.

The core defense is checking the **resolved IP address at connect time**, not the hostname. Hostnames like `localhost`, decimal IPs (`2130706433`), IPv6 forms and DNS rebinding all bypass string checks. With undici, pass a custom `connect.lookup` that resolves the name, rejects any address in a `BlockList` (loopback, RFC 1918 private ranges, link-local including **169.254.169.254** cloud metadata, CGNAT, IPv6 ULA and link-local), and then connects to that exact IP, so there's no second resolution an attacker can change.

Also:

- Re-validate every **redirect** (or disable redirects).
- Set timeouts and a response size limit.
- Run the fetcher in an isolated network segment with egress rules — defense in depth.
- On AWS, require IMDSv2.

**Follow-ups:** What's DNS rebinding? Why isn't a hostname denylist enough? Why was a `::ffff:0:0/96` rule a bug in my implementation? (Node's `BlockList` matches IPv4 addresses against IPv4-mapped rules, so it blocked everything.)

**Great answer includes:** Connect-time IP check; the bypass list; redirects; metadata endpoint; network-level egress control — [Part 3 §3.23](./06-nodejs-part3.md#323-security).

#### Q25. Explain prototype pollution and ReDoS. Why are they Node-specific concerns?

**Model answer.** **Prototype pollution:** a deep merge or path-setter copies attacker JSON such as `{"__proto__": {"isAdmin": true}}` onto `Object.prototype`, so *every* object in the process gains `isAdmin`. Since the process is long-lived and shared across users, one request can affect all later requests. Defenses:

- validate input with strict schemas (Zod `.strict()`);
- block `__proto__`, `constructor` and `prototype` keys in merges;
- use `Object.create(null)` or `Map` for dictionaries;
- `--disable-proto=delete` as hardening.

**ReDoS:** a regex with nested or overlapping quantifiers (`/^(a+)+$/`) backtracks exponentially on near-matching input. On one thread, that blocks *every* request. Measured: 26 characters took ~600 ms, and each 2 extra characters multiplied the time by 4–5. Defenses:

- rewrite the pattern without ambiguity;
- limit input length before matching;
- use a linear-time engine (`re2`) for user-supplied patterns;
- lint for unsafe regexes.

**Follow-ups:** Where do these show up in real CVEs? (Merge utilities, query-string parsers, validation libraries.) Does V8 have any protection? (V8 has an experimental non-backtracking engine behind a flag — check the current status before relying on it.)

**Great answer includes:** The mechanism of each; why the shared long-lived process makes it worse; multiple layered defenses; a measured sense of the exponential growth.

#### Q26. Liveness vs readiness checks — what goes in each?

**Model answer.** **Liveness** answers "is this process hopelessly broken and in need of a restart?" It should be cheap and check *only the process itself*: the event loop responds. If liveness checks the database, a database outage makes the orchestrator restart every healthy pod, which turns a dependency incident into a full outage plus a thundering herd on recovery.

**Readiness** answers "should I receive traffic right now?" It checks critical dependencies with short timeouts, and it **fails during shutdown** so the load balancer drains you. A **startup probe** covers slow boots.

Keep the checks unauthenticated but internal, cache dependency results briefly under high probe frequency, and exclude them from access logs and metrics noise.

**Follow-ups:** Should readiness fail if Redis (used only for caching) is down? (Probably not — the service still works degraded. Decide per dependency.)

**Great answer includes:** What each probe means to the orchestrator; no dependencies in liveness; readiness during shutdown; degraded vs down dependencies.

#### Q27. How do you test a Node API with confidence and keep tests fast?

**Model answer.**

- **Unit tests** cover pure domain logic.
- **Most of the value is in integration tests** that hit the HTTP layer with **Supertest** (no real port needed): they exercise routing, validation, auth, error shapes and status codes.
- For the database, test against **real Postgres in Testcontainers**, not mocks or SQLite: constraints, isolation behavior, JSON operators and query plans differ. Start one container per suite, run migrations once, and isolate tests with transactions or truncation.
- Inject dependencies (`createApp({ repo, authenticate })`) so you can swap fakes in where speed matters.

Use the built-in `node:test` runner (`node --test "test/**/*.test.ts"` with the glob quoted; a bare directory argument doesn't work) or Vitest. Cover contract tests between services and a few end-to-end smoke tests after deploy.

**Follow-ups:** How do you test code that depends on time? (Mock timers / inject a clock.) How do you keep the Testcontainers suite fast in CI? (Reuse the container across files, cache images.)

**Great answer includes:** The integration-heavy shape for APIs; real DB via containers; DI for testability; test isolation strategy — [Part 3 §3.24](./06-nodejs-part3.md#324-testing-node-apis).

#### Q28. Design a chat backend in Node for 100k concurrent WebSocket connections.

**Model answer.**

- **Connections:** at ~10–20k sockets per instance (memory and CPU bound — measure), that's around 10 instances behind an L4/L7 load balancer that supports upgrades, with idle timeouts above the heartbeat interval.
- **Auth:** at upgrade time, with a one-time short-lived ticket from the REST API (stored in Redis, consumed with `GETDEL`).
- **Fan-out:** each instance subscribes to Redis pub/sub channels for the rooms its users joined, and a message is published once and delivered by every instance with members in that room. For durability and history, write messages to a database (or Redis streams/Kafka) first, and give clients a cursor to catch up after reconnecting — pub/sub is fire-and-forget.
- **Backpressure:** check `bufferedAmount` and disconnect slow clients.
- **Rate limits** per user.
- **Presence** in Redis with TTLs refreshed by heartbeats.
- **Deploys:** drain by closing sockets gradually so reconnects spread out (jittered client backoff).

**Follow-ups:** Pub/sub vs streams? How do you guarantee ordering within a room? (Single partition per room, or sequence numbers from the DB.)

**Great answer includes:** Capacity math with "measure"; upgrade auth; broker fan-out; durability separate from delivery; slow consumers; reconnect storms. Full treatment: [09](./09-system-design.md).

#### Q29. p99 latency doubles under load, but CPU is only at 40%. What could it be?

**Model answer.** Low CPU with high latency means requests are **waiting**, not computing. Check the queues in order:

1. **Event loop delay** — a single slow synchronous chunk can stall the loop even at 40% average CPU.
2. **Thread pool queueing** — 4 threads shared by `bcrypt`/`scrypt`, `fs` and `dns.lookup`. Password hashing under load is the classic case.
3. **Connection pool exhaustion** — `pg` `max: 10` with slow queries means requests wait for a connection. Watch the pool's waiting count.
4. **Downstream latency** — a dependency without timeouts, or HTTP clients without keep-alive (new TLS handshakes every call).
5. **GC pauses** — large heaps or allocation-heavy paths.
6. **Container CPU throttling** — CFS quotas; average CPU looks fine while bursts are throttled.

I'd add metrics for each (loop delay, pool waiting, per-dependency latency, GC) and fix the specific queue rather than adding instances blindly.

**Follow-ups:** Why can adding instances make it worse? (More connections to an already-saturated database.) How does Little's Law help? (Concurrency = throughput × latency → size pools.)

**Great answer includes:** "Waiting, not computing"; the six queues; metrics before fixes; database-side effects of scaling out.

#### Q30. Is a Redis lock (`SET NX PX`) safe for protecting correctness-critical work?

**Model answer.** It's fine for **efficiency** — avoiding duplicate work, like the cache stampede lock — where an occasional double execution is harmless. It's **not safe for correctness** on its own. A process can pause (GC, CPU throttling, a network partition) past the lock's TTL, the lock expires, a second process acquires it, and both write.

Releasing with a token check (a Lua compare-and-delete) prevents deleting someone else's lock, but it doesn't stop the paused process from writing afterwards. The fix is **fencing tokens**: a monotonically increasing number issued with the lock, which the storage layer checks and rejects if stale. Alternatively, put the correctness guarantee in the database itself: unique constraints, `SELECT … FOR UPDATE`, conditional updates (`WHERE version = ?`), or a single-writer queue partition.

Redlock across several Redis nodes improves availability but doesn't remove the timing assumptions, as Kleppmann's analysis argues.

**Follow-ups:** How does `SELECT … FOR UPDATE SKIP LOCKED` give you a job queue in Postgres? ([07](./07-databases-and-apis.md))

**Great answer includes:** Efficiency vs correctness; the pause scenario; token-checked release; fencing tokens; pushing correctness into the database.

### Tricky

#### Q31. What does this ES module print?

```ts
// order.mts (ESM; Node 24 runs it directly with type stripping)
const out: string[] = [];
setTimeout(() => out.push('A'), 0);
setImmediate(() => out.push('B'));
Promise.resolve().then(() => {
  out.push('C');
  process.nextTick(() => out.push('D'));
});
process.nextTick(() => out.push('E'));
await null;
out.push('F');
setTimeout(() => console.log(out.join(' ')), 20);
```

**Model answer.** `C F E D`, followed by `A B` or `B A`. Measured on Node 24.21: 4 runs printed `C F E D A B` and 4 printed `C F E D B A`.

- The module is evaluated inside promise machinery, so after the synchronous part Node is **draining microtasks**. `C` was queued first, then the `await null` continuation, so `C` then `F` (and `C` queues tick `D`).
- With microtasks empty, Node drains the nextTick queue in FIFO order: `E` (queued during sync code), then `D`.
- `A` (timer) vs `B` (immediate) at the top level depends on whether 1 ms has elapsed when the loop starts, so the order varies.

In a `.cjs` file (without the `await`), `E` would run *before* `C`.

**Follow-ups:** What if this code ran inside an `fs.readFile` callback? (Ticks before microtasks, and `B` always before `A`.)

**Great answer includes:** ESM evaluation starts in a microtask drain; FIFO within each queue; the nondeterministic timer/immediate pair; the CJS contrast.

#### Q32. Does this crash the process?

```ts
const p = Promise.reject(new Error('boom'));
setTimeout(() => {
  p.catch((e: Error) => console.log('caught later:', e.message));
}, 0);
```

**Model answer.** **Yes.** With the default `--unhandled-rejections=throw` (Node 15+), Node checks for unhandled rejections after the microtask queue drains, which is well before the timer runs. No handler is attached at that point, so it raises the error as an uncaught exception, and the process exits with code 1 before "caught later" is printed. Verified on Node 24.21.

The fix is to attach the handler synchronously (or within the same microtask turn). Code that creates promises early and awaits them later (`const a = fetchA(); await slow(); await a;`) has the same bug if `a` rejects while `slow()` runs. Use `Promise.all` or `Promise.allSettled` instead.

**Follow-ups:** What does `rejectionHandled` mean? What changes with `--unhandled-rejections=warn`?

**Great answer includes:** Crash with exit code 1; when the check happens; the "start early, await later" real-world variant; `Promise.all`.

#### Q33. You raise `UV_THREADPOOL_SIZE` to 64 to speed up outgoing HTTP calls. Does it help?

**Model answer.** Mostly **no**. Socket I/O doesn't use the thread pool, so request/response handling isn't limited by it. The one piece that can be is **DNS**: `http`/`undici` resolve hostnames with `dns.lookup` (`getaddrinfo`), which *does* run on the pool. With many distinct hosts, slow DNS and only 4 threads, lookups queue up. Raising the pool size hides that symptom.

Better fixes:

- **keep-alive agents** and connection pooling, which avoid repeat DNS lookups and TLS handshakes;
- DNS caching;
- `dns.resolve*` (c-ares, not on the pool) where the semantics fit.

Also: 64 threads mostly cost memory and context switches, and they don't help CPU-bound pool work beyond the number of cores.

**Follow-ups:** Why does `dns.lookup` respect `/etc/hosts` and `dns.resolve` not?

**Great answer includes:** Sockets ≠ pool; `dns.lookup` as the exception; keep-alive as the real fix; cost of oversizing.

#### Q34. Does Express 5 catch every error in an async handler?

```ts
app.get('/report', async (req, res) => {
  setTimeout(() => {
    throw new Error('late failure');
  }, 10);
  const data = await buildReport(req.query);
  res.json(data);
});
```

**Model answer.** It catches errors that **reject the handler's promise**: a `throw` before or after an `await`, or a rejected `await`. That covers `buildReport` failing, which goes to the error middleware.

The `throw` inside `setTimeout` is different. It runs in a later macrotask, outside the handler's promise chain, so it's an **uncaught exception**. It crashes the process, taking every in-flight request with it, and the error middleware never sees it. The same is true for errors in event-emitter callbacks without an `'error'` listener and for callback-style APIs.

Fix: promisify (`await setTimeout(10)` from `node:timers/promises`) or wrap the callback-style APIs, so every failure flows through the promise.

**Follow-ups:** What does Express 4 do with `buildReport` rejecting? (Nothing: an unhandled rejection, and the request hangs until it times out — or the process crashes on Node 15+.)

**Great answer includes:** What Express 5 forwards and what it can't see; why; the crash blast radius; promisify everything.

#### Q35. The user clicks "log out". How do you make their JWT stop working immediately?

**Model answer.** A JWT can't be "un-signed". It stays valid until `exp` unless the verifier checks some state, so "immediate" logout is a trade-off. Options:

1. **Short access token lifetime** (5–15 min) plus revoking the **refresh token family** on logout. The access token dies soon. This is the usual answer.
2. **Denylist** the token's `jti` or session ID (`sid`) in Redis with a TTL equal to the remaining lifetime, and check it on each request. That adds back a lookup, but only one small key per logout.
3. A **per-user token version** (or `sid` validity) checked against a cache — it also supports "log out everywhere" and password-change revocation.

Clearing the cookie client-side isn't enough: anyone who copied the token can still use it.

**Follow-ups:** How do you revoke tokens across microservices? (Publish revocations, or have services check a shared session store for sensitive operations.) Doesn't the denylist make JWT pointless? (Partly — that's the honest trade-off from Q8.)

**Great answer includes:** "Can't revoke without state"; short TTL + refresh revocation; `jti`/`sid` denylist with TTL; the honest trade-off.

#### Q36. The logs say "shutdown complete, exitCode 0", but the container's exit code is 137. Is the shutdown code broken?

**Model answer.** Not necessarily. **137 = 128 + 9 — the process was SIGKILLed** by the runtime because the **grace period** ran out before the process exited. Common causes:

- a grace period shorter than drain delay + close time (I hit this: a Docker setup where every container had `StopTimeout: 1`, so a 1 s drain was killed right after "shutdown complete" — with `docker stop -t 30` it exited with 0);
- something keeping the event loop alive after cleanup — an open handle such as a non-unref'd interval, a socket or a client that wasn't closed (`process.getActiveResourcesInfo()` shows what's left);
- the signal not reaching Node at all (`npm start` or a shell as PID 1), so the whole grace period passes before the KILL.

To diagnose, check the configured grace period (`docker inspect`, `terminationGracePeriodSeconds`, ECS `stopTimeout`), the time between "shutdown started" and the kill, and the active resources after cleanup. 143 (128 + 15) means it died of the SIGTERM itself — no handler.

**Follow-ups:** What exit code does an OOM kill produce? (Also 137 — check `OOMKilled` in `docker inspect` or the pod status.)

**Great answer includes:** Decoding 128 + signal; grace period vs drain timing; leftover handles; PID 1 signal forwarding; OOM as the other 137.

---

## 10. Common Mistakes & Red Flags

| Red flag | Why it hurts | Say/do instead |
|----------|--------------|----------------|
| "Node is single-threaded, so it can't use multiple cores" | Ignores the thread pool, workers and cluster; signals shallow knowledge | JS runs on one thread; libuv pool, `worker_threads`, one process per core/container |
| Sync APIs (`readFileSync`, `pbkdf2Sync`, big `JSON.parse`) in request paths | Blocks every request, not just one | Async APIs; worker pool for CPU work; stream large payloads |
| Ignoring `write()`'s return value, or using `.pipe()` everywhere | Unbounded memory; leaked descriptors on error | `pipeline()` from `node:stream/promises` |
| `express-async-errors` or try/catch in every handler on Express 5 | Outdated; noise | Express 5 forwards rejections; one central error handler |
| Swallowing errors in `uncaughtException`/`unhandledRejection` and carrying on | Runs in an unknown state; hides bugs | Log, shut down gracefully, let the supervisor restart |
| Long-lived JWTs in `localStorage`; "logout" that only deletes the token client-side | XSS steals them; they stay valid | Short access tokens, rotating refresh in `HttpOnly` cookie, server-side revocation |
| SHA-256/MD5 for passwords, or sync bcrypt on the main thread | Crackable; blocks the loop | argon2id/scrypt async, stored parameters, rehash on login |
| In-memory rate limiting or sessions with multiple instances | Limits multiply per instance; sessions vanish on restart | Redis with atomic scripts; shared session store |
| Buffering uploads in memory (`multer` memory storage) without limits | One large upload OOMs the process | Stream with limits, or pre-signed URLs |
| Cache without TTL jitter, stampede protection or Redis-down handling | DB overload on expiry; outage when Redis blips | Single-flight + lock + jitter; degrade to a miss |
| Non-idempotent queue jobs | Duplicate emails/charges on retry | Deterministic job IDs, idempotency keys, outbox |
| Raw URLs as metric labels; logging full request/response objects | Cardinality explosion; leaked secrets; huge log bills | Route templates; serializers; redaction |
| Database checks in the liveness probe | Dependency outage → restart storm | Liveness = process only; readiness = dependencies |
| `process.exit()` on SIGTERM; `CMD ["npm","start"]` | Drops in-flight requests; signals may not arrive | Drain, close in order, exit naturally; exec-form `node` |
| Hostname-only SSRF checks | Bypassed by DNS, decimal IPs, IPv6, redirects | Connect-time IP check, redirect re-validation, egress rules |
| Mocking the database in all tests | Misses constraint, isolation and SQL bugs | Testcontainers Postgres for integration tests |
| "We'll add more instances" for every latency problem | Hides the real queue; can overload the database | Measure loop delay, pools, downstream, GC first |

---

## 11. Quick Revision Summary

### One-page recap

**Runtime**
- V8 runs JS on one thread; libuv provides the event loop, OS async I/O for sockets, and a 4-thread pool for `fs`, `dns.lookup`, crypto and zlib. Set `UV_THREADPOOL_SIZE` at launch.
- Phases: timers → pending → poll → check (`setImmediate`) → close. After each callback: nextTick queue, then microtasks, repeat. libuv 1.45+ (Node 20+) runs timers only after poll.
- Inside I/O: nextTick > promise > immediate > timeout. CJS top level: nextTick before promises; ESM top level: promises first.
- Measure loop delay (`monitorEventLoopDelay`) before guessing; profile with `--cpu-prof`.

**Streams & concurrency**
- `highWaterMark` 16 KiB (16 objects, `fs` 64 KiB); `write()` → `false` → wait for `'drain'`. Use `pipeline()` + async generators.
- cluster = processes sharing a port (often replaced by one process per container); `worker_threads` = CPU work behind a pool; `child_process` = other programs.
- `AsyncLocalStorage` for request context; typed `EventEmitter`; built-ins replace `node-fetch`, `dotenv` (`--env-file`), `nodemon` (`--watch`), `ts-node` (type stripping, stable since 24.12).

**HTTP & frameworks**
- Express 5: async rejections forwarded; new path syntax (`/*splat`, `{/:id}`); `req.query` getter; `req.body` undefined without a parser. Errors outside the promise chain still crash.
- Fastify: schemas, encapsulation, Ajv strips extra properties and coerces. Nest 12: DI/modules/guards/pipes, ESM-only, Node 20.19+/22.12+.
- Typed `AppError` hierarchy → one error handler → problem+json; `expose` controls messages. Validate env and input with Zod.

**Auth & edges**
- argon2id/scrypt, PHC strings, rehash, dummy hash, rate-limited login. Short EdDSA access JWT; opaque rotating refresh tokens in families with reuse detection; `HttpOnly` cookie; PKCE for OAuth.
- Rate limits in Redis via Lua (token bucket); `429` + `Retry-After`; correct `trust proxy`; fail-open vs fail-closed per route.
- Uploads: pre-signed URLs first; else stream busboy → `lib-storage` with limits, magic bytes, abort cleanup.
- SSE for one-way, WebSockets for two-way; broker fan-out; heartbeats; `bufferedAmount`; ticket auth at upgrade.

**Production**
- Cache-aside, delete on write, single-flight + lock + jitter + negative cache, Redis down → miss.
- BullMQ: at-least-once → idempotent jobs; backoff; `UnrecoverableError`; schedulers; `worker.close()`.
- Pino JSON logs + ALS mixin + redaction + compact serializers; OTel needs the ESM loader hook and `shutdown()` flush; Prometheus histograms with route-template labels.
- Liveness = process; readiness = dependencies and shutdown state.
- SIGTERM: fail readiness → drain delay → `server.close()` + `Connection: close` → close workers, pools, telemetry → exit within the grace period. 137 = SIGKILL.
- Security: connect-time SSRF checks, prototype-pollution-proof parsing, ReDoS-safe regexes, `npm ci` + audits, permission model (`--permission`).
- Tests: Supertest + Testcontainers Postgres + `node --test "glob"`. Leaks: heap-after-GC trend → snapshot diff → retainers.

### Last-day checklist

- [ ] I can draw the event loop phases and predict the output of a mixed timer/immediate/nextTick/promise puzzle in both ESM and CJS.
- [ ] I can list the thread-pool APIs and explain the `dns.lookup` gotcha.
- [ ] I can explain backpressure with `write()`/`'drain'` and why `pipeline()` beats `.pipe()`.
- [ ] I can choose between cluster, workers and child processes with one sentence each.
- [ ] I can name five Express 5 changes and the async error it *still* can't catch.
- [ ] I can whiteboard refresh token rotation with families and reuse detection, and explain JWT revocation honestly.
- [ ] I can write a Redis token-bucket limiter outline and explain why it must be a Lua script.
- [ ] I can explain cache stampede defenses and at-least-once job idempotency.
- [ ] I can walk through SIGTERM to exit in order, and decode exit codes 137 and 143.
- [ ] I can debug "p99 doubled at 40% CPU" by listing the queues to check.
- [ ] I can answer Q31–Q36 cold.

---

## Next Steps

- Update your Node.js rows in the [Progress Tracker](./00-README.md#progress-tracker).
- Keep the [Part 3 notes service](./06-nodejs-part3.md#4-full-example-the-notes-service) as your sandbox: run the exercises against it, and rebuild it on each new Node LTS to see what changed.
- ➡️ Continue to [07-databases-and-apis.md](./07-databases-and-apis.md) — SQL and PostgreSQL internals, indexing, transactions, MongoDB, Redis data structures, ORMs, and REST/GraphQL/tRPC/gRPC design with pagination, idempotency and versioning.
