# 04 — React

> This topic is split into four parts. Start with Part 1 and follow the "Next" links. Applies to React 19 (19.x).

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Rendering, Reconciliation & Hooks](./04-react-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.13 Detailed Explanations | Trigger → render → commit, what causes re-renders, reconciliation and keys, Fiber and lanes, `useState` snapshots and batching, `useEffect` cleanup and races, "You Might Not Need an Effect", refs and layout effects, `useReducer`/`useContext`, `useMemo`/`useCallback`, `useId`/`useSyncExternalStore`/`useEffectEvent`, Rules of Hooks, custom hooks with tests |
| [Part 2 — State, Performance, React 19, Patterns & Testing](./04-react-part2.md) | 3.1–3.10 Detailed Explanations · 4. Diagrams Index | Choosing a state tool (Context, Redux Toolkit, Zustand, TanStack Query), Profiler/memo/Compiler/code splitting/virtualization, Suspense and transitions, Actions with `useActionState`/`useFormStatus`/`useOptimistic`/`use`, Server Components, React Hook Form + Zod, error boundaries, accessibility, component patterns, RTL + MSW testing |
| [Part 3 — Machine Coding Round](./04-react-part3.md) | 3.0 Strategy · 3.1–3.7 Builds · 3.8 More Builds · Test Setup | Time-boxing plan and seven complete, accessible, tested components: Autocomplete, Infinite Scroll, Modal, Star Rating, Todo App, compound Tabs, Pagination |
| [Part 4 — Resources, Practice, Interview Questions & Revision](./04-react-part4.md) | 6. Resources · 7. How to Learn It · 8. Hands-on Practice · 9. Interview Questions · 10. Common Mistakes · 11. Quick Revision | 26 curated resources, a ~42.5 h learning path, 10 graded exercises, 36 interview questions with model answers, red flags, one-page recap and last-day checklist |

> 💡 Interview Tip: All code in Parts 1–3 was type-checked under `strict` + `noUncheckedIndexedAccess`, and every test was run with Vitest + jsdom against React 19.3. Copy the [Test Setup](./04-react-part3.md#test-setup) to practice with the same harness.

## Related Files

- Closures, event loop and `this` behind hooks and handlers → [02-javascript.md](./02-javascript.md)
- Typing props, events, refs and generic components → [03-typescript Part 2](./03-typescript-part2.md#316-typing-react)
- Server Components, caching and Server Actions in a framework → [05-nextjs.md](./05-nextjs.md)
- Testing strategy, CI and accessibility tooling → [08-engineering-practices.md](./08-engineering-practices.md)
- More UI builds and DSA practice → [13-coding-round-practice.md](./13-coding-round-practice.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./04-react-part1.md), then continue to [05-nextjs.md](./05-nextjs.md).
