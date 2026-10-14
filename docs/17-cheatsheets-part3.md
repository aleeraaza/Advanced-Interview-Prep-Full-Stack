# 17 — Cheatsheets (Part 3 of 3): Cloud, Coding, Behavioral, 48 Hours

> **Parts:** [Part 1](./17-cheatsheets-part1.md) · [Part 2](./17-cheatsheets-part2.md) · **Part 3 — Cloud / DSA / STAR / 48 h**
>
> Canonical: [10](./10-deployment-aws-ec2.md)–[16](./16-study-plan.md). Do **not** launch billed AWS, change Cloudflare zones, or PUT to the user's account. Do **not** start user Postgres/Redis. Puzzle **answers** belong in [14](./14-js-logical-interview-questions.md) — this sheet is traps only.

## Table of Contents

- [12. AWS EC2](#12-aws-ec2)
- [13. S3 / CloudFront](#13-s3--cloudfront)
- [14. Cloudflare](#14-cloudflare)
- [15. DSA & Machine Coding](#15-dsa--machine-coding)
- [16. JS Puzzle Traps](#16-js-puzzle-traps)
- [17. Behavioral](#17-behavioral)
- [18. Which Plan](#18-which-plan)
- [19. Last 48 Hours](#19-last-48-hours)
- [20. Resources](#20-resources)
- [21. How to Learn It](#21-how-to-learn-it)
- [22. Hands-on Practice](#22-hands-on-practice)
- [23. Interview Flashcards](#23-interview-flashcards)
- [24. Common Mistakes](#24-common-mistakes)
- [25. Quick Revision](#25-quick-revision)
- [Next Steps](#next-steps)

---

## 12. AWS EC2

Canonical: [10](./10-deployment-aws-ec2.md). IAM instance-profile depth stays there.

| Topic | Recite |
|-------|--------|
| VPC | Two AZs. Public: ALB, NAT, IGW. Private: app, RDS. SG **stateful**, SG-id refs. |
| Identity | **Instance profile** for AWS APIs. **OIDC** for GitHub. No keys on disk. |
| IMDS | IMDSv2 **required** (AL2023). Token then GET. Hop limit **2** with containers. SSM not public SSH. |
| Compute | Family + Graviton `g`. AL2023 + `nodejs24` (to Apr 2028 as in 10). User data = bootstrap. |
| Lab | Nginx → `127.0.0.1:3000`; `trust proxy 1`; SELinux `httpd_can_network_connect`. ACM on **ALB** replaces Certbot on cattle. |
| Prod | ALB + ACM + `/readyz` + deregistration delay. ASG min 2, launch template. `pm2 reload` / CodeDeploy B/G. |
| DNS | Alias not CNAME at apex. |
| 50x | 502 refused/upstream · 504 timeout · T-credits · disk full. |
| Pillars | Operational excellence, security, reliability, performance efficiency, cost optimization, **sustainability**. |

---

## 13. S3 / CloudFront

Canonical: [11](./11-deployment-aws-s3.md).

| Topic | Recite |
|-------|--------|
| Consistency | **Strong** (Dec 2020+). Not eventual. |
| Who | BPA **on**. BucketOwnerEnforced (no ACLs). Never `Principal: "*"`. |
| App | IAM on instance/task role, **prefix**. ListBucket vs object ARN split — [11 Part 1](./11-deployment-aws-s3-part1.md). |
| CDN | CloudFront **REST** origin (not website endpoint) + **OAC** (not OAI). Policy: `cloudfront.amazonaws.com` + `AWS:SourceArn`. |
| ACM | CloudFront certs in **us-east-1**. |
| Presign | PUT match `Content-Type`; SDK v3 `s3-request-presigner`; default `expiresIn` **900**. `lib-storage` `Upload` is **server-side**, not with a presigned URL. |
| POST | Policy when you need **size caps** in the browser. |
| Crypto | SSE-S3 **default** Jan 2023. SSE-KMS needs key policy for CF. |
| SPA | CF 403/404 → `/index.html`. Private docs: signed GET — not the public static bucket. |
| Dead | S3 Select **closed** to new customers Jul 2024. |
| Cost | **Egress** first, then requests, leftover MPUs. |

---

## 14. Cloudflare

Canonical: [12](./12-cloudflare.md). L4/L7 theory: [09](./09-system-design.md).

| Topic | Recite |
|-------|--------|
| Orange / grey | Orange = proxy (anycast, CF IPs). Grey = origin IP in DNS. Mail **grey**. |
| TLS | **Full (strict)** + Origin CA or ACM. Flexible = HTTP to origin (bad). AOP = mTLS. **AOP ≠ Tunnel**. |
| Errors | 525/526 TLS · 521 origin down · 524 origin timeout. |
| Lock | SG from [cloudflare.com/ips](https://www.cloudflare.com/ips/) **or** Tunnel outbound-only. IP list **≠** auth. |
| Cache | Default skips HTML. Cache Rules (Page Rules legacy). Hashed assets long TTL. `/api` bypass. |
| WAF | Managed + custom. Login: edge + Redis per-user. |
| Workers | V8 isolate. Free **10 ms** CPU; Paid default **30 s** (max **5 min**); **128 MB**. KV ~**60 s** eventual. DO **strong per object**. |
| R2 | S3 API, `region: "auto"`, presign `*.r2.cloudflarestorage.com`, **no POST policy**. No-egress **pitch**; operations still cost. |
| vs CF | One public edge. CloudFront = AWS OAC native. Don't dual-CDN. |

---

## 15. DSA & Machine Coding

Canonical: [13](./13-coding-round-practice.md). UI builds: [04 Part 3](./04-react-part3.md).

**Round:** Clarify → brute+O → pattern → code → trace. **Talk.**

| JS cost | Complexity |
|---------|------------|
| `shift` / `unshift` / `splice` / `includes` | O(n) |
| `sort()` | n log n; **need comparator** for numbers |
| string concat in a loop | O(n²) worst (immutable) |
| `Map` / `Set` get/set | avg O(1) |

| Pattern | One line |
|---------|----------|
| Hash | complement / freq |
| Pointers | sorted ends or fast/slow |
| Window | expand right, shrink left while invalid |
| Stack | next greater / valid parens |
| Binsearch A | `lo <= hi`, mid discard |
| Binsearch B | `lo < hi`, answer space; `lo = mid` **loops** |
| List | dummy head |
| Tree BFS | **index queue**, not `shift` |
| Heap | you wrote `MinHeap` (no PQ in JS); **explicit fields**, no param properties |
| Graph | DFS/BFS, Kahn cycle, UF |
| DP | `dp[i]` in English first |
| Backtrack | choose / unchoose |

**UI 60 min:** happy path → a11y → polish. **API 45:** validate + keyset + one test.

---

## 16. JS Puzzle Traps

Canonical: [14](./14-js-logical-interview-questions.md). Don't dump 108 here.

| Trap | Recite |
|------|--------|
| `var` in `for` | one binding; `let` per iteration |
| Q43 | `1 5 7 3 4 6 2` |
| nested `then` | `a c b` as in Part 2 — don't swap |
| Node queues | nextTick before promises **in CJS**; ESM top-level promises first ([06](./06-nodejs.md)) |
| `null == 0` | **false**; `null >= 0` **true** |
| `map` holes | **skips** |
| WeakMap keys | objects + **symbols** (Node 24); strings **throw** |
| `[] + {}` | string `"[object Object]"`; statement `{} + []` → `0` (block) |
| `typeof null` | `"object"` |
| freeze | **shallow** |
| `forEach` + `async` | does not await |
| `return` vs `return await` | `await` in `try/catch` to catch |

---

## 17. Behavioral

Canonical: [15](./15-other-interview-questions.md). `{{placeholders}}` — your tickets.

| Card | Recite |
|------|--------|
| Pitch 90 s | Present → two beats **with metrics** → why here |
| STAR | Short S/T, long **A**, R = number + learn |
| Eight | impact · ownership · conflict · failure · ambiguity · deadline · mentor · influence |
| LPs | Amazon **16** = coverage prompt, not a script |
| Deep-dive | Draw, your boxes, hard part, regret, five whys |
| Incident | Mitigate first → cause → lasting fix → blameless ([sre.google](https://sre.google/sre-book/postmortem-culture/)) |
| Product | User + one lens + 2-week bet + metric |
| Ask | Last incident; 6-month success |
| Resume | X/Y/Z; only defendable |
| Neg | Level first; writing; no fake offers. [McKenzie](https://kalzumeus.com/2012/01/23/salary-negotiation/) · [Qureshi](https://haseebq.com/my-ten-rules-for-negotiating-a-job-offer/) — paraphrase |

---

## 18. Which Plan

Canonical: [16](./16-study-plan.md). Hours: [01](./01-fullstack-syllabus.md#time-budget-overview).

| Hours | Do |
|-------|----|
| < 40 | **This file** + 15 DSA mediums + 4 STAR + [14](./14-js-logical-interview-questions.md) loop/closure |
| 40–180 | [4-week](./16-study-plan-part1.md) |
| 180–350 | [8-week](./16-study-plan-part2.md) |
| 350+ | [12-week](./16-study-plan-part3.md) |

Every day: 1 DSA. During 02: 5 puzzles. Every week: 1 STAR.

---

## 19. Last 48 Hours

| When | Hours | Do |
|------|:-----:|----|
| Night −2 | 3 | [Part 1](./17-cheatsheets-part1.md) aloud + 10 puzzles (no answers first) + pitch once |
| Morning −1 | 3 | [Part 2](./17-cheatsheets-part2.md) + one 20-min design sketch (limiter **or** shortener) |
| Afternoon −1 | 2 | Two STARs + deep-dive draw + `Promise.all` / debounce / LRU from memory |
| Evening −1 | 1 | [§12–§14](#12-aws-ec2) tables; **stop**. Sleep |
| Morning of | 0.5 | Pitch + `this` rules + isolation levels. Water. No new GitHub blogs |

> ⚠️ Pitfall: "One more NeetCode hard" the night before. It only raises cortisol.

---

## 20. Resources

| Resource | Where | Use |
|----------|-------|-----|
| Every topic file | [02](./02-javascript.md)–[16](./16-study-plan.md) | Canonical |
| Ready checklist | [00](./00-README.md#what-ready-means) | Pass/fail |
| NeetCode 150 | [neetcode.io/practice](https://neetcode.io/practice) | DSA order |
| TIH | [techinterviewhandbook.org](https://www.techinterviewhandbook.org/) | Behavioral/resume |
| CF IPs | [cloudflare.com/ips](https://www.cloudflare.com/ips) | SG lock |

---

## 21. How to Learn It

**~6 h** of recitation over two days — not a second syllabus. If a cell is blank, **open the linked file** for 10 minutes, then return.

| Block | Time |
|-------|:----:|
| Part 1 | 1.5 h |
| Part 2 | 1.5 h |
| Part 3 cloud + DSA | 1.5 h |
| Puzzles + impl | 1 h |
| STAR + pitch | 0.5 h |

---

## 22. Hands-on Practice

1. Recite §4 `this` + loop without looking.
2. Write debounce + `promiseAll` in 20 min ([14](./14-js-logical-interview-questions-part3.md)).
3. Draw VPC + orange-cloud path on one page.
4. Record pitch once; delete the file if you want — the point is the clock.
5. Tick [Ready](./00-README.md#what-ready-means). Gaps → [16](./16-study-plan.md), not a new course.

---

## 23. Interview Flashcards

One-line models. Follow-ups live in 02–15.

### Basic

#### Q1. `this` rules?

**Model answer.** `new` > explicit > implicit > default. Arrow lexical.

**Follow-ups:** Extracted method?

**Great answer includes:** Lose implicit; `bind` / wrap / arrow field.

#### Q2. Microtask vs task?

**Model answer.** After a task, **drain all** microtasks, then next task. `then`/`await` = micro.

**Follow-ups:** Node `setImmediate`?

**Great answer includes:** Check phase; [06](./06-nodejs.md) order.

#### Q3. `any` vs `unknown` vs `never`?

**Model answer.** Opt-out / safe top / bottom.

**Follow-ups:** `satisfies`?

**Great answer includes:** Checked, keeps inferred type.

#### Q4. Why did this child re-render?

**Model answer.** Parent render, context, or own state — not props by magic.

**Follow-ups:** `memo`?

**Great answer includes:** Identity of props; children-as-props pitfall.

#### Q5. RSC vs SSR?

**Model answer.** RSC can stay on the server with zero client JS; SSR still hydrates UI. Serializable props.

**Follow-ups:** `"use client"`?

**Great answer includes:** Entry boundary, not "makes it client-only forever" for children.

#### Q6. Access vs refresh?

**Model answer.** Short JWT access; opaque rotating refresh HttpOnly; reuse detection.

**Follow-ups:** Where stored?

**Great answer includes:** [06](./06-nodejs.md) talk track.

#### Q7. Composite index order?

**Model answer.** Equality columns, then range/sort.

**Follow-ups:** Function on column?

**Great answer includes:** Index not used unless expression index.

#### Q8. CORS vs CSRF?

**Model answer.** CORS = browser relaxation. CSRF = cookie-authenticated browser. Bearer header ≠ CSRF.

**Follow-ups:** `SameSite=Lax` enough?

**Great answer includes:** Not for all cookie APIs; [08](./08-engineering-practices.md).

---

### Intermediate

#### Q9. Next invalidate choices?

**Model answer.** `updateTag` read-your-writes; `revalidateTag` SWR; expire 0 immediate; path; `router.refresh()`.

**Follow-ups:** Version?

**Great answer includes:** State the caching model first ([05](./05-nextjs.md)).

#### Q10. Why Lua for Redis limiter?

**Model answer.** Atomic read-modify-write. Race without it.

**Follow-ups:** Fail open?

**Great answer includes:** Per-route; login fail-closed.

#### Q11. Lost update vs write skew?

**Model answer.** Lost update: two read-modify-write. Write skew: each tx ok, together not. RC allows both; SSI retries `40001`.

**Follow-ups:** Default PG?

**Great answer includes:** `READ COMMITTED`.

#### Q12. CAP on the logo?

**Model answer.** No — **on the path**. PACELC when partitioned vs not.

**Follow-ups:** Dynamo vs PG?

**Great answer includes:** Don't brand; [07](./07-databases-and-apis.md)/[09](./09-system-design.md).

#### Q13. OAC in one sentence?

**Model answer.** CloudFront REST origin; bucket policy `cloudfront.amazonaws.com` + `SourceArn`; BPA on.

**Follow-ups:** OAI?

**Great answer includes:** Legacy; use OAC.

#### Q14. Orange cloud?

**Model answer.** Proxy: visitor hits CF, origin IP hidden. Grey = DNS only.

**Follow-ups:** Full vs Full (strict)?

**Great answer includes:** Strict verifies origin cert.

#### Q15. `shift` in BFS?

**Model answer.** O(n) per pop → O(n²). Index queue.

**Follow-ups:** `lo = mid`?

**Great answer includes:** Infinite loop in binsearch B.

#### Q16. `null >= 0`?

**Model answer.** `>=` coerces; `null` → `0`. `==` has a null exception.

**Follow-ups:** `map` holes?

**Great answer includes:** Skips.

---

### Advanced

#### Q17. CVE-2025-29927 lesson?

**Model answer.** Middleware/proxy bypass via crafted header. Auth in **DAL** on every action/page/handler ([05](./05-nextjs.md)).

**Follow-ups:** Layout as auth?

**Great answer includes:** Layouts don't cover Server Actions.

#### Q18. SIGTERM order?

**Model answer.** Fail `/readyz` → drain → `server.close()` → workers/pools/OTel → exit before grace. 137 = KILL.

**Follow-ups:** ALB?

**Great answer includes:** Deregistration delay ([10](./10-deployment-aws-ec2.md)).

#### Q19. Consistent hashing move fraction?

**Model answer.** ~1/N keys when adding a node; vnodes smooth; hot keys still hot.

**Follow-ups:** `% N`?

**Great answer includes:** Almost all keys move.

#### Q20. Workers vs Node origin?

**Model answer.** Isolate, 10 ms free CPU, 128 MB. Heavy SSR: Node on [10](./10-deployment-aws-ec2.md), CF as proxy.

**Follow-ups:** KV vs DO?

**Great answer includes:** Eventual ~60 s vs strong per object.

---

### Tricky

#### Q21. Parameter properties in Node 24?

**Model answer.** Type-stripping **rejects** them. Explicit fields.

**Follow-ups:** `enum`?

**Great answer includes:** Avoid with erasable syntax ([03](./03-typescript.md)).

#### Q22. `lib-storage` + presigned URL?

**Model answer.** Unsupported. Presign PUT **or** server `Upload`, not both ([11](./11-deployment-aws-s3.md)).

**Follow-ups:** Default expiry?

**Great answer includes:** 900 s.

#### Q23. CF IPs in SG — done?

**Model answer.** Necessary **not** sufficient. Anyone on CF can hit you. AOP/Tunnel/app auth.

**Follow-ups:** Stale list?

**Great answer includes:** Breaks you; [cloudflare.com/ips](https://www.cloudflare.com/ips).

#### Q24. Prisma `include` is a join?

**Model answer.** **Two SELECTs** in Prisma 7.

**Follow-ups:** When join?

**Great answer includes:** Raw SQL / Drizzle closer to SQL.

#### Q25. Ready because you finished 17?

**Model answer.** No. [Ready](./00-README.md#what-ready-means) without notes + recent mocks.

**Follow-ups:** Weakest area?

**Great answer includes:** Named + mitigation ([16](./16-study-plan.md)).

---

## 24. Common Mistakes

- Using 17 as the **course**.
- Mixing browser loop with Node phases in one sentence.
- Quoting Next cache APIs from a 2023 blog.
- "S3 is eventually consistent."
- OAI instead of OAC; website endpoint as CF origin.
- Auth in middleware only.
- `% N` sharding; `shift` BFS; `sort()` without comparator.
- Inventing STAR metrics.
- Launching AWS "to revise."
- Skipping sleep for one more hard.

---

## 25. Quick Revision

**JS:** `this` order, micro vs task, `null` equality vs relational. **TS:** erased, `satisfies`, no param properties. **React:** render/commit, keys, effects bottom-up. **Next:** version + DAL auth + tag APIs. **Node:** phases + refresh rotation + SIGTERM. **DB:** equality-then-range, RC vs SSI. **08:** trophy, OWASP 2025 A03/A10, CORS ≠ authz. **09:** spine + limiter/shortener/feed. **10:** VPC + IMDSv2 + `/readyz`. **11:** strong consistency, OAC, us-east-1 ACM. **12:** orange, Full strict, isolate limits. **13:** JS costs + `lo<=hi`. **14:** Q43 + traps. **15:** 90 s + 8 STAR. **16:** hours → plan.

### Last-day checklist

- [ ] Recited Parts 1–3 once each
- [ ] Pitch + two STARs warm
- [ ] One medium DSA + one puzzle set today **or** yesterday — not tonight
- [ ] Ready ticks honest ([00](./00-README.md#what-ready-means))
- [ ] Sleep

---

## Next Steps

The numbered set **00–17 is complete**. Use [16](./16-study-plan.md) as the calendar and this file as the last-48-hour pass. Hub: [17-cheatsheets.md](./17-cheatsheets.md).
