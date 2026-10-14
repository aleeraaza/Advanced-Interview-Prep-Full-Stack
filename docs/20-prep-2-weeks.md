# 20 — Prepare in 2 Weeks

> **14 days.** ~6 h × 12 workdays + 2 mock/rest days ≈ **70–80 h**. This is the expanded [16 emergency](./16-study-plan-part3.md#15-less-than-two-weeks), not the [4-week](./16-study-plan-part1.md) (144 h) and not the 12-week complete path.
>
> Shorter: [18 — 2 days](./18-prep-2-days.md) · [19 — 1 week](./19-prep-1-week.md). Longer: [16](./16-study-plan.md) 4/8/12 weeks. Sheets: [17](./17-cheatsheets.md).
>
> Tick **one day at a time**. 1 DSA/day from day 1. 1 STAR every other day (8 by Day 12). Do **not** start user Postgres/Redis or billed AWS.

## Table of Contents

- [Rules](#rules)
- [Daily template](#daily-template)
- [What “done” means](#what-done-means)
- [Skip](#skip)
- [Week 1](#week-1)
- [Week 2](#week-2)
- [DSA list (don’t shuffle)](#dsa-list-dont-shuffle)
- [STAR cadence](#star-cadence)
- [If you fall behind](#if-you-fall-behind)
- [JD swap](#jd-swap)
- [Last-day checklist](#last-day-checklist)

---

## Rules

1. High rows only in each linked file. Medium only if that day’s table says so.
2. Out loud. Record pitch **once** (Day 3) and again if it was rambling.
3. Miss a day → keep DSA streak; slide topic by one; cut a Medium.
4. Mocks are **calendar events** (Days 7 and 13), not “when I feel ready.”
5. Week 2 is not “read everything again.” New files stop after Day 11 except [17](./17-cheatsheets.md).

---

## Daily template

Same as [16 Part 1 §5](./16-study-plan-part1.md#5-daily-template):

| Block | Time | What |
|------|:----:|------|
| A — Topic | 3.5–4 h | Today’s checklist |
| B — DSA | 45–60 min | One timed problem ([13](./13-coding-round-practice.md) / [NeetCode 150](https://neetcode.io/practice)) |
| C — Drill | 25–30 min | [14](./14-js-logical-interview-questions.md) ×5 **or** UI slice **or** STAR |
| D — Close | 15 min | 5 bullets |

---

## What “done” means

Closer to [Ready](./00-README.md#what-ready-means) than 19, still not staff AWS.

- [ ] Medium ~25 min talking (arrays → trees; islands)
- [ ] Autocomplete **or** infinite scroll in 60 min ([04 Part 3](./04-react-part3.md))
- [ ] Puzzles: closures, `this`, Q43, `null == 0` vs `null >= 0`
- [ ] `debounce`, `promiseAll`, LRU
- [ ] React pipeline + Next cache invalidation
- [ ] Auth tokens + SIGTERM + `/readyz`
- [ ] Indexes + isolation + keyset + idempotent POST
- [ ] Three designs: limiter, shortener, chat ([09](./09-system-design.md))
- [ ] Pitch + **8** STARs + 10 min deep-dive
- [ ] Two mocks (Day 7 coding, Day 13 dress)

---

## Skip

DP beyond “robber / coin change sentence,” tries, Kafka deep, GraphQL/gRPC, 08 Medium, Workers/DO, ASG tuning, a greenfield SaaS. Cloud: **recite** [17 §12–14](./17-cheatsheets-part3.md#12-aws-ec2) on Day 11 — no console.

---

## Week 1

### Day 1 — JS core

**Open:** [02 Part 1](./02-javascript-part1.md). [14 Part 1](./14-js-logical-interview-questions-part1.md) Q1–Q10. [15](./15-other-interview-questions-part1.md) pitch skeleton.

- [ ] Execution, scope, TDZ, closures
- [ ] `this` + prototypes skim
- [ ] DSA: Two Sum, Contains Duplicate
- [ ] Pitch outline (no recording)

### Day 2 — Loop, promises, puzzles

**Open:** 02 event loop + promises. [14 Part 2](./14-js-logical-interview-questions-part2.md) Q43–Q50.

- [ ] Browser: task → all microtasks → render
- [ ] `all` / `allSettled` / `race` / `any`; `return await` in `try`
- [ ] Q43 = `1 5 7 3 4 6 2`
- [ ] DSA: Group Anagrams, product except self
- [ ] STAR **impact**

### Day 3 — Implementations + TS High

**Open:** [02 Part 2](./02-javascript-part2.md), [14 Part 3](./14-js-logical-interview-questions-part3.md), [03](./03-typescript.md) High.

- [ ] `debounce`+cancel, `promiseAll` (explicit fields, Node 24)
- [ ] `unknown` / `satisfies` / discriminated union
- [ ] DSA: two pointers (3Sum **or** container with water)
- [ ] Record pitch 90 s
- [ ] STAR **ownership**

### Day 4 — React model

**Open:** [04 Part 1](./04-react-part1.md)–[Part 2](./04-react-part2.md).

- [ ] Render/commit; keys; effects order; “you might not need an effect”
- [ ] `useTransition` vs `useDeferredValue` (not debounce)
- [ ] DSA: sliding window (no-repeat **or** min window)
- [ ] Autocomplete **skeleton** only ([04 Part 3](./04-react-part3.md))
- [ ] STAR **conflict**

### Day 5 — Machine UI + Next High

**Open:** [04 Part 3](./04-react-part3.md) 60 min cap. [05](./05-nextjs.md) RSC + cache.

- [ ] Finish autocomplete **or** modal — happy path then a11y
- [ ] Next: version + shell vs cached vs streamed; tag APIs
- [ ] Proxy ≠ DAL auth
- [ ] DSA: stack (parens, daily temps)
- [ ] STAR **failure**

### Day 6 — Node

**Open:** [06](./06-nodejs.md) phases vs 02, Express errors, auth, Redis limiter pointer, shutdown.

- [ ] nextTick vs promise vs immediate (CJS vs ESM top-level)
- [ ] Access + refresh rotation talk (4 min)
- [ ] `/readyz` vs liveness; SIGTERM order; 137
- [ ] DSA: reverse list, cycle detect
- [ ] STAR **ambiguity**
- [ ] Optional: 45 min pagination API ([13 Part 4](./13-coding-round-practice-part4.md)) if auth talk was already solid

### Day 7 — Mock 1 + light

- [ ] **Mock 1 (60 min):** one medium + pitch + one STAR
- [ ] Log **3 gaps** → Days 8–12 override “next file”
- [ ] Easy DSA if behind; else rest
- [ ] Do **not** start 07 today

---

## Week 2

### Day 8 — Databases & APIs

**Open:** [07](./07-databases-and-apis.md) indexes, `EXPLAIN`, isolation, keyset, idempotency.

- [ ] `(user_id, created_at)` vs reverse
- [ ] RC lost update / write skew; SSI `40001`
- [ ] Keyset; Idempotency-Key; CORS ≠ authz
- [ ] DSA: invert tree, depth, BST validate (index-queue BFS)
- [ ] STAR **deadline**

### Day 9 — Design: limiter + shortener

**Open:** [09](./09-system-design.md) spine. [17 §11](./17-cheatsheets-part2.md#11-system-design).

- [ ] 45 min **rate limiter**
- [ ] 45 min **URL shortener** (302, base62)
- [ ] Fermi: day/8.6e4 ≈ /s, peak ×5
- [ ] DSA: LCA **or** level order
- [ ] STAR **mentor**

### Day 10 — Design: chat + behavioral spine

**Open:** [09](./09-system-design.md) chat. [15 Part 2](./15-other-interview-questions-part2.md).

- [ ] 45 min **chat**: persist then pub/sub
- [ ] 10 min project deep-dive (draw **your** boxes)
- [ ] Incident one-pager: detect → mitigate → cause → lasting fix
- [ ] Questions to ask (incident; 6-month success)
- [ ] DSA: number of islands
- [ ] STAR **influence**

### Day 11 — Weakest topic + cloud recite + LRU

**Open:** the Mock 1 gap file **or** leftover 04/06. Then [17 Part 3](./17-cheatsheets-part3.md) §12–14 (30–40 min). [14](./14-js-logical-interview-questions-part3.md) LRU.

- [ ] One gap only (max 3 h)
- [ ] Recite: VPC/IMDSv2/`/readyz`; S3 strong consistency + OAC; orange vs Full strict
- [ ] LRU from memory
- [ ] DSA: course schedule **or** Top K (heap you wrote)
- [ ] No new AWS account work

### Day 12 — Cheatsheets + mixed DSA

**Open:** [17 Parts 1–2](./17-cheatsheets-part1.md).

- [ ] Recite JS/`this`/loop, React pipeline, Next tags, Node SIGTERM, indexes
- [ ] Puzzle traps: `null == 0` false, `null >= 0` true; `map` skips holes ([17 §16](./17-cheatsheets-part3.md#16-js-puzzle-traps))
- [ ] Mixed medium 60 min
- [ ] All 8 STAR titles readable in 15 min
- [ ] Improve-the-app 15 min ([15](./15-other-interview-questions-part2.md)) if energy

### Day 13 — Dress mock

- [ ] **Mock 2 (90–120 min):** coding **or** machine, plus design **or** behavioral ([16 mock scripts](./16-study-plan-part3.md#14-mock-scripts))
- [ ] Three gaps — morning of Day 14 **only** if the loop is Day 15+
- [ ] Pitch + 2 STARs
- [ ] Stop by early evening. Sleep.

### Day 14 — Interview or rest

- [ ] If interviewing **today:** [18 last-hour](./18-prep-2-days.md#last-hour-checklist) (20 min). No DSA hard.
- [ ] If interviewing **tomorrow:** [17 last 48 hours](./17-cheatsheets-part3.md#19-last-48-hours) morning block only (3 h cap), then rest.
- [ ] If you have extra time: easy review, walk, sleep. **No new patterns.**

---

## DSA list (don’t shuffle)

Do **one timed** per day. Second problem only if the first finished under 20 min.

| Days | Patterns |
|:----:|----------|
| 1–3 | Hash, two pointers |
| 4–5 | Window, stack |
| 6–7 | Lists; mock uses a window or hash |
| 8–10 | Trees, islands |
| 11–12 | Heap **or** course-schedule; mixed |
| 13–14 | None new |

`shift` is O(n). Binsearch: `lo = mid` loops. Templates: [13](./13-coding-round-practice.md).

---

## STAR cadence

| Day | Slot |
|:---:|------|
| 2 | impact |
| 3 | ownership |
| 4 | conflict |
| 5 | failure |
| 6 | ambiguity |
| 8 | deadline |
| 9 | mentor |
| 10 | influence |

Days 12–13 = rehearse, don’t invent epics. Bank: [15 Part 1](./15-other-interview-questions-part1.md).

---

## If you fall behind

| Behind by | Cut |
|-----------|-----|
| 1 day | Day 11 gap block |
| 2 days | Chat design (keep limiter + shortener) |
| 3 days | Collapse to [19](./19-prep-1-week.md) from whatever day you have left — do not “speed 20” |

Never cut: Days **1–2 (JS)**, **6 (auth)**, **7 and 13 (mocks)**.

---

## JD swap

| JD | Steal | Give |
|----|-------|------|
| Backend | Day 5 UI polish | Extra 07 transactions + outbox sentence from 09 |
| Product | Day 11 cloud recite | Second 04 build (infinite scroll) |
| AWS/Cloudflare named | Day 10 chat | [10](./10-deployment-aws-ec2.md)/[11](./11-deployment-aws-s3.md)/[12](./12-cloudflare.md) **High rows only**, still no billed resources |
| Staff-leaning | Day 12 mixed DSA | [15 Part 3](./15-other-interview-questions-part3.md) staff vs IC 45 min |

---

## Last-day checklist

- [ ] Pitch under 100 s
- [ ] Eight STAR cards
- [ ] Deep-dive drawing of **your** system
- [ ] Two Sum, window, invert tree, islands
- [ ] debounce / `promiseAll` / LRU
- [ ] Token talk + Next cache talk + index talk
- [ ] Limiter, shortener, chat each drawn once
- [ ] Mock 2 done
- [ ] Sleep

Hub of calendars: [16-study-plan.md](./16-study-plan.md). Recitation: [17-cheatsheets.md](./17-cheatsheets.md).
