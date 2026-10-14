# 16 — Study Plan (Part 2 of 3): 8-Week Plan

> **Parts:** [Part 1 — Choose + 4-Week](./16-study-plan-part1.md) · **Part 2 — 8-Week** · [Part 3 — 12-Week, Mocks, Interview](./16-study-plan-part3.md)
>
> **~300–340 h.** All [01 High](./01-fullstack-syllabus.md#time-budget-overview) rows (≈ 303 h) plus **Medium** in React, Next.js, Node.js, and system design. Full NeetCode 150 **attempted**. Mocks from **week 3**. Daily habits still [Part 1 §5](./16-study-plan-part1.md#5-daily-template) with a longer DSA block.

## Table of Contents

- [7. 8-Week Intent](#7-8-week-intent)
- [8. Week-by-Week](#8-week-by-week)
- [9. Daily Shape (8-Week)](#9-daily-shape-8-week)
- [10. What You Skip](#10-what-you-skip)
- [11. Re-Weight by JD](#11-re-weight-by-jd)
- [Next: Part 3](#next-part-3)

---

## 7. 8-Week Intent

You are preparing for a **mid-to-senior** loop, not a crash filter. Interviewers will go one layer past cheatsheets: React re-renders, Next cache, Node event loop vs libuv, indexes, a real design.

| Track | Target |
|-------|--------|
| Topics | High **everywhere**; Medium in [04](./04-react.md), [05](./05-nextjs.md), [06](./06-nodejs.md), [09](./09-system-design.md) |
| DSA | NeetCode 150 **started**; ~80 clean under 25 min; rest attempted |
| Design | Framework + 6 problems (rate limiter, shortener, chat, news feed, unique ID, search **or** tickets) |
| Behavioral | 8 STAR slots + pitch + one project deep-dive ([15](./15-other-interview-questions.md)) |
| Cloud | **High only** in [10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md) — differentiator, not a second job |
| Mocks | **≥ 4** from week 3; week 8 is a dress rehearsal |

Hours: **6 h × 6 days × 8 = 288 h**, plus ~2–4 h Sunday mocks/review → **~310–330 h**. That is the 180–350 triage band.

> 💡 Interview Tip: If you only "finish files," you fail mocks. Every Sunday, one **timed** artifact: a problem, a 45-min design, a 45-min UI, or a STAR set.

> ⚠️ Pitfall: Spending week 6–8 rewriting notes. Notes are a byproduct. The tracker in [00](./00-README.md#progress-tracker) is the scoreboard.

---

## 8. Week-by-Week

**STAR cadence:** W1 impact · W2 ownership · W3 conflict · W4 failure · W5 ambiguity · W6 deadline · W7 mentor · W8 influence. Draft Sunday night, record once, do not polish for hours.

### Week 1 — JavaScript High + puzzles

| | |
|--|--|
| **Read/build** | [02](./02-javascript.md) High rows: execution, scope, closures, `this`, prototypes, event loop, promises, modules |
| **DSA** | Arrays + hashing (8–10 problems). Timer on. |
| **14** | 5/day from [Part 1](./14-js-logical-interview-questions-part1.md) then event-loop [Part 2](./14-js-logical-interview-questions-part2.md) |
| **15** | 90 s pitch v1 |
| **Done when** | You can walk a microtask vs macrotask example without looking |

### Week 2 — TypeScript + JS implementations

| | |
|--|--|
| **Read/build** | [03](./03-typescript.md) High: narrowing, generics you actually ship, `satisfies`, utility types you use. Finish 02 High leftovers (`bind`, iterator mental model). |
| **DSA** | Two pointers + window |
| **14** | Implement debounce, `promiseAll`, deep clone ([14 Part 3](./14-js-logical-interview-questions-part3.md)) |
| **15** | STAR **ownership** |
| **Done when** | You can type a small API client without `any` |

### Week 3 — React High + Medium

| | |
|--|--|
| **Read/build** | [04](./04-react.md) render, hooks, effects, state libraries, memo, a11y bar. One full [Part 3](./04-react-part3.md) component timed. |
| **DSA** | Stack + binsearch |
| **14** | 3 puzzles/day maintenance |
| **Mock 1** | 45 min medium + 15 min React "why did this re-render?" |
| **15** | STAR **conflict** |
| **Done when** | You can draw commit vs render vs paint and name when `memo` is wasted |

### Week 4 — Next.js High + Medium

| | |
|--|--|
| **Read/build** | [05](./05-nextjs.md) App Router, RSC, caching, data fetching, CWV as in that file. One route with loading/error. |
| **DSA** | Linked lists + start trees |
| **Mock 2** | 45–60 min **machine coding** (autocomplete or infinite scroll) |
| **15** | STAR **failure** |
| **Done when** | You can say what is cached, where, and what busts it |

### Week 5 — Node.js High + Medium

| | |
|--|--|
| **Read/build** | [06](./06-nodejs.md) libuv phases (don't recopy 02), HTTP servers, errors, auth tokens, Redis **as used** (Lua internals stay in 06 — don't re-derive). `/readyz`. |
| **DSA** | Trees |
| **Mock 3** | 45 min **API**: pagination + idempotent POST ([13 Part 4](./13-coding-round-practice-part4.md)) |
| **15** | STAR **ambiguity** |
| **Done when** | Access vs refresh location + rotation is a 4-minute talk |

### Week 6 — Databases, APIs, engineering High

| | |
|--|--|
| **Read/build** | [07](./07-databases-and-apis.md) indexes, isolation, REST, transactions. [08](./08-engineering-practices.md) **High only**: test pyramid, CI, OWASP **as listed** — no second security textbook. |
| **DSA** | Heap + graphs intro (BFS/DFS, islands) |
| **Mock 4** | 45 min **design**: rate limiter ([09](./09-system-design.md)) |
| **15** | STAR **deadline** |
| **Done when** | You can pick an index for "list my orders" and name the isolation you want for "place order" |

### Week 7 — System design High + Medium

| | |
|--|--|
| **Read/build** | [09](./09-system-design.md) framework, hashing, queues, feed, unique IDs. **Six** 45-min designs (reuse week-6 limiter). CAP as in 07/09 — don't invent a third copy. |
| **DSA** | Graphs + intro 1D DP |
| **15** | STAR **mentor**; 10 min project deep-dive |
| **Done when** | A stranger can follow your 45-min board: requirements → API → data → scale → failure |

### Week 8 — Cloud High skim, behavioral, dress rehearsal

| | |
|--|--|
| **Read/build** | [10](./10-deployment-aws-ec2.md)–[12](./12-cloudflare.md) **High rows only** (IMDSv2, ALB/ACM, S3+OAC, Full strict). [15](./15-other-interview-questions.md) remaining: questions-to-ask, negotiation **principles**, resume X/Y/Z. [17](./17-cheatsheets.md) when present. |
| **DSA** | Mixed timed set; no new patterns unless a mock exposed one |
| **Mock 5** | 90–120 min: coding + design **or** coding + behavioral |
| **15** | STAR **influence**; pitch v-final |
| **Done when** | [What "Ready" Means](./00-README.md#what-ready-means) is mostly ticked **without** notes |

---

## 9. Daily Shape (8-Week)

| Block | Time | Notes |
|------|:----:|-------|
| Topic | 3.5 h | Current week's files |
| DSA | **75–90 min** | 1 timed + 1 review/easier. This is how 150 gets **attempted**. |
| Drills | 25 min | Puzzles (W1–2) or STAR/pitch/UI (later) |
| Close | 15 min | 5 bullets |

Sunday: mock **or** 2 h weak-topic + rest. Do not start a new file on Sunday.

---

## 10. What You Skip

- **Low** rows in every syllabus table.
- AWS/Cloudflare **Medium/Low** (ASG tuning, advanced WAF, Workers/DO depth) unless the JD is infra.
- DSA: skip exotic DP until mocks demand it; greedy/tries if time dies.
- [08](./08-engineering-practices.md) Medium tooling wars (Biome vs ESLint essays).
- A "portfolio rewrite." If you need a story, **one** slice: existing app + one production-shaped change. Don't start a SaaS in week 6.

---

## 11. Re-Weight by JD

| JD signal | Steal hours from | Give hours to |
|-----------|------------------|---------------|
| Backend / platform | 04 machine extras | 07, 09, queues |
| Product / frontend | 10–12 High skim | 04, 05, CWV, a11y |
| "AWS required" | 08 Medium | 10 + 11 High **and** one Medium |
| "Cloudflare" in stack | 10 Medium | 12 High + Cache Rules |
| Staff-leaning | 14 extra puzzles | 15 staff vs IC, 09 trade-offs |

Never steal from **daily DSA** or **weekly STAR**.

---

## Next: Part 3

➡️ [Part 3 — 12-Week Plan](./16-study-plan-part3.md): full ~480 h path, mock scripts, <2-week emergency, interview questions about how you prepared.
