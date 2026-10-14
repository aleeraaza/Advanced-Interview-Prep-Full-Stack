# 14 — JS Logical Questions (Part 1 of 3): Closures, `this` & Prototypes

> **Parts:** **Part 1 — Closures, `this`, Prototypes** · [Part 2 — Event Loop, Coercion, Oddballs](./14-js-logical-interview-questions-part2.md) · [Part 3 — Implementations, Interview](./14-js-logical-interview-questions-part3.md)
>
> **How to drill.** Cover the snippet. Predict out loud. Then read **Prints** / **Throws**. Theory lives in [02](./02-javascript.md) — this file is the gym. **Environment:** ES module / Node 24 type-stripped `.ts` / `"type": "module"` → **strict**, top-level `this` is `undefined`, `var` does **not** become `globalThis.x`. Browser sloppy-script differences are called out. Do **not** paste Lydia Hallie answers from memory as if they were this file — these items are written here. 5/day while you study 02 ([00](./00-README.md#recommended-study-order)).

## Table of Contents

- [1. Overview](#1-overview)
- [2. Topic Map](#2-topic-map)
- [3. How to Answer in the Room](#3-how-to-answer-in-the-room)
- [4. Closures, `var`/`let`/`const`, Hoisting — Q1–Q18](#4-closures-varletconst-hoisting--q1q18)
- [5. `this` — Q19–Q32](#5-this--q19q32)
- [6. Prototypes & Classes — Q33–Q42](#6-prototypes--classes--q33q42)
- [Next: Part 2](#next-part-2)

---

## 1. Overview

Interviewers use **output questions** to see if [02](./02-javascript.md) is in your bones. A senior answer names the **rule** (per-iteration `let`, `new` beats `bind`, ToPrimitive) then the printout — not "I ran it once."

| Junior | Senior |
|--------|--------|
| "`var` is weird" | "One function-scoped binding; all timeouts close over the same `i`" |
| "`this` is the object" | Call-site rules; arrows are lexical; extraction loses implicit binding |
| "`__proto__` is the class" | `[[Prototype]]` chain; `constructor`; `instanceof` walks the chain |

> 💡 Interview Tip: Say the queue or the binding **before** the numbers. Wrong numbers with the right rule still beats memorized output.

---

## 2. Topic Map

- [ ] Closures / TDZ / hoisting — [Q1–Q18](#4-closures-varletconst-hoisting--q1q18)
- [ ] `this` — [Q19–Q32](#5-this--q19q32)
- [ ] Prototypes — [Q33–Q42](#6-prototypes--classes--q33q42)
- [ ] Event loop, coercion, descriptors, generators — [Part 2](./14-js-logical-interview-questions-part2.md)
- [ ] Implement debounce, `Promise.all`, LRU, emitter, pool — [Part 3](./14-js-logical-interview-questions-part3.md)

---

## 3. How to Answer in the Room

1. Strict or sloppy? Module or script?
2. When is the function **created** vs **called**?
3. What does `this` / the closure capture **at creation**?
4. Sync log → microtasks → tasks ([02 §3.7](./02-javascript-part1.md#37-the-event-loop-browser)).

---

## 4. Closures, `var`/`let`/`const`, Hoisting — Q1–Q18

Theory: [02 §3.2–3.4](./02-javascript-part1.md#32-hoisting--the-temporal-dead-zone).

**Q1 — `var` loop**
```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i), 0);
```
> **Prints:** `3` `3` `3`  
> **Why:** one `i`. Timeouts run after the loop.

**Q2 — `let` loop**
```js
for (let i = 0; i < 3; i++) setTimeout(() => console.log(i), 0);
```
> **Prints:** `0` `1` `2`  
> **Why:** new binding per iteration (`CreatePerIterationEnvironment`).

**Q3 — IIFE fix**
```js
for (var i = 0; i < 3; i++) {
  (function (j) { setTimeout(() => console.log(j), 0); })(i);
}
```
> **Prints:** `0` `1` `2`

**Q4 — `setTimeout` extra arg**
```js
for (var i = 0; i < 3; i++) setTimeout((j) => console.log(j), 0, i);
```
> **Prints:** `0` `1` `2`  
> **Why:** the host passes `i` *now* as the callback argument.

**Q5 — factory**
```js
function make(n) {
  return () => n++;
}
const a = make(0);
console.log(a(), a(), make(0)());
```
> **Prints:** `0` `1` `0`  
> **Why:** two closures, two `n` bindings.

**Q6 — shared object**
```js
const cfg = { n: 0 };
const f = () => ++cfg.n;
console.log(f(), f(), cfg.n);
```
> **Prints:** `1` `2` `2`  
> **Why:** live binding to the object, not a copy of `0`.

**Q7 — `var` leak in function**
```js
function f() {
  if (false) var x = 1;
  console.log(x);
}
f();
```
> **Prints:** `undefined`  
> **Why:** `var` hoisted, initialized `undefined`; `if` never assigns.

**Q8 — TDZ**
```js
console.log(a);
let a = 1;
```
> **Throws:** `ReferenceError` (TDZ). Not `undefined`.

**Q9 — `typeof` undeclared vs TDZ**
```js
console.log(typeof undeclared);
console.log(typeof b);
let b = 1;
```
> **Prints:** `"undefined"` then **Throws** `ReferenceError`  
> **Why:** `typeof` on an unresolvable reference is `"undefined"`; `b` *is* resolvable but uninitialized.

**Q10 — function vs `var` same name**
```js
console.log(typeof foo);
var foo = 1;
function foo() {}
console.log(typeof foo);
```
> **Prints:** `"function"` then `"number"`  
> **Why:** both hoisted; the function initializes the binding; then the assignment overwrites.

**Q11 — function expression**
```js
bar();
var bar = function () { console.log("hi"); };
```
> **Throws:** `TypeError` (`bar` is `undefined`, not a function).

**Q12 — function declaration usable early**
```js
foo();
function foo() { console.log("hi"); }
```
> **Prints:** `hi`

**Q13 — `const` object**
```js
const o = { x: 1 };
o.x = 2;
o = { x: 3 };
```
> **Prints:** none; assignment `o.x` ok; **Throws** on `o =` (`TypeError`).

**Q14 — default param TDZ**
```js
function f(x = y, y = 2) { return x + y; }
f();
```
> **Throws:** `ReferenceError` (`y` in TDZ while evaluating `x`).

**Q15 — default sees later binding after init**
```js
function f(x = 1, y = x) { return [x, y]; }
console.log(f(), f(5), f(5, 9));
```
> **Prints:** `[1,1]` `[5,5]` `[5,9]`

**Q16 — `catch` binding**
```js
try { throw 1; } catch (e) {}
console.log(typeof e);
```
> **Prints:** `"undefined"` (`e` is block-scoped to `catch`).

**Q17 — `switch` TDZ**
```js
const n = 1;
switch (n) {
  case 1:
    let x = 2;
    break;
  case 2:
    console.log(x);
}
```
> **Note:** `let x` scopes the whole `switch` block. Hitting `case 2` first would TDZ. Here only `case 1` runs — **no log**.

**Q18 — stale closure (the React cousin)**
```js
function make() {
  let n = 0;
  const read = () => n;
  const bump = () => { n++; };
  return { read, bump };
}
const { read, bump } = make();
bump(); bump();
console.log(read());
```
> **Prints:** `2`  
> **Why:** both functions share the same `n`. Contrast: capturing `n` *by value* into a new const inside `read` at creation time would freeze 0. React stale props = new function per render, old interval still holds the previous one ([04](./04-react.md)).

---

## 5. `this` — Q19–Q32

Theory: [02 §3.5](./02-javascript-part1.md#35-this-binding). Precedence: `new` > explicit (`call`/`apply`/`bind`) > implicit (`obj.fn()`) > default (`undefined` strict).

**Q19 — extraction**
```js
const obj = {
  n: 1,
  f() { return this.n; },
};
const g = obj.f;
console.log(obj.f(), g());
```
> **Prints:** `1` then **Throws** `TypeError` (read `n` of `undefined`) in a module.

**Q20 — arrow on a literal**
```js
const obj = {
  n: 1,
  f: () => this.n,
};
console.log(obj.f());
```
> **Throws** in a module (`this` is `undefined` at module top). Arrow captured **lexical** `this`, not `obj`.

**Q21 — method that returns an arrow**
```js
const obj = {
  n: 1,
  f() { return () => this.n; },
};
console.log(obj.f()(), obj.f.call({ n: 7 })());
```
> **Prints:** `1` `7`  
> **Why:** the arrow closes over `f`'s `this`.

**Q22 — class field arrow vs method**
```js
class C {
  n = 1;
  method() { return this.n; }
  arrow = () => this.n;
}
const c = new C();
const { method, arrow } = c;
console.log(arrow(), method());
```
> **Prints:** `1` then **Throws** (`method` lost `this`). Field arrow is bound per instance.

**Q23 — `bind` then `bind`**
```js
function f() { return this.n; }
const a = f.bind({ n: 1 });
const b = a.bind({ n: 2 });
console.log(a(), b());
```
> **Prints:** `1` `1`  
> **Why:** second `bind` cannot replace bound `this`. (It *can* prepend more args.)

**Q24 — `bind` then `new`**
```js
function F() { this.n = 1; }
const B = F.bind({ n: 99 });
const x = new B();
console.log(x.n, x instanceof F, x instanceof B);
```
> **Prints:** `1` `true` `true`  
> **Why:** `new` beats bound `this`. Bound functions use the target's `[[Prototype]]`. `instanceof B` is also true (bound functions set `prototype` forwarding).

**Q25 — `call` with a primitive (strict)**
```js
function f() { return typeof this; }
console.log(f.call(1));
```
> **Prints:** `"number"` in strict (primitive `this` is **not** boxed). Sloppy would box to `Number`.

**Q26 — `setTimeout` (browser)**
```js
const obj = { n: 1, f() { console.log(this.n); } };
setTimeout(obj.f, 0);
```
> **Prints:** `undefined` (or throws if the engine is strict about `this.n`). The timer **calls** `f` as a bare function. Fix: `() => obj.f()` or `obj.f.bind(obj)`.

**Q27 — nested function**
```js
const obj = {
  n: 1,
  f() {
    function inner() { return this.n; }
    return inner();
  },
};
console.log(obj.f());
```
> **Throws** in strict (`inner`'s default `this` is `undefined`).

**Q28 — `obj.a.b()`**
```js
const a = { n: 2, b() { return this.n; } };
const obj = { n: 1, a };
console.log(obj.a.b());
```
> **Prints:** `2`  
> **Why:** the base reference for the call is `obj.a`, not `obj`.

**Q29 — `class` without `new`**
```js
class C {}
C();
```
> **Throws:** `TypeError` (class constructors require `new`).

**Q30 — `this` in a getter**
```js
const obj = {
  n: 1,
  get f() { return this.n; },
};
const { f } = obj;
console.log(obj.f, f);
```
> **Prints:** `1` `1`  
> **Why:** destructuring **invokes** the getter with `obj` as `this`, then copies the already-computed `1`.

**Q31 — getter extracted as a function**
```js
const obj = {
  n: 1,
  get f() { return this.n; },
};
const desc = Object.getOwnPropertyDescriptor(obj, "f");
console.log(desc.get.call(obj), desc.get());
```
> **Prints:** `1` then **Throws** (`this` undefined).

**Q32 — explicit `undefined` in sloppy vs strict**
```js
function f() { return this; }
console.log(f.call(undefined) === globalThis);
```
> **Prints:** `false` in a module (strict: `this` is actually `undefined`). In sloppy script, `call(undefined)` becomes `globalThis` → `true`.

---

## 6. Prototypes & Classes — Q33–Q42

Theory: [02 §3.6](./02-javascript-part1.md#36-prototypes--inheritance).

**Q33 — chain**
```js
const p = { x: 1 };
const o = Object.create(p);
console.log(o.x, o.hasOwnProperty("x"), Object.getPrototypeOf(o) === p);
```
> **Prints:** `1` `false` `true`

**Q34 — overwrite**
```js
const p = { x: 1 };
const o = Object.create(p);
o.x = 2;
console.log(o.x, p.x, delete o.x, o.x);
```
> **Prints:** `2` `1` `true` `1`  
> **Why:** own property shadows; `delete` reveals the prototype again.

**Q35 — `instanceof`**
```js
class A {}
class B extends A {}
const b = new B();
console.log(b instanceof B, b instanceof A, b instanceof Object);
```
> **Prints:** `true` `true` `true`

**Q36 — constructor**
```js
class A {}
const a = new A();
console.log(a.constructor === A, a.constructor === A.prototype.constructor);
```
> **Prints:** `true` `true`

**Q37 — `new.target`**
```js
function F() { return new.target ? "ctor" : "call"; }
console.log(F(), new F());
```
> **Prints:** `"call"` `"ctor"`

**Q38 — static vs instance**
```js
class C {
  static s() { return "S"; }
  i() { return "I"; }
}
console.log(C.s(), new C().i(), typeof new C().s);
```
> **Prints:** `"S"` `"I"` `"undefined"`

**Q39 — extending `Array`**
```js
class MyArray extends Array {}
const a = new MyArray(1, 2);
console.log(a.length, a instanceof Array, a.map((x) => x) instanceof MyArray);
```
> **Prints:** `2` `true` `true`  
> **Why:** species / `Symbol.species` — `map` constructs `MyArray`.

**Q40 — `this` before `super`**
```js
class A { constructor() { this.x = 1; } }
class B extends A {
  constructor() { this.y = 2; super(); }
}
new B();
```
> **Throws:** `ReferenceError` (`this` of a derived class is TDZ until `super()`).

**Q41 — prototype method sharing**
```js
class C { f() {} }
console.log(new C().f === new C().f, new C().f === C.prototype.f);
```
> **Prints:** `true` `true`

**Q42 — arrow field not shared**
```js
class C { f = () => {}; }
console.log(new C().f === new C().f);
```
> **Prints:** `false`  
> **Why:** each instance gets its own function (and closes over that instance's `this`).

---

## Next: Part 2

➡️ [Part 2 — Event Loop, Coercion, Oddballs](./14-js-logical-interview-questions-part2.md): microtasks vs `setTimeout`, ToPrimitive / `==`, descriptors & freeze, generators, `typeof`, `0.1 + 0.2`.
