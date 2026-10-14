# 18 — Prepare in 2 Days

> **~14 focused hours.** Filter-pass only: talk tracks + 8–10 DSA + 4 STARs + 1 design sketch. You will **not** finish [02](./02-javascript.md)–[15](./15-other-interview-questions.md). If you already studied those files, skip this and run [17 last 48 hours](./17-cheatsheets-part3.md#19-last-48-hours) instead.
>
> Longer: [19 — 1 week](./19-prep-1-week.md) · [20 — 2 weeks](./20-prep-2-weeks.md) · [16 — 4/8/12 weeks](./16-study-plan.md)
>
> Do **not** start Postgres/Redis/pgAdmin, billed AWS, or Cloudflare labs.

## Table of Contents

- [Rules](#rules)
- [What you will be able to do](#what-you-will-be-able-to-do)
- [Skip](#skip)
- [Day 1 — Talk tracks (8 h)](#day-1--talk-tracks-8-h)
- [Day 2 — Prove it (6 h) then stop](#day-2--prove-it-6-h-then-stop)
- [If the interview is tonight](#if-the-interview-is-tonight)
- [If you fall behind](#if-you-fall-behind)
- [JD swap](#jd-swap)
- [Last-hour checklist](#last-hour-checklist)

---

## Rules

1. Tick boxes **in order**. Do not skip ahead to AWS.
2. **Out loud.** Every DSA, puzzle, STAR, design.
3. **One timer.** Phone face-down except the clock.
4. Miss a block → drop the *next* Medium, keep DSA + pitch.
5. Sleep is a block. A 1 a.m. hard problem is a fail.

Daily shape is gone — you are on **hour blocks**.

---

## What you will be able to do

- [ ] Predict a closure / `this` / event-loop snippet ([14](./14-js-logical-interview-questions.md))
- [ ] Two Sum + one window + invert tree, talking ([13](./13-coding-round-practice.md))
- [ ] 90 s pitch + **4** STARs: impact, conflict, failure, ownership ([15](./15-other-interview-questions-part1.md))
- [ ] Access vs refresh in 4 minutes ([06](./06-nodejs.md))
- [ ] React render vs commit in 2 minutes ([04](./04-react.md))
- [ ] Next: “what is cached, what busts it” in 3 minutes ([05](./05-nextjs.md))
- [ ] Rate limiter **or** URL shortener on paper, 25 min ([09](./09-system-design.md))
- [ ] Recite [17 Part 1](./17-cheatsheets-part1.md) JS/`this`/loop table once

---

## Skip

AWS/EC2/S3/CloudFront depth ([10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md)), DP, graphs beyond islands, Prisma internals, 08 tooling, GraphQL, Workers, a new repo.

One sentence from [17 Part 3](./17-cheatsheets-part3.md) if they ask deploy: “ALB + `/readyz` + S3/OAC or Cloudflare Full strict” — then stop.

---

## Day 1 — Talk tracks (8 h)

**Goal.** Language + UI + Node auth in your mouth. Pitch v1.

### Block A — JavaScript (2 h)

Open: [02 Part 1](./02-javascript-part1.md) (scope, closures, `this`, browser loop). Then [17 §4](./17-cheatsheets-part1.md#4-javascript).

- [ ] Recite `this` order: `new` > explicit > implicit > default. Arrow = lexical.
- [ ] Recite loop: one task → **all** microtasks → maybe render.
- [ ] [14 Part 1](./14-js-logical-interview-questions-part1.md) Q1–Q10 **before** answers.
- [ ] [14 Part 2](./14-js-logical-interview-questions-part2.md) Q43. Target output: `1 5 7 3 4 6 2`. If wrong, re-read 02 loop once.

### Block B — DSA (50 min)

Open: [13 Part 1](./13-coding-round-practice-part1.md). Timer. Talk.

- [ ] Two Sum (hash).
- [ ] Contains Duplicate **or** Valid Anagram.
- [ ] If both finish early: Best Time to Buy/Sell (window).

### Block C — React + Next (2 h)

Open: [04 Part 1](./04-react-part1.md) render/commit/hooks. [17 §6](./17-cheatsheets-part1.md#6-react). Then [05](./05-nextjs.md) **caching High only** + [17 §7](./17-cheatsheets-part1.md#7-nextjs).

- [ ] Draw trigger → render → commit → paint → effects.
- [ ] Say why index keys shuffle state.
- [ ] Say: App Router = RSC; auth in **DAL** not proxy (CVE-2025-29927 in [05](./05-nextjs.md)).
- [ ] Say one invalidate: `updateTag` vs `revalidatePath` vs `router.refresh()` — from 05, don’t invent.

**Skip** 04 Part 3 full machine coding. You do **not** have 60 min for a component today.

### Block D — Node auth (1.5 h)

Open: [06](./06-nodejs.md) event-loop phases (vs 02) + auth High. [17 §8](./17-cheatsheets-part2.md#8-nodejs).

- [ ] Node order inside I/O: nextTick > promise > immediate > timeout. ESM top-level: promises before nextTick.
- [ ] 4-minute talk: short access JWT; opaque rotating refresh; HttpOnly; reuse = steal.
- [ ] SIGTERM one-liner: fail `/readyz` → drain → `server.close()` → exit. 137 = KILL.

### Block E — Pitch + 2 STARs (1 h)

Open: [15 Part 1](./15-other-interview-questions-part1.md). Real tickets. `{{placeholders}}` filled.

- [ ] Pitch: present → two beats with **numbers** → why this company. Record once (90–100 s).
- [ ] STAR **impact** (S/T short, A long, R = metric + learn).
- [ ] STAR **failure** (mitigate first).

### Block F — Close (20 min)

- [ ] Five bullets you’d say in a screen tomorrow.
- [ ] Stop. No LeetCode after this.

---

## Day 2 — Prove it (6 h) then stop

**Goal.** One design, two more STARs, implementations, one mock, sleep.

If the **interview is this evening**, use [If the interview is tonight](#if-the-interview-is-tonight) instead.

### Block A — DSA (50 min)

- [ ] Sliding window: longest substring without repeat **or** max profit.
- [ ] Invert binary tree **or** max depth.
- [ ] Quote costs: `shift`/`includes` O(n); `sort` needs a comparator ([13](./13-coding-round-practice.md)).

### Block B — Implementations (50 min)

Open: [14 Part 3](./14-js-logical-interview-questions-part3.md). Node 24: **explicit fields**, no constructor parameter properties.

- [ ] `debounce` + cancel (20 min).
- [ ] `promiseAll` by index (20 min).
- [ ] If time: LRU `Map` (20 min) — else skip.

### Block C — Design (45 min)

Open: [09](./09-system-design.md) 45-min spine. [17 §11](./17-cheatsheets-part2.md#11-system-design).

- [ ] **Rate limiter:** token bucket + Redis Lua (pointer [06](./06-nodejs.md), don’t re-derive). Draw boxes. 429 + `Retry-After`.
- [ ] If that was clean and 15 min left: URL shortener 302 + 7-char base62. Else stop.

### Block D — Data one-pager (40 min)

Open: [07](./07-databases-and-apis.md) indexes + isolation. [17 §9](./17-cheatsheets-part2.md#9-databases--apis).

- [ ] Composite index: **equality then range**. `(user_id, created_at)` for “my recent orders.”
- [ ] Default PG = `READ COMMITTED`. Lost update vs write skew. Serializable → retry `40001`.
- [ ] POST needs Idempotency-Key. Pagination = **keyset**, not `OFFSET` for hot paths.

### Block E — STARs + questions (40 min)

- [ ] STAR **conflict**.
- [ ] STAR **ownership**.
- [ ] Two questions to ask them: last incident; 6-month success ([15 Part 2](./15-other-interview-questions-part2.md)).

### Block F — Mock (45 min) then cheatsheet (20 min)

- [ ] 25 min: one medium DSA, talk, no notes.
- [ ] 10 min: pitch + one STAR.
- [ ] 10 min: log **three** gaps. Do **not** open a new file for them.
- [ ] Recite [17 Part 1](./17-cheatsheets-part1.md) JS + React tables once.
- [ ] **Sleep.**

---

## If the interview is tonight

Cut Day 2 to **4 h**, end 3 hours before the loop:

- [ ] Block A DSA (40 min)
- [ ] Block C design 25 min (limiter only)
- [ ] Pitch + 2 STARs once (20 min)
- [ ] [17](./17-cheatsheets.md) Part 1 JS/`this`/loop + Part 2 auth/index (30 min)
- [ ] Walk / food / sleep if it’s late — **no** mock, no new pattern

---

## If you fall behind

| Missed | Drop | Keep |
|--------|------|------|
| Day 1 Block C Next | Next cache talk | JS + React pipeline + auth |
| Day 1 puzzles | Q6–10 | Q1–5 + Q43 |
| Day 2 LRU | LRU | debounce + `promiseAll` |
| Day 2 design | Shortener | Limiter |

Never drop: **pitch**, **Two Sum**, **`this`/loop**, **4 STARs**.

---

## JD swap

| JD says | On Day 1 steal from | Give to |
|---------|---------------------|---------|
| Backend / platform | React 30 min | [07](./07-databases-and-apis.md) indexes |
| Product / frontend | Node SIGTERM | [04 Part 3](./04-react-part3.md) autocomplete 45 min |
| “AWS required” | Data one-pager | [17 §12–13](./17-cheatsheets-part3.md#12-aws-ec2) recite only — no console |

---

## Last-hour checklist

- [ ] Pitch under 100 s
- [ ] Four STAR cards in reach (impact, failure, conflict, ownership)
- [ ] `this` + microtask drain + access/refresh
- [ ] Two Sum from memory
- [ ] Limiter boxes
- [ ] Two questions for them
- [ ] Water; no new GitHub blog

➡️ Next longer path: [19-prep-1-week.md](./19-prep-1-week.md)
