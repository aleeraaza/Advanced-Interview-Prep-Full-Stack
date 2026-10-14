# 13 — Coding Round Practice (Part 3 of 4): Graphs, DP, Greedy & Tries

> **Parts:** [Part 1 — Format, Big-O, Arrays, Pointers, Windows](./13-coding-round-practice-part1.md) · [Part 2 — Stack, Binary Search, Lists, Trees, Heap](./13-coding-round-practice-part2.md) · **Part 3 — Graphs, DP, Greedy, Tries** · [Part 4 — Machine Coding, Mocks, Interview](./13-coding-round-practice-part4.md)
>
> Graph BFS still must not `shift` ([Part 1](./13-coding-round-practice-part1.md#32-big-o-in-javascript)). Heap: [Part 2](./13-coding-round-practice-part2.md#310-heap--priority-queue). NeetCode 150 names: [neetcode.io/practice](https://neetcode.io/practice). Advanced graphs / math are **skim** for most product roles.

## Table of Contents

- [3. Detailed Explanations (Part 3)](#3-detailed-explanations-part-3)
  - [3.11 Graphs](#311-graphs)
  - [3.12 Recursion & Backtracking](#312-recursion--backtracking)
  - [3.13 Dynamic Programming](#313-dynamic-programming)
  - [3.14 Greedy & Intervals](#314-greedy--intervals)
  - [3.15 Tries](#315-tries)
  - [3.16 Queue, Prefix Sums, Bits](#316-queue-prefix-sums-bits)
  - [3.17 Dijkstra, MST, Math — Skim](#317-dijkstra-mst-math--skim)
  - [3.18 Mock Interviews](#318-mock-interviews)
- [Next: Part 4](#next-part-4)

---

## 3. Detailed Explanations (Part 3)

### 3.11 Graphs

**Represent.** Adjacency list `Map<T, T[]>` or `T[][]`. Grid: the graph *is* the cells; 4-dir `const D = [[1,0],[-1,0],[0,1],[0,-1]]`.

**DFS.** Flood fill, connected components, cycle in undirected (parent skip), path-with-visited for directed (three colors: unvisited / on-stack / done).

**BFS.** Unweighted shortest path (rotting oranges, walls and gates, word ladder). Queue + `head` index, never `shift`.

```ts
function numIslands(grid: string[][]): number {
  const r = grid.length;
  const c = grid[0]?.length ?? 0;
  const dfs = (i: number, j: number): void => {
    if (i < 0 || j < 0 || i >= r || j >= c || grid[i]![j] !== '1') return;
    grid[i]![j] = '0';
    dfs(i + 1, j); dfs(i - 1, j); dfs(i, j + 1); dfs(i, j - 1);
  };
  let n = 0;
  for (let i = 0; i < r; i++) {
    for (let j = 0; j < c; j++) {
      if (grid[i]![j] === '1') {
        n++;
        dfs(i, j);
      }
    }
  }
  return n;
}
```

Say you mutate the grid; clone if they forbid it.

**Topological sort (Kahn).** Indegree array, queue zeros, peel. If you emit fewer than `n` nodes → cycle. Course Schedule I/II.

**Union-Find.** Components, valid tree (`n-1` edges and one component), redundant connection.

```ts
class UnionFind {
  private parent: number[];
  private rank: number[];
  components: number;

  constructor(n: number) {
    this.parent = Array.from({ length: n }, (_, i) => i);
    this.rank = Array<number>(n).fill(0);
    this.components = n;
  }

  find(x: number): number {
    const p = this.parent;
    if (p[x] !== x) p[x] = this.find(p[x]!);
    return p[x]!;
  }

  union(a: number, b: number): boolean {
    let pa = this.find(a);
    let pb = this.find(b);
    if (pa === pb) return false;
    if (this.rank[pa]! < this.rank[pb]!) {
      const t = pa;
      pa = pb;
      pb = t;
    }
    this.parent[pb] = pa;
    if (this.rank[pa] === this.rank[pb]) this.rank[pa]!++;
    this.components--;
    return true;
  }
}
```

**NeetCode 150 — Graphs (19).** Islands · Max Area · Clone Graph · Walls and Gates · Rotting Oranges · Pacific Atlantic · Surrounded Regions · Course Schedule I/II · Graph Valid Tree · Connected Components · Redundant Connection · Word Ladder · Reconstruct Itinerary · Min Cost Connect Points · Network Delay Time · Swim in Rising Water · Alien Dictionary · Cheapest Flights K Stops.

Clone graph: `Map<old, copy>` + DFS/BFS. Pacific Atlantic: reverse-BFS from oceans.

### 3.12 Recursion & Backtracking

**Skeleton.** Choose → recurse → unchoose (`pop`). Prune when leftover cannot win.

```ts
function subsets(nums: number[]): number[][] {
  const out: number[][] = [];
  const cur: number[] = [];
  const dfs = (i: number): void => {
    if (i === nums.length) {
      out.push(cur.slice());
      return;
    }
    dfs(i + 1);
    cur.push(nums[i]!);
    dfs(i + 1);
    cur.pop();
  };
  dfs(0);
  return out;
}
```

**For-loop start at `i`** (combinations, combination sum): `for (let j = i; j < n; j++)` after sort, skip duplicates with `if (j > i && a[j] === a[j-1]) continue`. Permutations: swap or `used[]`. Grid word search: mark cell, recurse 4-dir, unmark.

**NeetCode 150 — Backtracking (9).** Subsets · Combination Sum · Combination Sum II · Permutations · Subsets II · Word Search · Palindrome Partitioning · Letter Combinations · N-Queens.

Generate Parentheses: backtrack with `open`/`close` counts (`close < open`).

### 3.13 Dynamic Programming

**Order.** (1) English subproblem. (2) Recurrence. (3) Base. (4) Table order. (5) Space squeeze if easy. Path: **recursion → memo → tabulation** once per problem, not as theater.

| Family | Subproblem | Recurrence sketch |
|--------|------------|-------------------|
| Climbing / Fibonacci | ways to `i` | `dp[i] = dp[i-1] + dp[i-2]` |
| House robber | max money ending at `i` | `dp[i] = max(dp[i-1], dp[i-2] + a[i])` |
| Coin change (unbounded) | min coins for amount `x` | `dp[x] = min(dp[x-c]) + 1` |
| 0/1 knapsack / partition | with first `i` items, capacity `w` | take / skip |
| LIS | LIS ending at `i` | `max(dp[j]+1)` for `j < i && a[j] < a[i]` — O(n²); patience O(n log n) if they want |
| LCS / edit distance | prefixes `i`, `j` | 2D; `dp[i][j]` from left/up/diag |
| Unique paths | cell `(i,j)` | sum from top + left |

```ts
function coinChange(coins: number[], amount: number): number {
  const inf = amount + 1;
  const dp = Array<number>(amount + 1).fill(inf);
  dp[0] = 0;
  for (let x = 1; x <= amount; x++) {
    for (const c of coins) {
      if (c <= x) dp[x] = Math.min(dp[x]!, dp[x - c]! + 1);
    }
  }
  const ans = dp[amount]!;
  return ans >= inf ? -1 : ans;
}
```

If you cannot name `dp[i]` in one sentence, you are guessing. 2D strings: index `i` = length of prefix (0..n), not "the i-th char" until you are consistent.

**NeetCode 150 — DP (23).** 1D: Climbing Stairs · Min Cost Climb · House Robber I/II · Palindromic substring(s) · Decode Ways · Coin Change · Max Product Subarray · Word Break · LIS · Partition Equal Subset Sum. 2D: Unique Paths · LCS · Stock cooldown · Coin Change II · Target Sum · Interleaving String · LIP in Matrix · Distinct Subsequences · Edit Distance · Burst Balloons · Regex Matching.

For product interviews, **1D + Unique Paths + LCS + Coin Change + House Robber + LIS** is the core. Burst Balloons / regex: if time.

### 3.14 Greedy & Intervals

**Intervals.** Sort. Merge: sort by start, extend `end` while overlap. Non-overlapping: sort by **end**, greedily take next that starts ≥ last end (max meetings). Meeting Rooms II: sort starts and ends, two pointers, count concurrent. Insert interval: splice into the merged list.

**Greedy.** Local choice with a proof ("if I skip this I cannot do better"). Jump Game: farthest reachable. Gas station: unique start = total gas ≥ total cost and track tank. Kadane (max subarray) is greedy/DP hybrid — running `cur = max(a[i], cur + a[i])`.

**NeetCode 150 — Intervals (6) + Greedy (8).** Insert / Merge / Non-overlapping / Meeting Rooms I/II / Min Interval to Include Query. Max Subarray · Jump I/II · Gas Station · Hand of Straights · Merge Triplets · Partition Labels · Valid Parenthesis String.

### 3.15 Tries

Children `Map<string, TrieNode>` (or `length-26` array for lowercase). `end` flag. Prefix search = walk. Word Search II: DFS the board **and** the trie together; prune dead prefixes; optional delete leaf to speed up.

```ts
class TrieNode {
  children = new Map<string, TrieNode>();
  end = false;
}

class Trie {
  private root = new TrieNode();

  insert(word: string): void {
    let n = this.root;
    for (const ch of word) {
      let c = n.children.get(ch);
      if (!c) {
        c = new TrieNode();
        n.children.set(ch, c);
      }
      n = c;
    }
    n.end = true;
  }

  search(word: string): boolean {
    const n = this.walk(word);
    return n !== undefined && n.end;
  }

  startsWith(prefix: string): boolean {
    return this.walk(prefix) !== undefined;
  }

  private walk(s: string): TrieNode | undefined {
    let n: TrieNode | undefined = this.root;
    for (const ch of s) {
      n = n.children.get(ch);
      if (!n) return undefined;
    }
    return n;
  }
}
```

**NeetCode 150 — Tries (3).** Implement Trie · Add and Search Words (`.` wildcard = DFS children) · Word Search II.

### 3.16 Queue, Prefix Sums, Bits

**Deque.** Two-end operations: use an array + `lo` index, or two stacks. Sliding-window maximum = monotonic deque ([Part 2](./13-coding-round-practice-part2.md#36-stack--monotonic-stack)).

**Prefix sums.** `pref[0] = 0`, `pref[i+1] = pref[i] + a[i]`. Range `i..j` = `pref[j+1] - pref[i]`. Subarray sum = k: `Map<prefix, count>` as you walk. 2D prefix for matrices (skim).

**Bits (basics).** `n & 1`, `n >> 1`. `n & (n-1)` drops lowest set bit. XOR: `a^a = 0`, `a^0 = a` → single number, missing number. Don't open with bit tricks unless the problem is clearly bits.

**NeetCode 150** folds these into other lists plus a **Bit Manipulation (7)** bucket (Number of 1 Bits, Counting Bits, Reverse Bits, Missing Number, Sum of Two Integers, Reverse Integer, Single Number — confirm on the site).

### 3.17 Dijkstra, MST, Math — Skim

**Dijkstra.** Non-negative weights. Min-heap of `[dist, node]`; skip stale heap entries (`if (d > dist[u]) continue`). `Network Delay Time`, `Cheapest Flights` (Bellman-Ford / constrained Dijkstra). **MST:** Kruskal (sort edges + UF) or Prim. Product roles: **Dijkstra + UF**, not Prim proofs.

**Math/geometry.** Rotate matrix layers, spiral, set zeroes (O(1) space = first row/col as markers), `pow(x,n)` binary exponent. Skim the NeetCode math list unless the JD says graphics.

### 3.18 Mock Interviews

Syllabus: **1 timed mock / week from week 3** ([16](./16-study-plan.md)). Pramp, interviewing.io, a peer, or a recording of yourself.

**Rules.** 45 minutes, **out loud**, no pausing the clock to "think privately," no LeetCode tags. After: note the first 5 minutes (did you freeze?), whether you stated complexity, one missed edge.

Reuse the [§3.1](./13-coding-round-practice-part1.md#31-the-coding-round) talk track. Machine-coding mocks: [Part 4](./13-coding-round-practice-part4.md) + [04](./04-react-part3.md).

---

## Next: Part 4

➡️ [Part 4 — Machine Coding, Mocks, Interview](./13-coding-round-practice-part4.md): 5-step UI/API plan (React builds stay in 04), vanilla DOM, 45-min REST, PR debugging, then resources, ~99 h, 10 exercises, 36 questions.
