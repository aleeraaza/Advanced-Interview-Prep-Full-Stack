# 03 — TypeScript (Part 3 of 3): Resources, Practice, Interview Questions & Revision

> **Parts:** [Part 1 — Overview, Topic Map, Type System](./03-typescript-part1.md) · [Part 2 — tsconfig, Typing React/Node/Next, Zod & Code Examples](./03-typescript-part2.md) · **Part 3 — Resources, Practice, Interview Questions & Revision**

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
| Everything (official) | TypeScript Handbook | docs | typescriptlang.org/docs/handbook | Free | Authoritative; "Narrowing", "Generics", "Type Manipulation" chapters are essential |
| tsconfig | TSConfig Reference | docs | typescriptlang.org/tsconfig | Free | Every flag with examples and defaults |
| What changed when | TypeScript release notes | docs | typescriptlang.org/docs/handbook/release-notes | Free | Learn `satisfies` (4.9), `const` type params (5.0), `NoInfer` (5.4), inferred predicates (5.5), `erasableSyntaxOnly` (5.8)… |
| Experimentation | TypeScript Playground | tool | typescriptlang.org/play | Free | Hover types, test versions, share repros |
| Practical advanced TS | Total TypeScript — Matt Pocock (free tutorials, *Total TypeScript Essentials* book online, paid workshops) | course/book | totaltypescript.com | Free + Paid | Best practical material on generics, type transformations, React + TS |
| Practical advanced TS | Matt Pocock's YouTube channel | video | YouTube "Matt Pocock" | Free | Short, precise videos on individual features |
| Best practices | *Effective TypeScript* (2nd ed.) — Dan Vanderkam | book | O'Reilly / bookstores | Paid | 80+ items on how to *use* the type system well; strong on soundness |
| Type-level programming | *Type-Level TypeScript* — Gabriel Vergnaud | course | type-level-typescript.com | Free chapters + Paid | Teaches conditional/mapped/recursive types as a programming language |
| Type-level practice | type-challenges | repo | github.com/type-challenges/type-challenges | Free | Graded puzzles with community solutions |
| Deep reference | *TypeScript Deep Dive* — Basarat Ali Syed | book | basarat.gitbook.io/typescript | Free | Broad coverage, good on compiler internals and patterns |
| React + TS | React TypeScript Cheatsheet | docs | react-typescript-cheatsheet.netlify.app | Free | Community-maintained answers for props, hooks, events, generics |
| React + TS | react.dev "Using TypeScript" | docs | react.dev/learn/typescript | Free | Official React typing guidance |
| Next.js + TS | Next.js docs "TypeScript" | docs | nextjs.org/docs (Configuring → TypeScript) | Free | Current `params` typing, typed routes, plugin |
| Runtime validation | Zod documentation | docs | zod.dev | Free | Schemas, Zod 4 changes, JSON Schema |
| Runtime validation | Standard Schema | docs | standardschema.dev | Free | Shared interface across Zod, Valibot, ArkType |
| Package publishing | "Are the types wrong?" — Andrew Branch | tool | arethetypeswrong.github.io | Free | Diagnose ESM/CJS/types resolution issues in packages |
| Performance | TypeScript wiki "Performance" | docs | github.com/microsoft/TypeScript/wiki/Performance | Free | Official advice on slow type-checking, tracing |
| Video series | "No BS TS" — Jack Herrington | video | YouTube "Jack Herrington" | Free | Practical TS for React developers |
| Overview | Fireship "TypeScript in 100 seconds" & related | video | YouTube "Fireship" | Free | Quick orientation |

---

## 7. How to Learn It

Total: **~27 hours** (matches the [syllabus](./01-fullstack-syllabus.md#2-typescript)).

| Step | What to do | Time |
|------|-----------|:----:|
| **0. Self-assess** | Tick the [Topic Map](./03-typescript-part1.md#2-topic-map). Turn on `strict` + `noUncheckedIndexedAccess` in a real project and count errors — each category of error is a gap to study. | 1 h |
| **1. Read** | Handbook: Everyday Types, Narrowing, More on Functions, Object Types, Generics, Type Manipulation (all subpages). Then Part 1 of this doc. | 6 h |
| **2. Watch** | 4–6 Matt Pocock videos on generics, `satisfies`, `infer`, and React typing. | 2 h |
| **3. Build** | Exercises 1–5 below in a real repo (or a fresh Next.js + Express monorepo). | 8 h |
| **4. Practice — types** | type-challenges: all "Warm-up" and "Core" rows from [Part 2 §3.20](./03-typescript-part2.md#320-type-challenges-a-curated-path), without peeking. | 5 h |
| **5. Practice — questions** | Answer all [Interview Questions](#9-interview-questions) out loud; for each, write the code example in the Playground. | 3 h |
| **6. Revise** | [Quick Revision Summary](#11-quick-revision-summary) at +1 day, +1 week, and the day before. Re-implement `Pick`, `Omit`, `ReturnType`, `Awaited`, `DeepPartial` from memory. | 2 h |

```mermaid
flowchart LR
    A[Self-assess<br/>1 h] --> B[Handbook + Part 1<br/>6 h] --> C[Videos<br/>2 h] --> D[Build exercises<br/>8 h] --> E[type-challenges<br/>5 h] --> F[Interview Qs<br/>3 h] --> G[Revise<br/>2 h]
```

> 💡 Interview Tip: TS interviews are usually woven into coding rounds ("type this function", "make this component generic") rather than standalone. Practice typing as you code, out loud: "I'll make this generic over `T` so the callback gets the right item type."

---

## 8. Hands-on Practice

| # | Exercise | Level | Acceptance criteria |
|---|----------|:-----:|---------------------|
| 1 | **Strict migration** — take a JS or loosely-typed TS module (~500 lines) and migrate to `strict` + `noUncheckedIndexedAccess` | 🟢 Easy | Zero `any` (lint `@typescript-eslint/no-explicit-any` as error); zero non-null assertions without a comment; `tsc --noEmit` passes in CI. |
| 2 | **Utility types from scratch** — implement `MyPartial`, `MyRequired`, `MyReadonly`, `MyPick`, `MyOmit`, `MyRecord`, `MyExclude`, `MyExtract`, `MyReturnType`, `MyParameters`, `MyAwaited`, `MyNonNullable` | 🟢 Easy | Each has `Expect<Equal<…>>` tests against the built-in for ≥ 3 inputs, including a union and an optional property. |
| 3 | **Typed API layer** — Zod schemas shared by an Express 5 API and a React client | 🟡 Medium | `validateBody` middleware types `req.body` from the schema; client uses `apiGet(url, schema)` returning `Result`; changing a schema field produces compile errors on both sides; invalid payload returns 400 with issues. |
| 4 | **Env validation** for a Next.js app and a Node service | 🟢 Easy | App refuses to start with a missing/invalid var and prints which one; `env.PORT` is `number`; client-exposed vars are a separate schema limited to `NEXT_PUBLIC_*`. |
| 5 | **Generic React components** — `<Select<T>>`, `<DataTable<Row>>` with typed column definitions (`accessor: keyof Row` or `(row: Row) => ReactNode`), and a polymorphic `<Text as>` | 🟡 Medium | Column `accessor` autocompletes row keys; sorting callback receives `Row`; `<Text as="a">` accepts `href`, `<Text as="span">` rejects it. |
| 6 | **Discriminated-union state machine** — checkout flow (`cart → shipping → payment → review → done`, plus `error`) with a typed reducer and transition table | 🟡 Medium | Illegal transitions are compile errors (transition table typed with mapped types); `assertNever` in every switch; UI renders each state without optional chaining on fields that should exist. |
| 7 | **Typed router helpers** — `buildPath("/orgs/:orgId/projects/:projectId", params)` and `parseParams` | 🔴 Hard | Params type derived from the path literal via template literal types; missing/extra params are errors; tests for paths with 0, 1 and 3 params. |
| 8 | **`Paths<T>` + typed `get`/`set`** for a nested settings object (like React Hook Form's `register`) | 🔴 Hard | `get(obj, "a.b.c")` returns the exact type; invalid paths are errors; depth limited to avoid "excessively deep" errors on a 6-level object; editor autocomplete works. |
| 9 | **Publish a dual ESM/CJS typed package** | 🔴 Hard | `exports` with `types` conditions; passes "Are the types wrong?" with no problems; consumers with `moduleResolution: nodenext` and `bundler` both get types. |
| 10 | **type-challenges sprint** | 🟡 Medium | 13 warm-up + 18 core challenges solved; for 5 of them, write a 3-sentence explanation of *why* the solution works. |

---

## 9. Interview Questions

### Basic

#### Q1. Why use TypeScript? What are the costs?

**Model answer.** Benefits: catches whole classes of bugs before runtime (null/undefined, typos, wrong shapes), makes refactoring safe across large codebases, serves as always-up-to-date documentation, and powers editor tooling (autocomplete, go-to-definition, rename). Costs: a build/type-check step, learning curve, type definitions for untyped dependencies, and complex types that can hurt readability. The biggest trap is false confidence: types are erased, so external data must still be validated at runtime.

**Follow-ups:** How would you introduce TS into a JS codebase? When wouldn't you use it?

**Great answer includes:** Incremental adoption (`allowJs`, `checkJs`, strictness ratchet); runtime-validation caveat; concrete bug example from experience.

#### Q2. `interface` vs `type` — when do you use each?

**Model answer.** Both describe object shapes. Only `type` can express unions, tuples, primitives, mapped and conditional types. Only `interface` supports declaration merging (needed for augmenting libraries like Express's `Request` or `Window`). `interface extends` reports incompatible overrides as errors, whereas an intersection silently produces `never` for conflicting properties; interfaces also tend to be cached better by the checker. I default to `interface` for object shapes and props, `type` for everything else, and follow the codebase's convention.

**Follow-ups:** Show a case where `&` produces `never`. How does merging work?

**Great answer includes:** Merging use case; `extends` vs `&` conflict behavior; acknowledging it's mostly a style choice.

#### Q3. Explain `any`, `unknown`, and `never`.

**Model answer.** `unknown` is the top type: anything can be assigned to it, but you can't use it until you narrow it — the safe choice for untrusted values and `catch` variables. `any` disables type checking entirely in both directions and spreads to everything it touches. `never` is the bottom type: no value has it; it represents impossible code paths (functions that always throw, exhausted unions), and it vanishes from unions, which makes it the "filter" in conditional types.

**Follow-ups:** How do you test whether a type is `never`? Where does `never` show up unexpectedly?

**Great answer includes:** `[T] extends [never]`; `never` from impossible intersections and empty arrays (`never[]`); `assertNever` pattern.

#### Q4. What is structural typing? What are excess property checks?

**Model answer.** TypeScript compares types by their shape: an object is assignable to a type if it has at least the required properties with compatible types, regardless of declared names. Excess property checks are a special rule for *fresh object literals* assigned directly to a typed location: extra properties are flagged because they're almost always typos. Once the object is held in a variable, extra properties are allowed by structural rules.

**Follow-ups:** How do you get nominal typing when you need it? Why does `Object.keys` return `string[]`?

**Great answer includes:** Freshness; branded types for nominal behavior; the "open types" consequence for `Object.keys`.

#### Q5. Annotation vs `as` vs `satisfies`?

**Model answer.** An annotation (`const x: T = v`) checks `v` against `T` and makes `x` have type `T`, losing more specific information. An assertion (`v as T`) tells the compiler to treat `v` as `T` with only a weak overlap check — it's unchecked and can lie. `satisfies` (TS 4.9) checks `v` against `T` but keeps `v`'s inferred type, so you get validation *and* precise literal keys/values. I use `satisfies` for config objects and lookup tables, annotations for function parameters and public APIs, and assertions only at well-understood boundaries.

**Follow-ups:** Combine `as const` and `satisfies`. When is `as` unavoidable?

**Great answer includes:** A theme/config example showing lost keys with annotation; `as const satisfies`.

#### Q6. What's the difference between `prop?: string` and `prop: string | undefined`?

**Model answer.** `prop?: string` means the property may be absent (and, by default, may also be present with value `undefined`). `prop: string | undefined` means the property must be present, though its value may be `undefined`. With `exactOptionalPropertyTypes`, `prop?: string` no longer accepts an explicit `undefined`, which matters for code that distinguishes "not provided" from "cleared" (e.g. PATCH payloads where `undefined` vs missing means different things).

**Follow-ups:** How does this interact with spreading objects? With `in` checks?

**Great answer includes:** `exactOptionalPropertyTypes`; PATCH semantics; `"prop" in obj` vs `obj.prop !== undefined`.

#### Q7. Enums vs union types — which do you prefer?

**Model answer.** Unions of string literals are zero-cost, structural, and work naturally with API data. When I also need a runtime list of values (dropdowns, validation), an `as const` object plus a derived union gives both. TS `enum`s generate runtime code, numeric enums have reverse mappings and historically loose assignability, string enums are nominal (a matching string literal isn't assignable), and `const enum` breaks under `isolatedModules`. Node's type stripping and `erasableSyntaxOnly` also reject enums. So I avoid enums in new code unless the codebase standardizes on them.

**Follow-ups:** How do you iterate an enum? How would you validate a union at runtime?

**Great answer includes:** `as const` object pattern; `z.enum`; isolatedModules/erasable syntax concerns.

#### Q8. What are generics? Give a non-trivial example.

**Model answer.** Generics are type parameters that let code work over many types while preserving relationships between inputs and outputs. Example: `groupBy<T, K extends PropertyKey>(items: T[], getKey: (item: T) => K): Record<K, T[]>` — `T` connects the items to the callback parameter and the output arrays, `K` captures the exact key union. Constraints (`extends`) restrict what can be passed and enable member access.

**Follow-ups:** When are generics unnecessary? Why can't TS infer a type parameter from the return type? What's `NoInfer`?

**Great answer includes:** "A type parameter should appear at least twice"; return-type-only generics as disguised assertions; `const` type parameters.

### Intermediate

#### Q9. How does narrowing work? Write a custom type guard.

**Model answer.** Control-flow analysis tracks a variable's type through branches. `typeof`, `instanceof`, `in`, equality checks, truthiness, `Array.isArray`, and discriminant checks narrow unions. Custom guards return `value is T` and narrow at call sites; assertion functions (`asserts value is T`) narrow everything after the call. Since TS 5.5, simple arrow predicates are inferred (e.g. `filter((x) => x !== undefined)`). A custom guard is a promise to the compiler, so it must be correct — for complex shapes I'd use a schema's `safeParse` instead.

**Follow-ups:** Why doesn't narrowing persist into a callback for a `let`? Why doesn't `filter(Boolean)` narrow?

**Great answer includes:** Guard vs assertion function; inferred predicates; the "guards can lie" caveat.

#### Q10. What are discriminated unions and why are they useful?

**Model answer.** A union of object types sharing a literal-typed tag property. Checking the tag narrows to one member, so each state only exposes the fields valid in that state. They make impossible states unrepresentable (vs. multiple booleans and optional fields), and with an `assertNever` default, adding a new member produces compile errors everywhere it isn't handled. They're ideal for request state, reducer actions, events, and API responses.

**Follow-ups:** How do you get exhaustiveness without a default case? How do you validate one at runtime?

**Great answer includes:** Before/after example with booleans; `assertNever`; `z.discriminatedUnion`.

#### Q11. Implement `Pick`, `Omit` and `Partial`.

**Model answer.**

```ts
type MyPartial<T> = { [K in keyof T]?: T[K] };
type MyPick<T, K extends keyof T> = { [P in K]: T[P] };
type MyOmit<T, K extends PropertyKey> = MyPick<T, Exclude<keyof T, K>>;
```

`Partial` maps over `keyof T` adding `?`; `Pick` maps over the chosen keys; `Omit` picks the keys that remain after excluding. Note the built-in `Omit`'s `K` is constrained to `keyof any`, not `keyof T`, so it accepts keys that don't exist — a common source of silent typos; some teams define a `StrictOmit`.

**Follow-ups:** Why does `Omit` collapse unions? Write `DeepPartial`.

**Great answer includes:** The `keyof any` constraint quirk; distributive variant.

#### Q12. Explain `keyof`, `typeof`, and indexed access types.

**Model answer.** `keyof T` is the union of `T`'s property keys. Type-level `typeof x` gets the type of a *value* (e.g. `typeof config`). Indexed access `T[K]` gets a property's type; `T[number]` gets element types of arrays/tuples. Combined: `(typeof ROLES)[number]` turns a `const` array into a union; `keyof typeof ORDER_STATUS` gets an object's keys; `T[keyof T]` gets a union of all value types.

**Follow-ups:** What's `keyof` of a union vs an intersection? Of a type with an index signature?

**Great answer includes:** `keyof (A | B)` = common keys; `keyof (A & B)` = all keys; `keyof { [k: string]: X }` = `string | number`.

#### Q13. How do you type React components, events, refs and generic components?

**Model answer.** Props as an interface (often extending `ComponentProps<"button">` to inherit native props); `children: ReactNode`. Inline handlers are contextually typed; extracted ones use `ChangeEvent<HTMLInputElement>` etc. `useRef<HTMLInputElement>(null)` for DOM refs (React 19 types make it `RefObject<HTMLInputElement | null>`), `useState<T | null>(null)` when the initial value is narrower. Context typed as `T | undefined` with a guarded custom hook. Generic components are regular generic functions — `function Select<T>(props: SelectProps<T>)` — so `T` is inferred from `options` and flows into `onChange`.

**Follow-ups:** How do you build a polymorphic `as` prop? Why avoid `React.FC` for generic components?

**Great answer includes:** `ComponentProps` reuse; context-without-default pattern; React 19 ref-as-prop.

#### Q14. How do you add `req.user` to Express's `Request` type?

**Model answer.** Module augmentation: in a `.d.ts` (or any module), `import "express"` then `declare module "express-serve-static-core" { interface Request { user?: AuthUser } }`. Interface merging adds the property to every `Request`. It's optional because only authenticated routes set it; handlers check `if (!req.user)` or a `requireAuth` middleware narrows by convention. The file must be included by tsconfig and be a module (have an import/export).

**Follow-ups:** How would you make `user` non-optional for protected routes only? How do you type `req.body` from a schema?

**Great answer includes:** Module vs script `.d.ts` pitfall; typed `RequestHandler<Params, ResBody, ReqBody, Query>` generics; schema-driven body typing.

#### Q15. Which tsconfig flags do you always enable and why?

**Model answer.** `strict` (null checks, implicit any, function types, catch variables as `unknown`…), `noUncheckedIndexedAccess` (array/record lookups include `undefined`), `noImplicitOverride`, `noFallthroughCasesInSwitch`, `isolatedModules` and `verbatimModuleSyntax` (compatibility with single-file transpilers and explicit `import type`), `skipLibCheck` for speed. Module settings depend on the runtime: `nodenext` for Node-run output, `bundler` + `noEmit` for Next/Vite. I'd consider `exactOptionalPropertyTypes` for new codebases.

**Follow-ups:** What does `skipLibCheck` risk? Difference between `target` and `lib`?

**Great answer includes:** Reasoning per flag; `lib` affects types only (no polyfills).

#### Q16. Why do you need runtime validation if you use TypeScript?

**Model answer.** Types are erased at compile time; nothing checks that `req.body` or `await res.json()` matches the annotation. An `as User` cast just moves the crash deeper into the code, where it's harder to debug — or silently corrupts data. Schemas (Zod, Valibot) validate at trust boundaries and infer the static type from the same definition, so there's one source of truth. Validate HTTP input, env vars, form data, third-party responses, webhooks, and `JSON.parse` output.

**Follow-ups:** Where *don't* you validate? `z.input` vs `z.output`? Performance concerns?

**Great answer includes:** Trust-boundary framing; "parse, don't validate" (return typed data); fail fast for env at startup.

#### Q17. How do `.d.ts` files and `@types` work? How do you type an untyped package?

**Model answer.** Declaration files describe the types of JS code without implementations. Packages either ship their own (`"types"` in package.json / `exports` conditions) or have community types on DefinitelyTyped installed as `@types/pkg`. For an untyped package, write `declare module "legacy-lib" { export function parse(input: string): Result; }` in a `.d.ts` file included by tsconfig, or as a last resort `declare module "legacy-lib";` (everything `any`). Global types come from `declare global` or script-style `.d.ts` files.

**Follow-ups:** Why might types resolve in one consumer but not another? (ESM/CJS conditions — "Are the types wrong?")

**Great answer includes:** Script vs module `.d.ts`; `types` condition ordering in `exports`.

### Advanced

#### Q18. Explain conditional types and distribution.

**Model answer.** `T extends U ? X : Y` picks a branch by assignability. When `T` is a naked type parameter instantiated with a union, the conditional distributes — it's evaluated per member and the results are unioned. That's how `Exclude<U, E> = U extends E ? never : U` filters unions. Wrapping both sides in a tuple (`[T] extends [U]`) disables distribution. `never` is the empty union, so distributive conditionals over `never` produce `never` — hence `[T] extends [never]` to detect it. Conditionals on unresolved generics are deferred, which is why you often can't return such a type from a generic function without overloads or casts.

**Follow-ups:** Write `IsNever`. Why does `ToArray<string | number>` give `string[] | number[]`?

**Great answer includes:** Naked parameter rule; tuple wrapping; `never` behavior; deferred evaluation.

#### Q19. What does `infer` do? Implement `ReturnType` and `Awaited`.

**Model answer.** `infer X` introduces a type variable inside an `extends` clause that TS fills in by pattern-matching.

```ts
type MyReturnType<F> = F extends (...args: any[]) => infer R ? R : never;
type MyAwaited<T> = T extends PromiseLike<infer V> ? MyAwaited<V> : T;
```

The real `Awaited` also handles `null`/`undefined` and thenables whose `then` has non-standard signatures. `infer` can be constrained (`infer S extends string`) and used in template literals to parse strings (`` `${infer Head}.${infer Rest}` ``).

**Follow-ups:** Extract the element type of an array; route params from a path string.

**Great answer includes:** Recursion; constrained `infer`; template literal parsing.

#### Q20. How do mapped types with key remapping work?

**Model answer.** `{ [K in keyof T as NewKey]: … }` iterates keys and lets you rename them (`` `get${Capitalize<K & string>}` ``) or drop them by mapping to `never`. Homomorphic mapped types (over `keyof T`) preserve `readonly`/optional modifiers and arrays/tuples; `-readonly` and `-?` remove modifiers. Uses: generating getters/handlers, `PickByValue`, converting event unions to handler maps, making API DTOs from models.

**Follow-ups:** Why `K & string`? What does `as` do to homomorphism?

**Great answer includes:** Filtering with `never`; modifier removal; `keyof` can include `number | symbol`.

#### Q21. What is variance, and why are method parameters bivariant?

**Model answer.** Variance describes how `Box<Sub>` relates to `Box<Super>`. Return types are covariant; parameters are contravariant under `strictFunctionTypes` (a handler for `Animal` can be used where a handler for `Dog` is expected, not vice versa). Mutable properties are effectively invariant (TS checks them covariantly, which is unsound). Method-shorthand parameters remain bivariant even in strict mode, so that common types like `Array<T>` (whose methods take `T`) stay assignable (`Dog[]` to `Animal[]`). Declaring callbacks as function-typed properties (`onChange: (v: T) => void`) gets stricter checking. TS 4.7 added `in`/`out` annotations.

**Follow-ups:** Show the unsoundness of covariant arrays.

**Great answer includes:** Concrete Dog/Animal example; property vs method syntax difference; array covariance hole.

#### Q22. `moduleResolution: bundler` vs `nodenext` — and what do `isolatedModules` and `verbatimModuleSyntax` do?

**Model answer.** `nodenext` models Node's real rules: each file is ESM or CJS based on extension and package `"type"`, relative ESM imports need file extensions (`./db.js`), and package `exports` conditions are respected. Use it when Node runs the emitted JS. `bundler` models bundlers: `exports` respected, extensionless imports allowed, no per-file format rules — use it with Vite/Next/webpack, usually with `noEmit`. `isolatedModules` errors on code that a per-file transpiler can't compile correctly (e.g. re-exporting a type without `export type`). `verbatimModuleSyntax` makes import elision explicit: only imports marked `type` are removed, so you must write `import type`, which avoids accidental side-effect imports or runtime imports of type-only modules.

**Follow-ups:** Why does Node complain about `ERR_MODULE_NOT_FOUND` for extensionless imports? How do `paths` aliases work at runtime?

**Great answer includes:** Who resolves imports at runtime determines the setting; `paths` don't rewrite output.

#### Q23. What are branded types and when would you use them?

**Model answer.** A brand intersects a base type with a unique phantom property (`string & { readonly [brand]: "UserId" }`) to emulate nominal typing at zero runtime cost. They prevent mixing structurally identical values — `UserId` vs `OrderId`, `Cents` vs `Dollars`, sanitized vs raw HTML, validated email vs any string. Values are created only through a validating constructor function (or `z.string().brand<"UserId">()`), so holding a branded value proves it was validated.

**Follow-ups:** Downsides? (Casting at creation, serialization loses brands, friction with libraries.)

**Great answer includes:** "Parse, don't validate" connection; money units example.

#### Q24. Give a real use of template literal types.

**Model answer.** Typed routing: `RouteParams<"/orgs/:orgId/projects/:projectId">` parses the string with `infer` to produce `{ orgId: string; projectId: string }`, so `buildPath(path, params)` rejects missing params. Others: i18n keys (`` `${Namespace}.${Key}` ``), CSS units (`` `${number}px` ``), event handler names (`` `on${Capitalize<Event>}` ``), and dotted object paths for form libraries. Watch out for cross-product explosions with large unions.

**Follow-ups:** Implement `Split<S, D>`. How do libraries like tRPC or Next typed routes do this?

**Great answer includes:** Working parser example; compile-time cost caveat.

#### Q25. Type-checking is slow in a large codebase. How do you diagnose and fix it?

**Model answer.** Measure first: `tsc --extendedDiagnostics` (check time, instantiation counts) and `tsc --generateTrace` (open in a trace viewer to find hot files/types). Common fixes: project references with `composite` + `tsc -b` to check packages incrementally; `incremental`; `skipLibCheck`; explicit return types on exported functions; prefer `interface extends` over large intersections; avoid huge unions and deeply recursive conditional/template types; split giant generated types; limit `include` globs and `types`. Also ensure the editor uses the workspace TS version.

**Follow-ups:** What makes a type expensive? Effect of the upcoming native compiler?

**Great answer includes:** Tooling names; concrete type-level culprits; the native (Go) compiler as a future speedup — verify current status.

### Tricky

#### Q26. Why does `Object.keys(obj)` return `string[]` instead of `(keyof typeof obj)[]`?

**Answer.** Object types are open: a value of type `{ a: number }` may have more properties at runtime (structural typing allows it). Promising `("a")[]` would be unsound. When you control the object's creation (e.g. an `as const` literal), a typed helper with a cast is acceptable.

**Great answer includes:** Concrete example where an extra key exists at runtime; the typed helper with a clear comment.

#### Q27. Why does `Omit<A | B, "id">` lose properties specific to `A` or `B`?

**Answer.** `Omit<T, K>` is `Pick<T, Exclude<keyof T, K>>`. `keyof (A | B)` is only the keys common to both members, and `Pick` over a union isn't distributive, so the result is a single object with the common keys. Fix with a distributive conditional: `type DistributiveOmit<T, K extends PropertyKey> = T extends unknown ? Omit<T, K> : never`.

**Great answer includes:** `keyof` of a union = intersection of key sets; naked-parameter distribution as the fix.

#### Q28. What's the difference between `{}`, `object`, `Object`, and `unknown`?

**Answer.** `unknown` accepts everything including `null`/`undefined`. `{}` means "any non-nullish value" — primitives like `"hi"` and `42` are assignable (it's not "empty object"). `object` means any non-primitive (objects, arrays, functions). `Object` (capital) is the interface of `Object.prototype`; it behaves like `{}` and is almost never what you want. For "a plain record", use `Record<string, unknown>`.

**Great answer includes:** `{}` accepting primitives; `NonNullable<T> = T & {}`; lint rules banning `{}`/`Object`.

#### Q29. Why does this compile?

```ts
function runAll(tasks: Array<() => void>) { tasks.forEach((t) => t()); }
runAll([() => 42, () => "done"]);
```

**Answer.** A function type with a `void` return accepts functions returning anything — `void` means "the return value will be ignored", not "must return undefined". This substitutability is deliberate so callbacks like `arr.forEach((x) => list.push(x))` work. In contrast, a function *declaration* annotated `(): void` can't `return 42`.

**Great answer includes:** Contextual vs declared `void`; why `undefined` as a return type is stricter.

#### Q30. Why doesn't `items.filter(Boolean)` narrow `(T | undefined)[]` to `T[]`?

**Answer.** `Boolean` is a constructor typed as `(value?: unknown) => boolean`, not a type predicate, so `filter`'s predicate overload isn't selected. TS 5.5's inferred type predicates apply to functions whose bodies TS can analyze (like `(x) => x !== undefined`), not to `Boolean`. Use `filter((x): x is T => x != null)` or `filter((x) => x !== undefined)` in 5.5+. Also note `Boolean` removes `0` and `""`, which may be a bug.

**Great answer includes:** Predicate overload of `filter`; 5.5 inference scope; falsy-value pitfall.

#### Q31. Why is `const user = {} as User` allowed, and why is it dangerous?

**Answer.** `as` permits conversions between types where one is assignable to the other; `{}` and `User` are "comparable" (`User` is assignable to `{}`), so the assertion is accepted. The result claims to have every `User` field while having none — a runtime `undefined` waiting to happen. Prefer building the full object, `Partial<User>` during construction, or validation. `x as unknown as T` (double assertion) bypasses even the comparability check and should be treated as a code smell.

**Great answer includes:** Comparability rule; safe alternatives; lint rule `consistent-type-assertions`.

#### Q32. A teammate wrote `function parse<T>(json: string): T { return JSON.parse(json); }`. What's wrong?

**Answer.** `T` appears only in the return position, so callers choose `T` freely and the function performs an unchecked cast — it looks type-safe but validates nothing. `JSON.parse` returns `any`, which also silences errors. Better: `function parse<S extends z.ZodType>(json: string, schema: S): z.output<S>` (the type is inferred *and* enforced), or return `unknown` and force callers to narrow.

**Great answer includes:** "Return-only generic = disguised assertion"; schema-based alternative; `any` leakage from `JSON.parse`/`res.json()`.

---

## 10. Common Mistakes & Red Flags

| Red flag | Why it hurts | Do instead |
|----------|-------------|-----------|
| `as` everywhere, especially `as unknown as T` | Turns the checker off where bugs live | Narrow with guards or parse with schemas |
| `any` to "make it compile" | Spreads silently; hides real errors | `unknown` + narrowing; `// @ts-expect-error` with a reason for genuine gaps |
| Typing API responses with interfaces only | Runtime data can differ; crashes far from the cause | Zod/Valibot at the boundary |
| Multiple booleans for state (`isLoading`, `isError`, `data?`) | Impossible states compile | Discriminated unions |
| Non-null assertions `!` on values that can actually be null | Converts compile errors into runtime crashes | Guards, early returns, or fix the type at the source |
| Over-engineered type-level code in app code | Unreadable, slow to check, hard to change | Simple types first; type magic only in shared libraries with tests |
| Generics that appear once | Noise, or disguised assertions | `unknown`, or tie input to output |
| Not knowing what your tsconfig does | Can't debug module/resolution issues | Explain every flag in your project's config |
| Thinking `private` is runtime privacy | Security/encapsulation misconceptions | `#private` for runtime privacy |
| Using `enum` without knowing the trade-offs | Interop and tooling friction | Union literals / `as const` objects |
| Assuming the bundler type-checks | Type errors ship to production | `tsc --noEmit` in CI |
| `@ts-ignore` instead of `@ts-expect-error` | Ignore comments rot silently when the error disappears | `@ts-expect-error` (fails when no longer needed) |

---

## 11. Quick Revision Summary

### One-page recap

**Foundations**
- Types are **erased**; bundlers strip types without checking → run `tsc --noEmit` in CI; validate runtime data.
- **Structural** typing; excess property checks only on fresh literals. Brands for nominal behavior.
- `const` keeps literals; `let`/object props widen; `as const` freezes literals deeply.
- `unknown` (safe top) vs `any` (opt-out) vs `never` (bottom, vanishes in unions). `void` callbacks accept any return.

**Narrowing & modeling**
- `typeof` / `instanceof` / `in` / equality / truthiness / `Array.isArray` / discriminants / `x is T` / `asserts x is T`; 5.5 infers simple predicates.
- Discriminated unions + `assertNever` = exhaustive, impossible states unrepresentable.

**Generics**
- Tie inputs to outputs; constrain with `extends`; type param should appear ≥ 2 times; return-only generics are casts.
- `const T` for literal inference (5.0); `NoInfer<T>` (5.4).

**Type manipulation**
- `keyof`, `typeof`, `T[K]`, `T[number]`.
- Mapped: `{ [K in keyof T as …]-?: … }`; filter by remapping to `never`.
- Conditional: distributive over naked type params; `[T] extends [X]` to stop it; `infer` (with `extends` constraints) to pattern-match; recursion for deep/path types.
- Template literals: cross products, parsing with `infer`; watch performance.
- Utility one-liners: `Partial`, `Required`, `Readonly`, `Pick`, `Omit = Pick<T, Exclude<keyof T, K>>`, `Record`, `Exclude`, `Extract`, `NonNullable = T & {}`, `ReturnType`, `Parameters`, `Awaited`.

**Assertions**
- Annotation (type = T) · `as` (unchecked) · `satisfies` (checked, keeps inferred type) · `!` (unchecked non-null).

**Functions, classes, variance**
- Overloads for input-dependent returns. Params contravariant (function-property syntax), methods bivariant.
- `#private` = runtime privacy; `private` = compile-time. Avoid `enum` / parameter properties if using erasable-syntax-only tooling.

**Config**
- `strict` + `noUncheckedIndexedAccess` + `noImplicitOverride`; `isolatedModules` + `verbatimModuleSyntax`; `skipLibCheck`.
- `nodenext` when Node runs output; `bundler` + `noEmit` for Next/Vite. `lib` ≠ polyfills. `paths` ≠ runtime aliases.

**Applied**
- React: `ComponentProps<"el">`, `ReactNode`, contextual event types, `useRef<T>(null)`, context `T | undefined` + guarded hook, generic components as generic functions.
- Express: augment `express-serve-static-core` `Request`; `RequestHandler<P, Res, Body, Query>`; schema-driven `req.body`.
- Next 15+: `params`/`searchParams` are Promises; Server Action state as a discriminated union; validate `FormData`.
- Zod 4: `z.infer`/`z.output` vs `z.input`, `safeParse`, `discriminatedUnion`, `coerce`, `brand`, `z.flattenError`.

### Last-day checklist

- [ ] I can implement `Pick`, `Omit`, `Partial`, `ReturnType`, `Awaited`, and `DeepPartial` from memory.
- [ ] I can explain distributive conditional types and why `Omit` collapses unions.
- [ ] I can explain `any` vs `unknown` vs `never` and `annotation` vs `as` vs `satisfies` with examples.
- [ ] I can model a request/checkout state as a discriminated union with exhaustive handling.
- [ ] I can type a generic `<Select<T>>` component and a polymorphic `as` prop.
- [ ] I can augment Express's `Request` and type `process.env` — and explain why env still needs Zod.
- [ ] I can explain each line of a Node ESM tsconfig and a Next.js tsconfig.
- [ ] I can say why `Object.keys` returns `string[]` and why `filter(Boolean)` doesn't narrow.

---

## Next Steps

- Update your TypeScript row in the [Progress Tracker](./00-README.md#progress-tracker).
- Keep 2–3 type-challenges per week in rotation until the interview.
- ➡️ Continue to [04-react.md](./04-react.md)
