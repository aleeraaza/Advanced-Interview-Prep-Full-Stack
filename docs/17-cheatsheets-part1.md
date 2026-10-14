# 17 — Cheatsheets (Part 1 of 3): Language, React, Next.js

> **Parts:** **Part 1 — JS / TS / React / Next** · [Part 2 — Node / Data / Practices / Design](./17-cheatsheets-part2.md) · [Part 3 — Cloud, Coding, Behavioral, 48 h](./17-cheatsheets-part3.md)
>
> **Re-read, don't learn.** Canonical explanations: [02](./02-javascript.md)–[05](./05-nextjs.md). If a line here disagrees with a topic file, trust that file. Versions move — Next caching and React 19 APIs: verify on nextjs.org / react.dev.

## Table of Contents

- [1. Overview](#1-overview)
- [2. Topic Map](#2-topic-map)
- [3. How to Use These Sheets](#3-how-to-use-these-sheets)
- [4. JavaScript](#4-javascript)
- [5. TypeScript](#5-typescript)
- [6. React](#6-react)
- [7. Next.js](#7-nextjs)
- [Next: Part 2](#next-part-2)

---

## 1. Overview

Last **48 hours** and **< 40 h** triage ([01](./01-fullstack-syllabus.md#priority-triage-if-you-only-have-x-hours), [16 Part 3](./16-study-plan-part3.md#15-less-than-two-weeks)): tables you can recite. Not a substitute for never opening 02–06.

| Sheet | File | Recite in |
|-------|------|-----------|
| JS | [02](./02-javascript.md) | 8 min |
| TS | [03](./03-typescript.md) | 5 min |
| React | [04](./04-react.md) | 8 min |
| Next | [05](./05-nextjs.md) | 8 min |

> 💡 Interview Tip: Open every Next answer with **version + caching model**. Open every JS loop answer with **browser vs Node**.

> ⚠️ Pitfall: Memorizing this file then freezing on a follow-up. The follow-up lives in the linked part.

---

## 2. Topic Map

- [ ] Recite §4–§7 aloud once
- [ ] One puzzle set from [14](./14-js-logical-interview-questions.md) after JS
- [ ] Part 2 Node/DB/08/09
- [ ] Part 3 cloud + DSA + STAR + 48 h script

---

## 3. How to Use These Sheets

1. Cover the right-hand column; say it; uncover.
2. Miss → open the **canonical file**, not another YouTube.
3. After each sheet: **one** timed artifact (puzzle, component, design sketch).
4. Sleep beats a fourth pass.

---

## 4. JavaScript

Canonical: [02](./02-javascript.md). Puzzles: [14](./14-js-logical-interview-questions.md). Node phases: [06](./06-nodejs.md).

| Topic | Recite |
|-------|--------|
| Scope | EC = records + outer. `var` → `undefined`; fn → value; `let/const/class` → TDZ. Lexical. Top-level `let` ≠ `globalThis`. |
| Closures | Live bindings, not copies. `let` in `for` = per iteration. Closures retain what they close over. |
| `this` | `new` > `call/apply/bind` > `obj.method()` > default (`undefined` strict). Arrow = lexical. Extract loses. `bind` sticky; `new` beats `bind`. |
| Proto | Read walks `[[Prototype]]`; write = own. `extends`: instance chain **and** constructor chain. |
| Browser loop | One task → **all** microtasks → maybe render. Micro: then/`await`/`queueMicrotask`. Task: timers, events. Async body sync until first `await`. |
| Promises | Executor sync; `then` always async. `all` fail-fast; `allSettled` never rejects; `race` first settle; `any` first fulfill. `return await` in `try`. `forEach` doesn't await. |
| Coercion | `null == undefined` only. `null == 0` **false**; `null >= 0` **true**. `Object.is` for `NaN`/`-0` (React). |
| Clone | spread shallow < JSON lossy < `structuredClone` (no functions) < custom + cycles. |
| Modules | ESM live bindings, TLA; CJS copies. Cycles: CJS partial exports. |
| Render path | CSS blocks render; `defer` for app JS; batch reads then writes; animate `transform`/`opacity`. |

**Write in 10 min each:** `bind` (with `new`), `Promise.all`, debounce+cancel, `deepClone` with cycles — [14 Part 3](./14-js-logical-interview-questions-part3.md).

**Q43 order (Node/browser mix as in 14):** `1 5 7 3 4 6 2` — don't re-derive here; if blank, [14 Part 2](./14-js-logical-interview-questions-part2.md).

---

## 5. TypeScript

Canonical: [03](./03-typescript.md).

| Topic | Recite |
|-------|--------|
| Reality | Types **erased**. `tsc --noEmit` in CI. Zod at the edge. |
| Tops | `unknown` safe; `any` opt-out; `never` bottom. `void` callbacks accept any return. |
| Widen | `const` keeps literals; `as const` deep. Excess checks on **fresh** literals. |
| Narrow | `typeof` / `in` / equality / discriminants / `x is T`. Exhaust with `assertNever`. |
| Generics | Param ≥ 2 uses. `const T` (5.0); `NoInfer` (5.4). |
| Mapped | `{ [K in keyof T as …]-?: … }`; remap to `never` to drop keys. |
| Conditional | Distributes on **naked** `T`; `[T] extends [X]` to stop. `Omit` collapses unions — that's why. |
| Utils | `Omit = Pick<T, Exclude<keyof T, K>>`. `NonNullable = T & {}`. |
| Assert | annotation vs `as` (unchecked) vs `satisfies` (checked, keeps infer) vs `!`. |
| Privacy | `#` runtime; `private` compile-time. **No** constructor parameter properties on Node 24 type-strip (`ERR_UNSUPPORTED_TYPESCRIPT_SYNTAX`). |
| Config | `strict` + `nodenext` when Node runs JS; `bundler` + `noEmit` for Next/Vite. `paths` ≠ runtime. |
| React | `ComponentProps<"el">`, `useRef<T>(null)`, context `T \| undefined` + guard. Next 15+: `params` are Promises. |

**Write from memory:** `Pick`, `Partial`, `ReturnType`, `Awaited`, `DeepPartial`.

---

## 6. React

Canonical: [04](./04-react.md). Machine: [04 Part 3](./04-react-part3.md). RTL/a11y stay there.

| Topic | Recite |
|-------|--------|
| Pipeline | Trigger → **render** (pure) → **commit** (DOM, refs, layout effects) → paint → passive effects. |
| Re-render | Own state, context, parent render. Not "props changed" alone. Same-value `setState` bails. |
| Keys | Type + position + key. Bad index keys shuffle state. `key` remounts. |
| Effects | After paint; cleanup before re-run/unmount; `Object.is` deps. Strict: setup→cleanup→setup. Layout before passive; cleanups before setups; effects **bottom-up**. |
| Don't effect | Derive in render; events in handlers; reset with `key`. |
| Memo | Expensive work / child identity. Compiler first; manual when identity is a contract. |
| External | `useSyncExternalStore`. IDs: `useId`. |
| Concurrent | `useTransition` = update you own; `useDeferredValue` = value you receive. **Not** debounce. |
| Query | `staleTime` default 0; `gcTime` default 5 min. Keys + invalidate + optimistic + rollback. |
| RSC | Server default, serializable props, `"use client"` boundary. Server Functions: **auth + validate**. |
| Errors | Boundaries catch render/lifecycle/`use`/transition — **not** event handlers. |
| Perf order | Profiler → composition → memo/Compiler → split → virtualize → transitions. |
| A11y | Native + label + keyboard + focus + test **by role**. |

**60 min:** autocomplete **or** modal **or** infinite scroll — cut happy path first.

---

## 7. Next.js

Canonical: [05](./05-nextjs.md). CWV numbers live there; don't invent new thresholds.

| Topic | Recite |
|-------|--------|
| Model | App Router = RSC. `"use client"` = client **entry**. Donut: server wrap client. `server-only`. |
| Files | `layout` persists; `template` remounts; `loading` = Suspense; `error` + retry; `route` = handler. |
| Build glyphs | ○ static · ● SSG params · ◐ PPR · ƒ dynamic. |
| Fetch | Parallelize. `React.cache` per request vs `'use cache'` across. |
| Invalidate | `updateTag` (read-your-writes in actions) · `revalidateTag` SWR · `{ expire: 0 }` immediate · `revalidatePath` · `router.refresh()`. |
| Actions | Public POST. DAL + Zod + ownership + invalidate. 1 MB default. Bound args = client input. |
| Proxy | `proxy.ts` = redirects/headers, **not** auth. CVE-2025-29927: crafted header skipped middleware — checks in **DAL**. |
| Env | `NEXT_PUBLIC_` inlined at **build**. |
| Image/font | `sizes`; `remotePatterns`; `next/font` self-host. |
| CWV p75 | LCP ≤ 2.5 s · INP ≤ 200 ms · CLS ≤ 0.1. |
| Self-host | Encryption key, shared cache + tags, `deploymentId`, no buffering, SIGTERM, copy `public` + `.next/static`. |
| Streaming | First byte freezes status; late `notFound()` can be 200 + noindex. |

> ⚠️ Pitfall: Auth only in middleware/proxy/layout. Layouts don't re-run for every action; actions are public.

---

## Next: Part 2

➡️ [Part 2](./17-cheatsheets-part2.md) — Node, databases/APIs, engineering practices, system design.
