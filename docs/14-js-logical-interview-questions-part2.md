# 14 — JS Logical Questions (Part 2 of 3): Event Loop, Coercion & Oddballs

> **Parts:** [Part 1 — Closures, `this`, Prototypes](./14-js-logical-interview-questions-part1.md) · **Part 2 — Event Loop, Coercion, Oddballs** · [Part 3 — Implementations, Interview](./14-js-logical-interview-questions-part3.md)
>
> Draw the queues. Coercion: name **ToPrimitive / ToNumber**, don't memorize memes. Theory: [02 §3.7–3.10](./02-javascript-part1.md#37-the-event-loop-browser), [02 §3.11](./02-javascript-part2.md#311-iterators--generators). **Node extra:** `process.nextTick` drains **before** promise microtasks ([06](./06-nodejs.md)) — only use that when the prompt is Node. Verified on **Node 24.21** (October 2026) for the snippets below.

## Table of Contents

- [7. Event Loop — Q43–Q56](#7-event-loop--q43q56)
- [8. Coercion & Equality — Q57–Q72](#8-coercion--equality--q57q72)
- [9. Descriptors, Freeze, Generators, `typeof`, Precision — Q73–Q86](#9-descriptors-freeze-generators-typeof-precision--q73q86)
- [Next: Part 3](#next-part-3)

---

## 7. Event Loop — Q43–Q56

**Q43 — the standard mix**
```js
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
queueMicrotask(() => console.log(4));
(async () => {
  console.log(5);
  await null;
  console.log(6);
})();
console.log(7);
```
> **Prints:** `1 5 7 3 4 6 2`  
> **Why:** sync `1,5,7`; async body until `await`; then all microtasks (`then`, `queueMicrotask`, await continuation); then the timer task. Same as [02](./02-javascript-part1.md#37-the-event-loop-browser).

**Q44 — nested `then` vs already-queued microtask**
```js
Promise.resolve().then(() => {
  console.log("a");
  Promise.resolve().then(() => console.log("b"));
});
queueMicrotask(() => console.log("c"));
```
> **Prints:** `a c b`  
> **Why:** queue is `[a, c]`; `a` enqueues `b` at the **end**.

**Q45 — timer then microtask**
```js
setTimeout(() => {
  console.log("t");
  Promise.resolve().then(() => console.log("m"));
}, 0);
```
> **Prints:** `t m`  
> **Why:** after the timeout **task**, a checkpoint drains `m` before the next task.

**Q46 — `await` of a value**
```js
async function f() {
  console.log("in");
  const v = await 1;
  console.log(v);
}
f();
console.log("out");
```
> **Prints:** `in` `out` `1`  
> **Why:** `await 1` ≡ `Promise.resolve(1)` then continuation as a microtask.

**Q47 — rejected promise, no catch (sync throw vs reject)**
```js
Promise.reject("x").then(() => console.log("ok"));
console.log("sync");
```
> **Prints:** `sync`, then an **unhandled rejection** (`ok` never runs). `.then` only handles fulfill; use `.catch` / second `then` arg.

**Q48 — `finally`**
```js
Promise.resolve(1)
  .finally(() => { console.log("f"); return 99; })
  .then((v) => console.log(v));
```
> **Prints:** `f` `1`  
> **Why:** `finally` fulfillment value is ignored unless it throws / returns a rejected promise.

**Q49 — `then` returns a promise**
```js
Promise.resolve(1)
  .then((v) => Promise.resolve(v + 1))
  .then(console.log);
```
> **Prints:** `2` (adoption / unwrap).

**Q50 — `async` + `forEach`**
```js
const sleep = () => Promise.resolve();
async function run() {
  [1, 2].forEach(async () => { await sleep(); console.log("x"); });
  console.log("done");
}
run();
```
> **Prints:** `done` then `x` `x`  
> **Why:** `forEach` does not await. Sequential: `for...of` + `await`.

**Q51 — two `setTimeout(0)`**
```js
setTimeout(() => console.log("a"), 0);
setTimeout(() => console.log("b"), 0);
```
> **Prints:** `a b` (FIFO tasks, same delay).

**Q52 — microtask starvation (conceptual)**
```js
function spin() {
  Promise.resolve().then(spin);
}
spin();
```
> **Prints:** never paints, never runs timers. Microtask checkpoint never ends. Yield with a **task** (`setTimeout` / `scheduler.yield()`).

**Q53 — `Promise.all([])`**
```js
Promise.all([]).then((v) => console.log(v));
console.log("s");
```
> **Prints:** `s` then `[]` (already-settled, still a microtask).

**Q54 — Node only: `nextTick` vs `then`**
```js
Promise.resolve().then(() => console.log("p"));
process.nextTick(() => console.log("n"));
```
> **Prints (Node):** `n` `p`  
> **Why:** nextTick queue runs before promise jobs ([06](./06-nodejs.md)). **Not** in the browser.

**Q55 — `return await` in `try`**
```js
async function a() {
  try { return Promise.reject("e"); }
  catch { return "caught"; }
}
async function b() {
  try { return await Promise.reject("e"); }
  catch { return "caught"; }
}
a().then((v) => console.log("a", v), (e) => console.log("a", e));
b().then((v) => console.log("b", v), (e) => console.log("b", e));
```
> **Prints:** `a e` (reject path) and `b caught` (fulfill). Don't bet on which microtask runs first.  
> **Why:** `return promise` skips `try/catch`; `return await` unwraps inside `try`.

**Q56 — `Promise.race` already settled**
```js
const p = Promise.resolve("fast");
Promise.race([p, new Promise(() => {})]).then(console.log);
```
> **Prints:** `fast`

---

## 8. Coercion & Equality — Q57–Q72

Walk ToPrimitive ([02 §3.10](./02-javascript-part1.md#310-type-coercion--equality)).

**Q57** `[] + []` → `""` (both `toString` to `""`).

**Q58** `[] + {}` → `"[object Object]"`.

**Q59 — statement vs expression**
```js
({} + []); // expression
```
> **Prints:** `"[object Object]"`  
> As a **statement**, `{}` is an empty **block**, then `+[]` → `0`. Always wrap objects in parens in the pad.

**Q60** `1 + "2"` → `"12"` (`+` concatenates if either side is string after ToPrimitive).

**Q61** `"3" * "4"` → `12` (`*` is always numeric).

**Q62** `[] == false` → `true` (`false` → `0`; `[]` → `""` → `0`).

**Q63** `[0] == false` → `true` (`[0]` → `"0"` → `0`).

**Q64** `null == 0` → `false` (`null` only `== undefined`).

**Q65** `null >= 0` → `true` (relational uses `ToNumber(null) === 0`).

**Q66** `NaN === NaN` → `false`; `Object.is(NaN, NaN)` → `true`.

**Q67** `Object.is(0, -0)` → `false`; `0 === -0` → `true`.

**Q68** `[1] == 1` → `true`.

**Q69** `"" == 0` → `true`.

**Q70** `[null] == 0` → `true` (`[null].toString()` is `""`).

**Q71** `[] == ![]` → `true` (`![]` is `false`; then Q62).

**Q72** `!!new Boolean(false)` → `true` (objects are truthy, even `new Boolean(false)`). Use `=== false` or unbox `.valueOf()`.

---

## 9. Descriptors, Freeze, Generators, `typeof`, Precision — Q73–Q86

**Q73 — `freeze` own assign (strict)**
```js
const o = { n: 1 };
Object.freeze(o);
o.n = 2;
```
> **Throws:** `TypeError` in a module. Sloppy script: silent no-op. `o.n` stays `1`.

**Q74 — freeze is shallow**
```js
const o = { a: { x: 1 } };
Object.freeze(o);
o.a.x = 9;
console.log(o.a.x);
```
> **Prints:** `9`

**Q75 — `defineProperty` non-writable**
```js
const o = {};
Object.defineProperty(o, "x", { value: 1, writable: false, enumerable: true });
o.x = 2;
console.log(o.x);
```
> **Throws** in strict; value stays `1`.

**Q76 — getter vs own data after `Object.assign`**
```js
const src = { get x() { return 1; } };
const dst = Object.assign({}, src);
console.log(Object.getOwnPropertyDescriptor(dst, "x"));
```
> **Prints:** a **data** descriptor `{ value: 1, writable: true, … }` — `assign` **invokes** getters.

**Q77 — `seal` vs add**
```js
const o = { x: 1 };
Object.seal(o);
o.x = 2;
o.y = 3;
console.log(o.x, o.y);
```
> **Prints:** `2` `undefined` (and **Throws** on `o.y =` in strict). Seal: mutate existing, no add/delete.

**Q78 — generator**
```js
function* g() {
  yield 1;
  yield 2;
}
const it = g();
console.log(it.next().value, it.next().value, it.next());
```
> **Prints:** `1` `2` `{ value: undefined, done: true }`

**Q79 — `yield*`**
```js
function* inner() { yield "a"; yield "b"; }
function* outer() { yield 1; yield* inner(); yield 2; }
console.log([...outer()]);
```
> **Prints:** `[1, "a", "b", 2]`

**Q80 — `typeof`**
```js
console.log(typeof null, typeof [], typeof class C {}, typeof NaN);
```
> **Prints:** `"object"` `"object"` `"function"` `"number"`  
> Arrays: `Array.isArray`. `null` is the billion-dollar mistake.

**Q81 — `typeof` undeclared**
```js
console.log(typeof notDefined);
```
> **Prints:** `"undefined"` (does not throw).

**Q82 — `0.1 + 0.2`**
```js
console.log(0.1 + 0.2 === 0.3, 0.1 + 0.2);
```
> **Prints:** `false` `0.30000000000000004`  
> **Why:** IEEE-754. Money: integers cents, or `BigInt`, or a decimal library — not `toFixed` as a source of truth.

**Q83 — `parseInt`**
```js
console.log(parseInt("08"), parseInt("hello"), parseInt("10px"));
```
> **Prints:** `8` `NaN` `10` (ES5+ no octal from leading 0). Always pass radix `10` in interviews anyway.

**Q84 — labeled `break` (rare)**
```js
outer: for (let i = 0; i < 2; i++) {
  for (let j = 0; j < 2; j++) {
    if (i === 0 && j === 1) break outer;
    console.log(i, j);
  }
}
```
> **Prints:** `0 0` only.

**Q85 — spread vs `arguments`**
```js
function f(a, ...rest) {
  console.log(a, rest, arguments.length);
}
f(1, 2, 3);
```
> **Prints:** `1` `[2, 3]` `3`

**Q86 — optional chaining assign**
```js
const o = null;
o?.x = 1;
```
> **Throws:** `SyntaxError` (optional chain is not a valid assignment target).

---

## Next: Part 3

➡️ [Part 3 — Implementations, Interview](./14-js-logical-interview-questions-part3.md): 20-minute polyfills (debounce, `bind`, `Promise.all`, flatten, deep equal, emitter, LRU, retry, pool) plus the remaining output items, ~11 h path, 36 meta-questions.
