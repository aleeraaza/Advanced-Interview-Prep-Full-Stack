# 14 — JS Logical / Output Questions

> This topic is split into three parts. Start with Part 1. **108 output-prediction items** plus timed implementations. Theory is [02](./02-javascript.md) — do not re-learn the language here; predict, then check. Environment unless noted: **ES module / Node 24 / strict**. Browser sloppy-script and Node `process.nextTick` are labeled. Five puzzles per day from week 1 ([00](./00-README.md#recommended-study-order)). Coercion and event-loop snippets were checked on **Node 24.21** (October 2026).

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Closures, `this`, Prototypes](./14-js-logical-interview-questions-part1.md) | 1–3 · Q1–Q42 | How to drill; `var`/`let`/TDZ; four `this` rules; prototype chain |
| [Part 2 — Event Loop, Coercion, Oddballs](./14-js-logical-interview-questions-part2.md) | Q43–Q86 | Microtasks vs timers; ToPrimitive / `==`; freeze; generators; `typeof`; `0.1+0.2` |
| [Part 3 — Implementations, Interview](./14-js-logical-interview-questions-part3.md) | Q87–Q108 · §11–17 | Holes/JSON/Map; debounce, `Promise.all`, LRU, emitter, retry, pool; ~11 h path; 36 meta-questions |

> 💡 Interview Tip: Name the **rule** first (`CreatePerIterationEnvironment`, `new` beats `bind`, drain all microtasks). The numbers follow.

## Related Files

- Language internals → [02-javascript](./02-javascript.md)
- Node `nextTick` / libuv phases → [06-nodejs](./06-nodejs.md)
- DSA live coding → [13-coding-round-practice](./13-coding-round-practice.md)
- Typing curry/debounce → [03-typescript](./03-typescript.md)
- Compact revision → [17-cheatsheets](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./14-js-logical-interview-questions-part1.md), then continue to [15-other-interview-questions.md](./15-other-interview-questions.md).
