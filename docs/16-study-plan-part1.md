# 16 — Study Plan (Part 1 of 3): How to Choose & the 4-Week Plan

> **Parts:** **Part 1 — Choose + 4-Week** · [Part 2 — 8-Week](./16-study-plan-part2.md) · [Part 3 — 12-Week, Mocks, Interview](./16-study-plan-part3.md)
>
> Hours match [01 Time Budget](./01-fullstack-syllabus.md#time-budget-overview) and [Priority Triage](./01-fullstack-syllabus.md#priority-triage-if-you-only-have-x-hours). **12-week ≈ 480 h** at 5.5–6 h/day. **8-week ≈ 300–340 h** (all High + most-asked Medium). **4-week ≈ 140–170 h** (core High only). Parallel from **day 1**: 1 DSA ([13](./13-coding-round-practice.md)), 5 puzzles while in [14](./14-js-logical-interview-questions.md)/[02](./02-javascript.md), 1 STAR/week ([15](./15-other-interview-questions.md)). Do not launch billed AWS/Cloudflare labs on the 4-week path.

## Table of Contents

- [1. Overview](#1-overview)
- [2. Topic Map](#2-topic-map)
- [3. How to Use Any Plan](#3-how-to-use-any-plan)
- [4. Pick 4 / 8 / 12](#4-pick-4--8--12)
- [5. Daily Template](#5-daily-template)
- [6. The 4-Week Plan](#6-the-4-week-plan)
- [Next: Part 2](#next-part-2)

---

## 1. Overview

This file is a **calendar**, not more theory. You already have the syllabus ([01](./01-fullstack-syllabus.md)) and the topic files ([02](./02-javascript.md)–[15](./15-other-interview-questions.md)). Here: which hours on which day, when to mock, what to skip, and how to compress if the loop moved up.

| Plan | Calendar | Hours | You will **not** finish |
|------|----------|------:|-------------------------|
| **4-week** | 6 days × ~6 h (Sun light) | ~144–168 | Full NeetCode 150, AWS/CF depth, most Medium/Low, DP |
| **8-week** | 6–7 days × ~6 h | ~300–340 | Most Low rows, some AWS Medium, leisurely DP |
| **12-week** | 6–7 days × ~5.5–6 h | **~480** | Nothing required; Low still skippable if the JD is silent |

> 💡 Interview Tip: The job description **re-weights** the calendar. Backend-heavy: more [07](./07-databases-and-apis.md)/[09](./09-system-design.md). Product: more [04](./04-react.md)/[05](./05-nextjs.md)/machine coding. DevOps in the title: keep [10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md).

> ⚠️ Pitfall: Saving DSA for week 4. It is the slowest skill and the most common hard filter. **One problem every day from day 1.**

---

## 2. Topic Map

- [ ] Choose a plan from hours-until-loop — [4](#4-pick-4--8--12)
- [ ] Install the daily template — [5](#5-daily-template)
- [ ] Run 4-week if that is you — [6](#6-the-4-week-plan)
- [ ] 8-week — [Part 2](./16-study-plan-part2.md)
- [ ] 12-week, mock scripts, <2-week emergency — [Part 3](./16-study-plan-part3.md)

---

## 3. How to Use Any Plan

1. **Tick learning** in the [Progress Tracker](./00-README.md#progress-tracker), not just "I opened the file."
2. **Study method** is still [01](./01-fullstack-syllabus.md#the-learning-method-applies-to-every-row): read → one talk if needed → smallest build → aloud → revise.
3. **Out loud.** DSA, design, STAR, puzzles. Silent reading is not interview practice.
4. **Rest.** One half-day off per week. Sleep is a performance feature. Do not "make up" 12 hours on Sunday.
5. **Mocks are calendar events**, not "if I feel ready." Ready is a side effect of mocks.
6. **Skip Low** unless the JD names it. The triage table already decided this.

**If you miss a day.** Do **not** double tomorrow's topic block. Keep the DSA + one puzzle streak; slide the topic by one day and cut a Medium row.

---

## 4. Pick 4 / 8 / 12

| Hours you actually have | Plan | Also |
|-------------------------|------|------|
| **2 days** | [18-prep-2-days.md](./18-prep-2-days.md) | Sleep |
| **1 week** | [19-prep-1-week.md](./19-prep-1-week.md) | 2 mocks |
| **2 weeks** | [20-prep-2-weeks.md](./20-prep-2-weeks.md) | 2 mocks |
| **< 40** (not a 2-day block) | [17](./17-cheatsheets.md) + 15 DSA mediums + 4 STARs + event-loop/closure from [14](./14-js-logical-interview-questions.md). | Sleep |
| **40–180** | **4-week** (this part). If that 40–180 is actually ≤14 days, use [20](./20-prep-2-weeks.md) instead. | 2 mocks |
| **180–350** | **8-week** | 4+ mocks from week 3 |
| **350+** | **12-week** | Weekly mocks from week 3; optional portfolio slice |

Re-read the JD every Monday. Move hours; don't add a 13th week of random YouTube.

---

## 5. Daily Template

**Default block (6 h)** — shrink proportionally if you only have 3.

| Block | Time | What |
|------|:----:|------|
| A — Topic | 3.5–4 h | Current file: Topic Map ticks, code, exercises |
| B — DSA | 45–60 min | **One** NeetCode 150 problem, timer, talk ([13](./13-coding-round-practice.md)) |
| C — Drills | 30 min | [14](./14-js-logical-interview-questions.md) ×5 **or** a [04](./04-react-part3.md) UI slice **or** STAR/pitch ([15](./15-other-interview-questions.md)) |
| D — Close | 15–20 min | Write 5 bullets: what you'd say in a round tomorrow |

Sunday (or your rest day): mock **or** cheatsheet + missed DSA, not a new topic.

**DSA order** (don't shuffle): Arrays & hashing → two pointers → window → stack → binsearch → lists → trees → heap → graphs → backtracking → 1D DP → rest. Lists: [13](./13-coding-round-practice.md) / [neetcode.io/practice](https://neetcode.io/practice).

---

## 6. The 4-Week Plan

**Goal.** Pass **filters**: coding + one design + a human conversation. Not staff-level AWS.

**In:** High rows in JS, React, Next, Node, DB/APIs, DSA core, behavioral. Three designs: rate limiter, URL shortener, chat ([09](./09-system-design.md)). Two mocks.

**Out:** [10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md) depth, most of [08](./08-engineering-practices.md) Medium, DP/advanced graphs, Low rows, full 150.

**Hours.** 6 h × 6 days × 4 = **144 h**. Seventh day: 2–3 h mock/review (weeks 2 and 4 are mocks).

### Week 1 — Language + how you speak

| Day | Topic (block A) | DSA (block B) | Drills (block C) |
|-----|-----------------|---------------|------------------|
| 1 | [02 Part 1](./02-javascript-part1.md) execution, scope, closures | Two Sum / Contains Duplicate | [14](./14-js-logical-interview-questions-part1.md) Q1–Q5; start 90 s pitch |
| 2 | 02 `this`, prototypes, event loop | Valid Anagram, Group Anagrams | Q6–Q10; finish pitch draft |
| 3 | 02 promises/async + coercion | Product except self / Longest consecutive | Q43–Q47 event loop |
| 4 | [02 Part 2](./02-javascript-part2.md) debounce/throttle + `bind`/`Promise.all` skim | Two pointers: palindrome, Two Sum II | Implement debounce 20 min ([14](./14-js-logical-interview-questions-part3.md)) |
| 5 | [03](./03-typescript.md) High only (narrowing, generics you use) | 3Sum or Container with water | Pitch recorded 90 s |
| 6 | Catch-up + [14](./14-js-logical-interview-questions.md) mixed 15 | Sliding window: buy/sell + no-repeat | STAR slot **impact** drafted |
| 7 | Light: revise 02 Quick Revision | One easy if you missed a day | Rest or puzzles only |

### Week 2 — React + Next + machine coding

| Day | Topic | DSA | Drills |
|-----|-------|-----|--------|
| 8 | [04 Part 1](./04-react-part1.md) render, hooks, effects | Window: replacement / permutation | Autocomplete **skeleton** ([04 Part 3](./04-react-part3.md)) |
| 9 | [04 Part 2](./04-react-part2.md) state choice, memo, a11y bar | Min window or stock | Autocomplete happy path 60 min cap |
| 10 | 04 Part 3 modal + infinite scroll (pick one full) | Stack: valid parens, daily temps | STAR **conflict** |
| 11 | [05](./05-nextjs.md) App Router, RSC, caching **High** | Binsearch: classic + Koko | Next: explain cache invalidation aloud |
| 12 | 05 data fetching / auth skim as used in [06](./06-nodejs.md) | Rotated array **or** skip to lists | Tabs or pagination 45 min |
| 13 | Catch-up + RTL/a11y only as in 04/08 pointers | Reverse list, cycle | STAR **failure** |
| 14 | **Mock 1** (60 min): 1 medium DSA + 15 min "tell me about yourself" | — | Notes: 3 gaps → next week |

### Week 3 — Node, data, APIs

| Day | Topic | DSA | Drills |
|-----|-------|-----|--------|
| 15 | [06](./06-nodejs.md) event loop phases, libuv vs [02](./02-javascript.md) | Merge lists, reverse Nth | Auth: access + refresh **talk track** |
| 16 | 06 Express/Fastify, middleware, errors | Trees: invert, depth, BST validate | 45-min POST+GET pagination ([13](./13-coding-round-practice-part4.md)) |
| 17 | 06 rate limit / Redis pointer; shutdown `/readyz` | Level order, LCA | STAR **ownership** |
| 18 | [07](./07-databases-and-apis.md) indexes, isolation, **your** ORM | Graphs: islands | Pagination/idempotency aloud |
| 19 | 07 REST + HTTP + transactions skim | Course schedule | STAR **ambiguity** |
| 20 | Catch-up; one webhook/idempotency exercise | Connected components or UF | STAR **deadline** |
| 21 | Light + design **rate limiter** 45 min ([09](./09-system-design.md)) | Easy if behind | Rest |

### Week 4 — Design, behavioral, cut

| Day | Topic | DSA | Drills |
|-----|-------|-----|--------|
| 22 | URL shortener 45 min + review [09](./09-system-design.md) framework | Trees leftover | Pitch + 2 STARs aloud |
| 23 | Chat design 45 min | Heap: Top K **or** skip | Deep-dive 10 min on **your** project ([15](./15-other-interview-questions-part2.md)) |
| 24 | [15](./15-other-interview-questions.md) remaining STARs; questions to ask | Mixed medium | Incident postmortem one-pager |
| 25 | [17](./17-cheatsheets.md) when it exists; else 02/04/06 Quick Revisions | Mixed medium | Improve-an-app 15 min |
| 26 | Weakest topic only (you logged it week 2) | Mixed | `Promise.all` + LRU from memory |
| 27 | **Mock 2** (90 min): medium + 45 min design **or** behavioral | — | Send thank-you notes to yourself: 5 bullets |
| 28 | Rest + skim cheatsheets + sleep | Optional easy | No new topics |

**Week-4 honesty.** If the loop is backend, swap two React days in week 2 for extra 07/09. If product, swap week 3 Redis depth for another 04 build.

---

## Next: Part 2

➡️ [Part 2 — 8-Week Plan](./16-study-plan-part2.md): all High rows, NeetCode 150, Medium in React/Next/Node/design, weekly mocks from week 3.
