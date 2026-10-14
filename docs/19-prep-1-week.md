# 19 — Prepare in 1 Week

> **7 days × ~6 h ≈ 42 h.** High rows in JS, React, Next, Node, DB, one machine UI, two designs, ~10 DSA, 6 STARs, **2 mocks**. Not the [4-week](./16-study-plan-part1.md) (~144 h). Shorter: [18 — 2 days](./18-prep-2-days.md). Longer: [20 — 2 weeks](./20-prep-2-weeks.md).
>
> Tick **in order**. 1 DSA every day. Do **not** start user DB containers or billed AWS.

## Table of Contents

- [Rules](#rules)
- [Daily template](#daily-template)
- [What “done” means](#what-done-means)
- [Skip](#skip)
- [Day 1 — JavaScript](#day-1--javascript)
- [Day 2 — TypeScript + implementations](#day-2--typescript--implementations)
- [Day 3 — React + machine UI](#day-3--react--machine-ui)
- [Day 4 — Next + Node](#day-4--next--node)
- [Day 5 — Data + limiter](#day-5--data--limiter)
- [Day 6 — Shortener, STARs, sheets](#day-6--shortener-stars-sheets)
- [Day 7 — Mock and stop](#day-7--mock-and-stop)
- [If you fall behind](#if-you-fall-behind)
- [JD swap](#jd-swap)
- [Last-day checklist](#last-day-checklist)

---

## Rules

1. Open the **linked file**, Topic Map, High rows only. Do not read Medium/Low.
2. Out loud. Silent reading is not prep.
3. Miss a day: keep DSA + one STAR; slide the topic; **do not** double tomorrow.
4. One half-evening off (pick Day 3 or 5). Sleep.
5. Recite [17](./17-cheatsheets.md) only on Days 6–7, not as the course.

---

## Daily template

| Block | Time | What |
|------|:----:|------|
| A — Topic | 3.5–4 h | Today’s files, tick below |
| B — DSA | 45–50 min | **One** timed problem, talk ([13](./13-coding-round-practice.md)) |
| C — Drill | 25 min | Puzzles **or** STAR **or** leftover UI |
| D — Close | 15 min | 5 bullets for tomorrow |

---

## What “done” means

You will **not** tick all of [Ready](./00-README.md#what-ready-means). After Day 7 you should:

- [ ] Medium DSA ~25–35 min talking (arrays/window/tree)
- [ ] One UI in 60 min (autocomplete **or** modal)
- [ ] Loop / `this` / closure puzzles
- [ ] `debounce` + `promiseAll` from memory
- [ ] Next cache story + auth token story
- [ ] Limiter + shortener on paper
- [ ] Pitch + **6** STARs (impact, ownership, conflict, failure, ambiguity, deadline)
- [ ] Two mocks logged (Day 4 lite + Day 7)

---

## Skip

[10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md) labs, DP, Kafka, GraphQL/gRPC, 08 Medium, Workers/DO, portfolio rewrite. Deploy = [17 Part 3](./17-cheatsheets-part3.md) tables on Day 6 if the JD names AWS/CF.

---

## Day 1 — JavaScript

**Open:** [02 Part 1](./02-javascript-part1.md), then loop/promises in the same hub. Puzzles: [14 Part 1](./14-js-logical-interview-questions-part1.md) + Q43 in [Part 2](./14-js-logical-interview-questions-part2.md). Pitch: [15 Part 1](./15-other-interview-questions-part1.md).

- [ ] Scope, TDZ, closures as live bindings
- [ ] `this` four rules + lost binding
- [ ] Browser loop: task → drain microtasks
- [ ] Promises: executor sync; `all` vs `allSettled`; `forEach` doesn’t await
- [ ] DSA: Two Sum + Contains Duplicate (if first < 25 min, second untimed)
- [ ] Puzzles Q1–Q10, then Q43 (`1 5 7 3 4 6 2`)
- [ ] Pitch skeleton (don’t record yet)

**Done when:** you can trace Q43 without notes.

---

## Day 2 — TypeScript + implementations

**Open:** [03](./03-typescript.md) High (narrowing, `satisfies`, `unknown`). [14 Part 3](./14-js-logical-interview-questions-part3.md). [02 Part 2](./02-javascript-part2.md) debounce skim.

- [ ] `any` vs `unknown` vs `never`; annotation vs `as` vs `satisfies`
- [ ] Discriminated union + `assertNever` (one example)
- [ ] Node 24: **no** constructor parameter properties
- [ ] Write `debounce`+cancel (20 min) and `promiseAll` (20 min)
- [ ] DSA: Valid Anagram, Group Anagrams **or** two pointers (palindrome / Two Sum II)
- [ ] Record pitch once (90–100 s)
- [ ] STAR **impact** drafted from a real ticket

**Done when:** debounce and `promiseAll` run without looking.

---

## Day 3 — React + machine UI

**Open:** [04 Part 1](./04-react-part1.md)–[Part 2](./04-react-part2.md) High. **Build:** [04 Part 3](./04-react-part3.md) autocomplete, **60 min cap**.

- [ ] Render vs commit vs effects (layout before passive; effects bottom-up)
- [ ] Keys; `memo` wasted when parent passes new inline children
- [ ] Three effects you’d delete (derive / handler / `key`)
- [ ] Autocomplete: happy path first, then keyboard, then polish — **stop at 60**
- [ ] DSA: sliding window (buy/sell **or** no-repeat substring)
- [ ] STAR **conflict**

**Done when:** you shipped a typed list + input, not a design system.

---

## Day 4 — Next + Node

**Open:** [05](./05-nextjs.md) App Router + caching High. [06](./06-nodejs.md) phases vs 02, auth, `/readyz`.

- [ ] Open Next answers with **version + caching model**
- [ ] `'use cache'` vs `React.cache`; `updateTag` vs `revalidateTag` vs `revalidatePath`
- [ ] Proxy ≠ auth; DAL on every action ([05](./05-nextjs.md) CVE-2025-29927)
- [ ] Node I/O puzzle order; access vs refresh + rotation
- [ ] DSA: stack (valid parens) **or** binsearch (`lo <= hi` vs `lo < hi`)
- [ ] STAR **failure**
- [ ] **Mock 1 (40 min):** one medium + 90 s pitch. Log 3 gaps.

**Done when:** 4-minute token talk is smooth.

---

## Day 5 — Data + limiter

**Open:** [07](./07-databases-and-apis.md) indexes, isolation, keyset, idempotency. [09](./09-system-design.md) framework + rate limiter.

- [ ] B-tree composite: equality then sort/range
- [ ] RC vs SSI (`40001`); lost update vs write skew
- [ ] Keyset pagination; Idempotency-Key on POST
- [ ] Prisma `include` = two SELECTs (don’t say “join”)
- [ ] **45 min design:** limiter — token bucket, Redis Lua pointer, 429
- [ ] DSA: invert tree, max depth (BFS = **index queue**, not `shift`)
- [ ] STAR **ownership**

**Done when:** you can pick `(user_id, created_at)` and say why.

---

## Day 6 — Shortener, STARs, sheets

**Open:** [09](./09-system-design.md) shortener. [15](./15-other-interview-questions.md) remaining cards + [Part 2](./15-other-interview-questions-part2.md) deep-dive. [17](./17-cheatsheets.md) Parts 1–2.

- [ ] URL shortener 45 min: 302 not 301, base62, cache the read
- [ ] 10 min deep-dive on **your** app (draw boxes)
- [ ] STAR **ambiguity** + **deadline**
- [ ] Two questions-to-ask (incident; 6-month success)
- [ ] Recite 17 JS/`this`/loop + React pipeline + Node SIGTERM
- [ ] DSA: BST validate **or** number of islands
- [ ] LRU from memory if Day 2 skipped it

**Done when:** 6 STAR titles exist on paper with real metrics.

---

## Day 7 — Mock and stop

**Open:** nothing new. [17 Part 3](./17-cheatsheets-part3.md) only if AWS/CF is on the JD (30 min cap).

- [ ] Weak-topic from Mock 1 — **one** hour max
- [ ] Mixed easy/medium DSA 40 min
- [ ] **Mock 2 (90 min):** 45 coding + 45 design **or** behavioral
- [ ] Three gaps — do not start a file
- [ ] Pitch + 2 STARs once
- [ ] Sleep. If the loop is tomorrow: [18 last-hour](./18-prep-2-days.md#last-hour-checklist) in the morning, 20 min

---

## If you fall behind

| Day missed | Collapse into |
|------------|----------------|
| 2 (TS) | Day 3 morning: `satisfies` + debounce only |
| 3 UI | Day 4 evening: 45 min modal instead of autocomplete |
| 5 design | Day 6: limiter **or** shortener, not both |
| 6 sheets | Day 7 morning: 17 Part 1 only |

Never skip Days **1, 4 (auth), 7 (mock)**.

---

## JD swap

| JD | Steal from | Give to |
|----|------------|---------|
| Backend | Day 3 polish | Extra 07 + chat design 20 min on Day 6 |
| Product | Day 5 isolation depth | Second 04 component on Day 6 |
| AWS in title | Day 6 shortener polish | [17 §12–13](./17-cheatsheets-part3.md#12-aws-ec2) 40 min — still no console |

---

## Last-day checklist

- [ ] Pitch recorded once this week
- [ ] Six STAR cards
- [ ] Two Sum, one window, invert tree from memory
- [ ] Token talk + Next cache talk
- [ ] Limiter **and** shortener drawn once
- [ ] Mock 2 done
- [ ] Sleep

➡️ Next longer path: [20-prep-2-weeks.md](./20-prep-2-weeks.md)
