# 13 — Coding Round Practice (Part 2 of 4): Stack, Binary Search, Lists, Trees & Heap

> **Parts:** [Part 1 — Format, Big-O, Arrays, Pointers, Windows](./13-coding-round-practice-part1.md) · **Part 2 — Stack, Binary Search, Lists, Trees, Heap** · [Part 3 — Graphs, DP, Greedy, Tries](./13-coding-round-practice-part3.md) · [Part 4 — Machine Coding, Mocks, Interview](./13-coding-round-practice-part4.md)
>
> JS has **no** `PriorityQueue`. Write a heap once and paste it. Recursion on skewed trees will blow the stack ([02](./02-javascript-part1.md#31-execution-context--the-call-stack)) — know the iterative version. `shift()` in BFS is still O(n) per pop ([Part 1](./13-coding-round-practice-part1.md#32-big-o-in-javascript)).

## Table of Contents

- [3. Detailed Explanations (Part 2)](#3-detailed-explanations-part-2)
  - [3.6 Stack & Monotonic Stack](#36-stack--monotonic-stack)
  - [3.7 Binary Search](#37-binary-search)
  - [3.8 Linked List](#38-linked-list)
  - [3.9 Trees](#39-trees)
  - [3.10 Heap / Priority Queue](#310-heap--priority-queue)
- [Next: Part 3](#next-part-3)

---

## 3. Detailed Explanations (Part 2)

### 3.6 Stack & Monotonic Stack

**Stack.** LIFO. Matching brackets, nested structure, "evaluate" (RPN), undo. Array `push`/`pop` only — never `shift`.

```ts
function isValid(s: string): boolean {
  const st: string[] = [];
  const close: Record<string, string> = { ')': '(', ']': '[', '}': '{' };
  for (const ch of s) {
    const open = close[ch];
    if (open === undefined) st.push(ch);
    else if (st.pop() !== open) return false;
  }
  return st.length === 0;
}
```

**Monotonic stack.** Indices in increasing (or decreasing) order of value. When the order would break, pop and **the answer for the popped index is the current index** (next greater / warmer day / rectangle width).

```ts
function dailyTemperatures(t: number[]): number[] {
  const ans = Array<number>(t.length).fill(0);
  const st: number[] = []; // indices, temps strictly decreasing
  for (let i = 0; i < t.length; i++) {
    while (st.length > 0 && t[i]! > t[st[st.length - 1]!]!) {
      const j = st.pop()!;
      ans[j] = i - j;
    }
    st.push(i);
  }
  return ans;
}
```

Same skeleton: largest rectangle, next greater element, sliding-window maximum (deque of indices, decreasing values — pop back while smaller, pop front when out of window).

**NeetCode 150 — Stack (7).** Valid Parentheses · Min Stack · Evaluate RPN · Generate Parentheses · Daily Temperatures · Car Fleet · Largest Rectangle in Histogram.

Min stack: two stacks, or store `{ val, minSoFar }`. Generate parentheses is backtracking ([Part 3](./13-coding-round-practice-part3.md#312-recursion--backtracking)) that *uses* a stack of parentheses.

### 3.7 Binary Search

Two families. Name which one you are in **before** the loop.

**A. Exact find in a sorted array** — `lo <= hi`, `mid` excluded from both sides:

```ts
function binarySearch(a: number[], target: number): number {
  let lo = 0;
  let hi = a.length - 1;
  while (lo <= hi) {
    const mid = lo + ((hi - lo) >> 1); // not (lo+hi)/2 overflow theater; still avoids lo+hi surprise
    const v = a[mid]!;
    if (v === target) return mid;
    if (v < target) lo = mid + 1;
    else hi = mid - 1;
  }
  return -1;
}
```

**B. First true / lower bound** — search the **answer space**. Invariant: `lo` is the first index that might be valid, `hi` is exclusive. `while (lo < hi)`, never infinite if `mid` is `lo + ((hi-lo)>>1)` and you always do `lo = mid + 1` or `hi = mid`.

```ts
/** First index i with a[i] >= target (or a.length). */
function lowerBound(a: number[], target: number): number {
  let lo = 0;
  let hi = a.length;
  while (lo < hi) {
    const mid = lo + ((hi - lo) >> 1);
    if (a[mid]! < target) lo = mid + 1;
    else hi = mid;
  }
  return lo;
}

/** Smallest eating speed so Koko finishes in h hours. */
function minEatingSpeed(piles: number[], h: number): number {
  const can = (k: number): boolean => {
    let hours = 0;
    for (const p of piles) hours += Math.ceil(p / k);
    return hours <= h;
  };
  let lo = 1;
  let hi = Math.max(...piles);
  while (lo < hi) {
    const mid = lo + ((hi - lo) >> 1);
    if (can(mid)) hi = mid;
    else lo = mid + 1;
  }
  return lo;
}
```

**Rotated array.** Compare `a[lo]`, `a[mid]`, `a[hi]` to see which half is sorted; then decide if `target` lives there. Find-min-in-rotated is "search on answer" for the rotation point.

**Duplicates.** If `a[lo] === a[mid] === a[hi]`, you may have to `lo++` / `hi--` and lose the log. Say that.

**NeetCode 150 — Binary Search (7).** Binary Search · Search a 2D Matrix · Koko Eating Bananas · Find Minimum in Rotated Sorted Array · Search in Rotated Sorted Array · Time Based Key-Value Store · Median of Two Sorted Arrays.

> ⚠️ Pitfall: Mixing A and B. `hi = a.length - 1` with `hi = mid` and `lo < hi` is a stuck loop or skipped cell. Pick one template and **prove** the loop shrinks.

### 3.8 Linked List

Draw boxes. Dummy head (`const dummy = { val: 0, next: head }`) for insert/delete at head. Two pointers: `slow`/`fast` for mid and cycle (Floyd). `ahead` by `n` then walk together for nth-from-end.

```ts
class ListNode {
  val: number;
  next: ListNode | null;
  constructor(val = 0, next: ListNode | null = null) {
    this.val = val;
    this.next = next;
  }
}

function reverseList(head: ListNode | null): ListNode | null {
  let prev: ListNode | null = null;
  let cur = head;
  while (cur) {
    const nxt = cur.next;
    cur.next = prev;
    prev = cur;
    cur = nxt;
  }
  return prev;
}

function hasCycle(head: ListNode | null): boolean {
  let slow = head;
  let fast = head;
  while (fast && fast.next) {
    slow = slow!.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}
```

Merge two sorted: dummy + tail. Reorder list: mid, reverse second half, weave. Copy random pointer: the "interleave copies" trick or a `Map<old, copy>`. LRU: `Map` + doubly linked list (JS `Map` insertion order can fake LRU for interviews — know both; they often want the list).

**NeetCode 150 — Linked List (11).** Reverse · Merge Two Sorted · Cycle · Reorder · Remove Nth From End · Copy Random Pointer · Add Two Numbers · Find the Duplicate Number · LRU Cache · Merge k Sorted Lists · Reverse Nodes in k-Group.

Merge k: min-heap of k heads ([§3.10](#310-heap--priority-queue)) or pairwise merge.

### 3.9 Trees

```ts
class TreeNode {
  val: number;
  left: TreeNode | null;
  right: TreeNode | null;
  constructor(val = 0, left: TreeNode | null = null, right: TreeNode | null = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}
```

**Recursive DFS.** Height, invert, same tree, path sum, validate BST (`lo < val < hi` with `-Infinity`/`Infinity`, not a global prev unless inorder). Return **two facts** when needed (height **and** balanced; max path through node).

**Iterative DFS.** Explicit stack of nodes (or `{ node, state }`).

**BFS / level order.** Queue. Do **not** `shift` — use an index:

```ts
function levelOrder(root: TreeNode | null): number[][] {
  if (!root) return [];
  const q: TreeNode[] = [root];
  let i = 0;
  const out: number[][] = [];
  while (i < q.length) {
    const end = q.length;
    const level: number[] = [];
    while (i < end) {
      const n = q[i++]!;
      level.push(n.val);
      if (n.left) q.push(n.left);
      if (n.right) q.push(n.right);
    }
    out.push(level);
  }
  return out;
}
```

**BST.** Inorder is sorted. LCA: walk while `p` and `q` are on the same side of `node`. Kth smallest: inorder until `k`.

**Construct from preorder+inorder.** `pre[0]` is root; partition inorder; recurse. Map value → inorder index once. Serialize: preorder with `null` sentinels, or BFS.

**NeetCode 150 — Trees (15).** Invert · Max Depth · Diameter · Balanced · Same Tree · Subtree · LCA of BST · Level Order · Right Side View · Good Nodes · Validate BST · Kth Smallest BST · Construct from Pre+In · Max Path Sum · Serialize/Deserialize.

> 💡 Interview Tip: Validate BST is **not** "left < node < right" locally only. A right-left grandchild can still violate the ancestor bound. Pass the range.

### 3.10 Heap / Priority Queue

JS **does not** have one. Interviewers expect you to write a binary heap or say "I'd import a heap; here is the API" **and still implement it** at many companies.

0-based array: children `2i+1`, `2i+2`; parent `(i-1)>>1`.

```ts
class MinHeap {
  private a: number[] = [];

  get size(): number {
    return this.a.length;
  }

  peek(): number | undefined {
    return this.a[0];
  }

  push(x: number): void {
    this.a.push(x);
    this.up(this.a.length - 1);
  }

  pop(): number | undefined {
    const n = this.a.length;
    if (n === 0) return undefined;
    const top = this.a[0]!;
    const last = this.a.pop()!;
    if (n > 1) {
      this.a[0] = last;
      this.down(0);
    }
    return top;
  }

  private up(i: number): void {
    const a = this.a;
    while (i > 0) {
      const p = (i - 1) >> 1;
      if (a[p]! <= a[i]!) break;
      const tmp = a[p]!;
      a[p] = a[i]!;
      a[i] = tmp;
      i = p;
    }
  }

  private down(i: number): void {
    const a = this.a;
    for (;;) {
      let m = i;
      const l = i * 2 + 1;
      const r = l + 1;
      if (l < a.length && a[l]! < a[m]!) m = l;
      if (r < a.length && a[r]! < a[m]!) m = r;
      if (m === i) break;
      const tmp = a[i]!;
      a[i] = a[m]!;
      a[m] = tmp;
      i = m;
    }
  }
}
```

Generic heap: store `{ key, val }` and compare `key`. Max-heap: negate, or flip comparisons.

**Top K.** Size-k min-heap of the best so far, O(n log k). Bucket sort of frequencies is O(n) for Top K Frequent.

**Median stream.** Max-heap (lower half) + min-heap (upper half); rebalance sizes.

**NeetCode 150 — Heap (7).** Kth Largest in a Stream · Last Stone Weight · K Closest Points · Kth Largest in an Array · Task Scheduler · Design Twitter · Find Median from Data Stream.

Reuse this class in graph Dijkstra ([Part 3](./13-coding-round-practice-part3.md#317-dijkstra-mst-skim)).

---

## Next: Part 3

➡️ [Part 3 — Graphs, DP, Greedy, Tries](./13-coding-round-practice-part3.md): BFS/DFS/topo/union-find, backtracking skeleton, 1D/2D DP, intervals, tries, prefix/bits, then mocks.
