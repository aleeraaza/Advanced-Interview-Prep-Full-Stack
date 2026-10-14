# 08 — Engineering Practices (Part 5 of 5): Resources, Practice, Interview Questions & Revision

> **Parts:** [Part 1 — SOLID, Patterns, Clean Code](./08-engineering-practices-part1.md) · [Part 2 — Testing](./08-engineering-practices-part2.md) · [Part 3 — Git, CI/CD, Docker, Monorepos](./08-engineering-practices-part3.md) · [Part 4 — Security, Observability, Accessibility](./08-engineering-practices-part4.md) · **Part 5 — Resources, Practice, Interview Questions & Revision**
>
> Applies to: Vitest 5, Playwright 1.64, MSW 3, ESLint 10, Biome 2.5, Turborepo 2.11, `actions/checkout@v7`, OWASP Top 10:2025, `@sentry/node` 11 — as of October 2026. Verify version-specific claims on the official docs.

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
| SOLID / architecture | *Clean Architecture* (Robert C. Martin) | book | Publisher / libraries | Paid | SRP and DIP in the large; skip the Java ceremony, keep the axes of change |
| Patterns | Refactoring Guru — Design Patterns | site | refactoring.guru/design-patterns | Free | Structure + when *not* to use it |
| Patterns in JS | patterns.dev | site | patterns.dev | Free | Rendering/performance patterns next to classic GoF names |
| Smells / refactoring | *Refactoring* (Fowler, 2nd ed., JS examples); Refactoring Guru "Code smells" | book/site | Book; refactoring.guru | Paid/Free | The move catalog you use in PRs |
| Hexagonal | Alistair Cockburn "Hexagonal Architecture" | article | alistair.cockburn.us | Free | Ports and adapters, original |
| DDD vocab | Fowler bliki (Bounded Context, Ubiquitous Language) | article | martinfowler.com | Free | Enough vocabulary for a design interview |
| Testing trophy | Kent C. Dodds "The Testing Trophy and Testing Classifications" | article | kentcdodds.com/blog | Free | Why integration sits in the bowl |
| Test pyramid | Martin Fowler "The Practical Test Pyramid" | article | martinfowler.com | Free | Cost vs confidence |
| Vitest 5 | Vitest documentation + v5 announcement | docs | vitest.dev | Free | `clearMocks`, top-level `vi.mock`, Node 22.12 |
| RTL | Testing Library docs; Kent "Common mistakes with RTL" | docs/article | testing-library.com; kentcdodds.com/blog | Free | Query priority; async `findBy` |
| MSW 3 | MSW docs (v3) | docs | mswjs.io | Free | `msw/http` entrypoint |
| Playwright | Playwright docs: locators, auth, CI | docs | playwright.dev | Free | `storageState`, traces |
| Doubles | Fowler "Mocks Aren't Stubs" | article | martinfowler.com | Free | Dummy/stub/spy/mock/fake |
| k6 / Pact | Grafana k6 docs; Pact docs | docs | grafana.com/docs/k6; docs.pact.io | Free | Skim; one script is enough |
| Git | *Pro Git* book | book | git-scm.com/book | Free | Bisect, reflog, rebase — the source |
| Git practice | Learn Git Branching | exercises | learngitbranching.js.org | Free | Muscle memory for rebase/merge |
| Code review | Google Engineering Practices — Code Review | guide | google.github.io/eng-practices | Free | What to look for; CL size |
| Feature flags | Fowler "Feature Toggles" | article | martinfowler.com | Free | Release/experiment/ops/permission |
| GitHub Actions | GitHub Actions docs; checkout v7 changelog | docs | docs.github.com/en/actions; github.blog/changelog | Free | Environments, OIDC, pwn-request defaults |
| Docker | Docker docs: building, multi-stage, Compose | docs | docs.docker.com | Free | Layers and `USER` |
| Monorepos | Turborepo docs; pnpm Workspaces; Nx docs | docs | turborepo.com; pnpm.io; nx.dev | Free | Task graph vs "just workspaces" |
| ESLint 10 | ESLint "Configure ESLint" (flat config) | docs | eslint.org | Free | `.eslintrc` is gone |
| Biome | Biome docs | docs | biomejs.dev | Free | Lint + format in one |
| ADRs | adr.github.io | site | adr.github.io | Free | The five-section template |
| OWASP web | OWASP Top 10:2025 | docs | owasp.org/Top10/2025/ | Free | A03 supply chain; A10 exceptional conditions |
| OWASP API | OWASP API Security Top 10:2023 | docs | owasp.org | Free | BOLA vocabulary |
| XSS / CSRF | OWASP Cheat Sheets; MDN CSP | docs | cheatsheetseries.owasp.org; MDN | Free | Encoding, tokens, `SameSite` |
| Headers | MDN HTTP headers | docs | MDN | Free | What `helmet` actually sets |
| Node risks | Node.js Security Best Practices; [06](./06-nodejs-part3.md#323-security) | docs | nodejs.org/en/learn | Free | SSRF, pollution, ReDoS |
| SLOs | Google SRE Book ch. 4 & 6 | book | sre.google/books | Free | SLI/SLO/error budget |
| Sentry 11 | Sentry Node docs + v10→v11 migration | docs | docs.sentry.io | Free | Native spans; `enableOpenTelemetrySetup` |
| Accessibility | WCAG 2.2 quickref; axe DevTools; APG | docs | w3.org/WAI/WCAG22/quickref; deque.com/axe; w3.org/WAI/ARIA/apg | Free | AA bar; what axe cannot see |
| Perf budgets | web.dev "Performance budgets"; Lighthouse CI | docs | web.dev; github.com/GoogleChrome/lighthouse-ci | Free | Lab gate vs field RUM |
| CWV mechanics | [05-nextjs Part 3 §3.16](./05-nextjs-part3.md#316-core-web-vitals) | notes | This repo | Free | Don't re-learn LCP here |

> 💡 Interview Tip: Cheat sheets age. Confirm the OWASP *year* on owasp.org/Top10/2025/ the morning of the interview.

---

## 7. How to Learn It

Total: **~34 hours** (matches the [syllabus](./01-fullstack-syllabus.md#time-budget-overview) Testing 10 h + Engineering practices 16 h + Web security 8 h). Prerequisites: [04](./04-react.md) (RTL queries), [06](./06-nodejs.md) (API tests, Pino/OTel, Node exploits), [07](./07-databases-and-apis.md) (parameterized SQL). CWV math stays in [05](./05-nextjs.md).

| Step | What to do | Time |
|------|-----------|:----:|
| **0. Self-assess** | Tick the [Topic Map](./08-engineering-practices-part1.md#2-topic-map). Answer [Q31–Q36](#tricky) cold. | 0.5 h |
| **1. SOLID & patterns** | [Part 1 §3.1–3.2](./08-engineering-practices-part1.md). Refactor a god `checkout`. Name five patterns in libraries you already use. | 3.5 h |
| **2. Clean code & hexagonal** | [§3.3–3.4](./08-engineering-practices-part1.md#33-clean-code-smells-and-refactoring). Extract a 200-line function behind tests. Draw ports for your API. | 2 h |
| **3. Trophy + Vitest 5** | [Part 2 §3.5–3.6](./08-engineering-practices-part2.md). Classify your current tests. Debounce with fake timers (verified snippet). | 3 h |
| **4. RTL, MSW 3, Playwright, doubles** | [§3.7–3.9](./08-engineering-practices-part2.md#37-component-tests-and-msw-3) + [04 §3.10](./04-react-part2.md#310-testing-react). One page test with `msw/http`; one Playwright journey with `storageState`. | 4.5 h |
| **5. k6 / Pact skim** | [§3.10](./08-engineering-practices-part2.md#310-load-contract-mutation--skim). One k6 script with a p95 threshold. | 0.5 h |
| **6. Git + review** | [Part 3 §3.11–3.13](./08-engineering-practices-part3.md). Recover a commit with reflog; run `git bisect`; review an OSS PR with Google's guide. | 2 h |
| **7. GitHub Actions** | [§3.15](./08-engineering-practices-part3.md#315-github-actions). Lint → typecheck → test → build. Read the checkout v7 `pull_request_target` note. | 2 h |
| **8. Docker** | [§3.16](./08-engineering-practices-part3.md#316-docker-layers-multi-stage-compose). Multi-stage, non-root, Compose template (don't collide with your existing Postgres/Redis ports). | 2 h |
| **9. Monorepo, flags, lint, ADRs** | [§3.14, 3.17–3.19](./08-engineering-practices-part3.md). `packages/types` between web and API; one flag; one ADR. | 2 h |
| **10. XSS, CSRF, CORS, injection** | [Part 4 §3.20–3.22](./08-engineering-practices-part4.md). Exploit `dangerouslySetInnerHTML`; `$ne` test; explain `SameSite=Lax` limits. | 3.5 h |
| **11. OWASP 2025, secrets, headers** | [§3.23–3.27](./08-engineering-practices-part4.md#323-owasp-top-102025-and-api-top-102023). Recite 2025 one-liners. Rotate-a-secret dry run. | 2.5 h |
| **12. SLOs, Sentry, a11y, budgets** | [§3.28–3.30](./08-engineering-practices-part4.md#328-slis-slos-and-sentry). Write one SLO; init Sentry 11; axe the checkout; a bundle budget. | 2.5 h |
| **13. Interview questions** | Answer every [question](#9-interview-questions) out loud in ≤ 2 minutes. | 2.5 h |
| **14. Revise** | [Quick Revision Summary](#11-quick-revision-summary) at +1 day, +1 week, the day before. | 1 h |

```mermaid
flowchart LR
    A[Self-assess 0.5 h] --> B[SOLID 3.5 h] --> C[Clean/hex 2 h]
    C --> D[Trophy+Vitest 3 h] --> E[RTL/MSW/PW 4.5 h] --> F[k6 0.5 h]
    F --> G[Git 2 h] --> H[Actions 2 h] --> I[Docker 2 h] --> J[Mono/flags 2 h]
    J --> K[XSS/CSRF 3.5 h] --> L[OWASP 2.5 h] --> M[SLO/a11y 2.5 h]
    M --> N[Qs 2.5 h] --> O[Revise 1 h]
```

> 💡 Interview Tip: Steps 10–11 are the discriminator on security. Everyone has used Helmet. Few candidates can name A03 in *2025* and show a `$ne` test.

---

## 8. Hands-on Practice

| # | Exercise | Level | Acceptance criteria |
|---|----------|:-----:|---------------------|
| 1 | **Debounce lab** — [Part 2](./08-engineering-practices-part2.md#36-vitest-5-units-mocks-fake-timers) helper with Vitest 5 fake timers | 🟢 Easy | Three rapid calls → one fire at 200 ms; `clearMocks` default does not break the spy; Node 22.12+ |
| 2 | **Trophy audit** — classify every test in a real repo | 🟢 Easy | A table: static / unit / integration / E2E. You delete or rewrite one test that mocked the thing under test |
| 3 | **MSW 3 page test** — notes list with `http`/`HttpResponse` from `msw/http` | 🟡 Medium | Query by role; `findBy` for async; `onUnhandledFrame` fails the test on stray requests; no mocked React Query |
| 4 | **Playwright journey** — login → create item → logout | 🟡 Medium | Locators by role/label; `storageState` reused; trace on retry; CI job uses `npx playwright install --with-deps` |
| 5 | **Reflog + bisect** | 🟡 Medium | You "lose" a commit with a rebase, recover it from reflog onto a new branch; `git bisect` finds a planted `throw` in ≤ log₂(n) steps |
| 6 | **Review an OSS PR** using Google's guide | 🟡 Medium | Written notes: one blocking issue (or explicit "none"), two nits, PR-size verdict, a security look (authz, XSS, secrets) |
| 7 | **CI pipeline** — lint → `tsc --noEmit` → Vitest → build | 🟡 Medium | `actions/checkout@v7` + `actions/setup-node@v7`; npm cache; concurrency group; no `pull_request_target` |
| 8 | **Multi-stage image + Compose template** | 🟡 Medium | Non-root `USER`; `npm ci --omit=dev`; `.dockerignore` excludes `node_modules`; Compose Postgres+Redis on **non-default ports** if 5432/6379 are taken |
| 9 | **Injection + XSS** — `$ne` login bypass and a CSP | 🔴 Hard | `unsafeFind` vs `safeFind` tests pass as in [Part 4](./08-engineering-practices-part4.md#322-injection-sql-nosql-command); a toy `dangerouslySetInnerHTML` payload is blocked by CSP (`script-src 'self'`, no `'unsafe-inline'`) |
| 10 | **Release bar** — SLO + axe + bundle budget | 🔴 Hard | Written SLO (SLI, target, window, error-budget action); `@axe-core/playwright` fails on serious issues for checkout; `size-limit` (or equivalent) fails a PR that adds > the budget |

---

## 9. Interview Questions

### Basic

#### Q1. Recite SOLID without animals. Point at a TypeScript service.

**Model answer.** SRP: one *axis of change* — tax math isn't the same reason to change as persistence. OCP: unions + exhaustive `switch` (or a Strategy map) instead of a growing `if`. LSP: a cache decorator that returns `null` on Redis-down must match the documented miss contract, not swallow errors as empty lists unless that's the contract. ISP: readers shouldn't depend on `chargeCard`. DIP: `checkout` takes `OrderRepo`, not `pg.Pool`; tests inject `InMemoryRepo`. The [Part 1 checkout](./08-engineering-practices-part1.md#31-solid-in-typescript) is the example.

**Follow-ups:** Is a 400-line `UserService` an SRP violation?

**Great answer includes:** Axis of change, not "one class"; `createApp({ repo })` as DIP.

#### Q2. Name three patterns you already ship, and one you refuse.

**Model answer.** Express middleware = Chain of Responsibility. Prisma/S3 behind `NotesRepo`/`BlobStore` = Adapter. Tax/hasher = Strategy. `EventEmitter` = Observer. I refuse **Singleton as a bag of request state** (`Session.currentUser`) — races under concurrency. A module-level `pg.Pool` is a process resource, not the GoF Singleton party trick.

**Follow-ups:** Is React Context Observer?

**Great answer includes:** Smell column from [§3.2](./08-engineering-practices-part1.md#32-design-patterns-you-already-use); "function as Strategy".

#### Q3. Pyramid vs trophy — which tests would you add to a notes app?

**Model answer.** Static: `tsc`, lint. Units: slugify, debounce, pricing. Integration: Supertest against `createApp` with in-memory repo *and* one Testcontainers path for SQL; RTL+MSW for the notes page. E2E: one Playwright login→create→logout. I would **not** E2E every button or unit-test `useState`.

**Follow-ups:** Where do you mock?

**Great answer includes:** Mock across a network/process boundary; never mock the unit under test.

#### Q4. How do you test a debounced function?

**Model answer.** Vitest fake timers: call three times, `advanceTimersByTime(199)` → not called, `+1ms` → once. Restore real timers. Verified on Vitest 5.0.4.

**Follow-ups:** What did Vitest 5 change about mocks?

**Great answer includes:** `clearMocks` default on; `vi.mock` top-level only.

#### Q5. Why query by role in RTL?

**Model answer.** `getByRole('button', { name: /save/i })` fails when the control isn't a button or has no accessible name — the test is also an a11y check. `getByTestId` / class selectors survive inaccessible UI.

**Follow-ups:** `getBy` vs `findBy` vs `queryBy`?

**Great answer includes:** `findBy` for async appearance; `queryBy` for absence; details in [04](./04-react-part2.md#310-testing-react).

#### Q6. Trunk-based vs GitFlow — when is GitFlow justified?

**Model answer.** Trunk-based: short-lived PRs onto `main`, flags for incomplete work, many deploys/day. GitFlow (`develop`/`release`/`hotfix`) fits versioned products with a freeze. For a Next SaaS, GitFlow's failure mode is hotfixes missing `develop`.

**Follow-ups:** How do you ship a half-done feature on trunk?

**Great answer includes:** Feature flags; PR size; not a week-long branch.

#### Q7. Rebase or merge?

**Model answer.** Rebase **local feature branches** onto `main` to keep the PR linear; squash-merge (or merge commit — pick a policy) onto `main`. Never rebase commits others have pulled; never force-push `main`. `--force-with-lease` if you must rewrite a feature branch.

**Follow-ups:** What does interactive rebase do for reviewers?

**Great answer includes:** Squash `wip`; one idea per commit; reflog if it goes wrong.

#### Q8. What is `git reflog` for?

**Model answer.** Local history of `HEAD`. After a bad rebase, `git reflog` still has the old SHA; `git checkout -b recover <sha>`. It is per-clone and expires. Not a substitute for `git push`.

**Follow-ups:** Bisect?

**Great answer includes:** Binary search; `git bisect run npm test`.

#### Q9. Image vs container vs layer.

**Model answer.** Image = immutable snapshot + metadata + default CMD. Container = instance with a writable layer. Layer = one Dockerfile instruction; cache hits when it and every parent are unchanged. That's why `COPY lockfile` + `npm ci` come before `COPY src`.

**Follow-ups:** Why multi-stage?

**Great answer includes:** Drop compilers and devDependencies; non-root `USER`; smaller pull/attack surface.

---

### Intermediate

#### Q10. Stub vs mock vs fake vs spy.

**Model answer.** Fowler: dummy fills an unused arg; stub returns canned data; spy records calls (often wrapping real); mock is a pre-programmed *expectation* (overuse → brittle); fake is a working lightweight impl (`InMemoryNotesRepo`). I write fakes and stubs; I spy at boundaries; I rarely use mock-style `expect(mailer.send).toHaveBeenCalled` as the *only* assertion.

**Follow-ups:** When is TDD the wrong tool?

**Great answer includes:** CSS, exploratory UI; characterization tests for legacy.

#### Q11. MSW 3 vs mocking `fetch`.

**Model answer.** MSW intercepts the network so the real client (React Query, `api.ts`) runs. v3 is ESM-only, Node 22+, `import { http, HttpResponse } from 'msw/http'`, `setupServer` from `msw/node`. Mocking `fetch` couples tests to an implementation you might replace with `axios`.

**Follow-ups:** GraphQL?

**Great answer includes:** `msw/graphql`; `onUnhandledFrame`.

#### Q12. Playwright auth without logging in every spec.

**Model answer.** `globalSetup` logs in once, saves `storageState` (cookies + localStorage), specs reuse it. Locators by role/label. CI: `npx playwright install --with-deps`, `trace: 'on-first-retry'`, upload the HTML report on failure.

**Follow-ups:** Why not E2E the whole app?

**Great answer includes:** Cost and flakes; trophy.

#### Q13. What do you look for in a PR?

**Model answer.** User-visible correctness, **authz in the data layer**, tests that would fail if the behavior broke, migrations (expand/contract), secrets, XSS sinks, unbounded lists. Style last. I reject 1,800-line mixed refactor+feature PRs — split them. Feedback: `blocking:` vs `nit:`, comments on the code.

**Follow-ups:** How big should a PR be?

**Great answer includes:** Hundreds of lines of *meaningful* diff; Google eng-practices.

#### Q14. Sketch CI for a Next app.

**Model answer.** `pull_request` + `push` to `main`. Job: checkout@v7, setup-node@v7 (Node 24, cache), `npm ci`, lint, `tsc --noEmit`, Vitest, build. E2E on `main` (or a label). Deploy is a separate job with an **environment**, `id-token: write` for OIDC — no long-lived AWS keys in secrets if we can avoid them. Concurrency group cancels stale PR runs.

**Follow-ups:** Why is `pull_request_target` dangerous?

**Great answer includes:** Base-repo secrets + executing fork code = pwn request; v7 blocks fork checkout by default.

#### Q15. How do you share types between a Next app and an API?

**Model answer.** pnpm workspace `packages/types` (Zod schemas). Both apps depend with `workspace:*`. Turborepo `build.dependsOn: ["^build"]` so types emit first. Not copy-paste DTOs; not a private npm publish you forget.

**Follow-ups:** Turborepo vs Nx?

**Great answer includes:** Turbo = task graph + cache on pnpm; Nx = generators, boundaries, heavier.

#### Q16. Feature flags — kinds and a trap.

**Model answer.** Fowler: release, experiment, ops (kill switch), permission. Trap: flags that live forever become a second product. Interface `isOn(key, ctx)` so tests inject; env in dev, LaunchDarkly/Unleash in prod. Roll out 1% → SLO → 100% → **delete**.

**Follow-ups:** Flag vs branch?

**Great answer includes:** Trunk-based; incomplete work on `main`.

#### Q17. XSS types and the actual fix.

**Model answer.** Stored / reflected / DOM. React encodes JSX text; holes are `dangerouslySetInnerHTML`, `javascript:` URLs, server HTML concat. Fix: encode in context, sanitizer only with a tight allow-list, CSP without `'unsafe-inline'` on scripts.

**Follow-ups:** Does Helmet fix XSS?

**Great answer includes:** Helmet is headers; CSP is depth; encoding is the fix.

#### Q18. When is `SameSite=Lax` not enough against CSRF?

**Model answer.** Cross-site POSTs from other sites are blocked. Not enough for: state-changing **GET**; attackers on a **subdomain**; old browsers. Cookie sessions still want a CSRF token (or don't use cookies for the mutating API — Bearer in `Authorization` isn't auto-attached).

**Follow-ups:** Is CORS a CSRF defense?

**Great answer includes:** CORS is a browser read restriction; `curl` ignores it; authz is server-side.

#### Q19. Show a NoSQL injection.

**Model answer.** Body `{ "email": { "$ne": null } }` passed as a Mongo filter matches every document with a non-null email — login bypass. Vitest 5.0.4: `unsafeFind` returned 2 users; `safeFind` requires a string. Fix: Zod parse; never spread `req.body` into `find`.

**Follow-ups:** SQL equivalent?

**Great answer includes:** Parameterized `$1`; tagged `$queryRaw`; [07](./07-databases-and-apis.md).

#### Q20. What did OWASP Top 10 change in 2025?

**Model answer.** A01 still broken access control — **SSRF and CSRF folded in**. A02 misconfiguration climbed. **A03 is Software Supply Chain Failures** (not injection). Injection is **A05**. **A10 is new: Mishandling of Exceptional Conditions** (fail-open, leaky 500s). Reciting 2021 numbers is a miss.

**Follow-ups:** API Top 10 item #1?

**Great answer includes:** BOLA; 404 not 403 for other tenants; [06](./06-nodejs-part3.md#323-security).

---

### Advanced

#### Q21. Hexagonal architecture — prove you use it.

**Model answer.** Domain in the middle; ports are interfaces (`OrderRepo`); adapters are Postgres/HTTP/queue. Proof is `createApp({ repo: new InMemoryNotesRepo() })` in tests — not a slide. The [06 notes service](./06-nodejs-part2.md) is a small hexagon.

**Follow-ups:** Bounded context vs module?

**Great answer includes:** "Order" in checkout ≠ warehouse; ubiquitous language.

#### Q22. How do you stop flaky tests?

**Model answer.** Causes: time, order, network, asserting before the UI settles, retries that hide races. Fake timers *or* Playwright `expect`; isolate DB state; MSW/Testcontainers; `findBy` / web-first assertions; traces on retry. Quarantine is a ticket, not a strategy. I don't raise `retries: 3` and walk away.

**Follow-ups:** Vitest 5 concurrency?

**Great answer includes:** Tests must be isolated; shared module state is the flake.

#### Q23. Design a progressive rollout with an SLO.

**Model answer.** SLI: fraction of `POST /v1/checkout` with status < 500 and latency < 300 ms, 30-day window. SLO: 99.9%. Error budget 0.1%. Flag at 1% → watch burn rate → 10/50/100 → delete flag. If budget is exhausted, freeze features. Alert on burn, not a single 500. Sentry 11 for the exception cluster; RED metrics in [06](./06-nodejs-part3.md#321-observability-traces-metrics--health-checks).

**Follow-ups:** 100% SLO?

**Great answer includes:** No error budget; you'll never ship.

#### Q24. Sentry 11 vs OpenTelemetry in the same Node process.

**Model answer.** v11 owns native Sentry spans and **does not** register an OTel provider by default (`enableOpenTelemetrySetup` replaced `skipOpenTelemetrySetup`; default off except Next/SvelteKit SDKs). If 06-style OTel already traces, keep Sentry OTel setup off, unset `tracesSampleRate`, add `openTelemetryIntegration()` so errors join the active span. Two providers = duplicate or missing spans.

**Follow-ups:** PII?

**Great answer includes:** `sendDefaultPii: false`; hash user ids.

#### Q25. Supply-chain (A03) for a Node app in CI.

**Model answer.** Lockfile + `npm ci`; Docker `--ignore-scripts` unless native addons; Dependabot; pin Actions majors (SHA for high-sensitivity); no `curl | bash`. `pull_request` to run untrusted PR code **without** secrets. checkout v7 blocks fork checkout on `pull_request_target`. Rotate leaked tokens *before* rewriting git history.

**Follow-ups:** `npm audit` as a gate?

**Great answer includes:** Signal, not policy; reachability; don't block on noise.

#### Q26. Multi-stage Dockerfile — walk through cache invalidation.

**Model answer.** `deps` stage: copy lockfile, `npm ci --omit=dev`. `build` stage: full `npm ci`, `tsc`. Runtime: copy prod `node_modules` + `dist`, `USER node`, exec-form `CMD ["node", "dist/main.js"]` so SIGTERM hits PID 1 ([06 shutdown](./06-nodejs-part3.md#322-graceful-shutdown)). Changing `src` does **not** bust the deps layer. `.dockerignore` `node_modules`. Alpine's `node` user already exists.

**Follow-ups:** Type-stripping instead of `tsc`?

**Great answer includes:** Node 24 can `CMD ["node", "src/main.ts"]` as in 06; emit when you need a compile gate.

#### Q27. Accessibility as a release bar, not a workshop.

**Model answer.** WCAG 2.2 AA. Component rules in [04 §3.8](./04-react-part2.md#38-accessibility-in-react). Gate: axe on Playwright journeys (fail serious+); RTL by role; keyboard pass of checkout; one design-system Dialog that traps focus. axe won't catch wrong focus after save — that's the human pass.

**Follow-ups:** Div onClick?

**Great answer includes:** Not focusable; no role; fail `getByRole('button')`.

#### Q28. Performance budgets vs Core Web Vitals.

**Model answer.** CWV mechanics (LCP/INP/CLS) are [05](./05-nextjs-part3.md#316-core-web-vitals). Practice: **lab budgets in CI** (route JS bytes, Lighthouse CI on preview) to block regressions; **field RUM** to know the truth. A Lighthouse 100 with 4 s field LCP means the lab isn't your users. k6 p95 on the API is the backend twin.

**Follow-ups:** Who owns a failed budget?

**Great answer includes:** Conversation or revert; not a silenced check.

#### Q29. ESLint 10 vs Biome 2.5.

**Model answer.** ESLint 10 is flat config only — `eslint.config.js`, `.eslintrc` dead. Biome lints and formats in one binary; new repos often skip Prettier. Keep ESLint when you need `jsx-a11y` / security plugins. Don't double-format. Pre-commit `lint-staged` is convenience; CI is the gate (`--no-verify` exists).

**Follow-ups:** Why still typecheck in CI if ESLint has type-aware rules?

**Great answer includes:** `tsc --noEmit` is the source of truth for types.

#### Q30. Write an ADR in 60 seconds.

**Model answer.** Title, status, date, context, decision, consequences. Example: "Postgres source of truth, Redis cache-aside" — backup story vs invalidation cost. Not "we use TypeScript". Store in `docs/adr/`; status can become Superseded.

**Follow-ups:** ADR vs README?

**Great answer includes:** ADRs are a timeline of *choices*; README is how to run it.

---

### Tricky

#### Q31. "A03 is injection, right?"

**Model answer.** In **2021**, yes. In **2025**, A03 is **Software Supply Chain Failures**. Injection moved to **A05**. SSRF is under **A01**. If the interviewer is on 2021, I'll name both editions. Reciting the old list as current is the trick.

**Follow-ups:** What's new as A10?

**Great answer includes:** Mishandling of Exceptional Conditions; fail closed; generic 500s.

#### Q32. `Access-Control-Allow-Origin: *` with cookies.

**Model answer.** Spec-invalid with `Access-Control-Allow-Credentials: true`; browsers refuse. Reflecting the request `Origin` with credentials means **any website** can invoke the API as the user. CORS still isn't authz — a non-browser client ignores it.

**Follow-ups:** Simple vs preflight?

**Great answer includes:** Custom headers / JSON trigger OPTIONS; don't "fix" prod by echoing any origin.

#### Q33. `pull_request_target` + `ref: github.event.pull_request.head.sha` + `npm test`.

**Model answer.** Classic pwn request: workflow and secrets from the **base** repo, code from the **fork**. `npm test` runs attacker scripts with your AWS role. **checkout v7 refuses** that fork checkout unless `allow-unsafe-pr-checkout: true`. Correct shape: `pull_request` for tests (no secrets), or inspect fork code as data without executing it.

**Follow-ups:** `workflow_run` after a PR?

**Great answer includes:** Same class if it checks out the PR head with base secrets.

#### Q34. Returning 403 when Bob requests Alice's note by id.

**Model answer.** Confirms the id exists (BOLA / user enumeration). Return **404**. Filter `WHERE id = $1 AND owner_id = $2` in the **data layer**, not only in middleware that some worker forgets. Tested in [06](./06-nodejs-part3.md#324-testing-node-apis).

**Follow-ups:** GraphQL?

**Great answer includes:** Field-level auth; don't leak via error messages.

#### Q35. CSP with `'unsafe-inline'` on `script-src`.

**Model answer.** You kept the header and lost the XSS depth charge: injected `<script>…</script>` still runs. Use nonces/hashes (Next can emit them) or no inline scripts. `'unsafe-inline'` on `style-src` is a smaller, still-real issue (CSS injection / data exfil in some browsers).

**Follow-ups:** `dangerouslySetInnerHTML` + CSP?

**Great answer includes:** CSP is defense in depth; don't ship the sink.

#### Q36. Fake timers leaked into a Playwright test.

**Model answer.** Vitest `useFakeTimers()` without `useRealTimers()` in `finally` makes later tests hang on real `fetch`/Playwright waits until timeout — "flaky CI, green locally" if local files didn't share the worker. Isolate; don't mix fake clocks with real network. Vitest 5's `clearMocks` does **not** restore the clock.

**Follow-ups:** `Temporal`?

**Great answer includes:** Vitest 5 fake timers also mock `Temporal`.

---

## 10. Common Mistakes & Red Flags

| Red flag | Why it hurts | Say/do instead |
|----------|--------------|----------------|
| Reciting SOLID with `Animal`/`Shape` | Signals no production use | Checkout / `createApp({ repo })` |
| "We have 80% coverage" | Vanity; untested payments | Behavior on critical paths |
| Mocking Prisma to "unit test" SQL | Tests the mock | Testcontainers / [06](./06-nodejs-part3.md#324-testing-node-apis) |
| `getByTestId` everywhere | Survives inaccessible UI | `getByRole` |
| GitFlow on a SaaS that deploys hourly | Diverging `develop` | Trunk + flags |
| Force-push `main` | Rewrites shared history | `--force-with-lease` on *feature* branches only |
| 2,000-line PR "it's all related" | Unreviewable | Split refactor vs feature |
| `pull_request_target` to "get secrets on fork PRs" | Pwn request | `pull_request` without secrets |
| Root user in Docker, `npm install` in the image | Supply chain + privilege | `npm ci --omit=dev`, `USER node` |
| "Helmet so we're secure" | Headers ≠ A01 | BOLA tests, CSP, parameterized queries |
| OWASP 2021 numbers in 2026 | A03 isn't injection anymore | 2025 list |
| `SameSite=Lax` as a complete CSRF story | GETs / subdomains | Token or Bearer |
| CORS as a server firewall | `curl` ignores it | Authz every request |
| Spreading `req.body` into `find()` | `$ne` / `$gt` login bypass | Zod strings |
| 403 on other-tenant ids | Confirms existence | 404 + data-layer filter |
| 100% SLO | No error budget | 99.9% and a freeze policy |
| Quarantine + `retries: 3` forever | Flakes go to prod | Trace, then time/order/network |
| axe-only a11y | Misses focus bugs | Keyboard pass + design system |
| Lighthouse-only performance | Lab ≠ field | Budgets in CI **and** RUM |

---

## 11. Quick Revision Summary

### One-page recap

**Design**
- SOLID is axes of change + DIP via `createApp({ repo })`. Patterns: name them in Express, Prisma, React; Singleton only for process resources.
- Smells → extract with tests; never mix refactor and feature in one PR.
- Hexagon: ports in the domain, adapters at the edge; DDD words (bounded context, aggregate, domain event).

**Testing**
- Trophy: static + some units + many integration (RTL+MSW, Supertest, Testcontainers) + few Playwright journeys.
- Vitest 5: Node 22.12+, `clearMocks` on, top-level `vi.mock`, fake timers (+ `Temporal`).
- MSW 3: `msw/http`. Playwright: `storageState`, traces. Doubles per Fowler. Flakes have causes.

**Shipping**
- Trunk-based + flags. Rebase locally, squash onto `main`. Bisect, reflog, `--force-with-lease`.
- Review: authz, tests, size. GHA: checkout **v7** / setup-node **v7**, cache, environments, OIDC. v7 blocks fork checkout on `pull_request_target`.
- Docker: layer order, multi-stage, non-root, exec-form CMD. pnpm workspaces + Turborepo `^build`. ESLint 10 flat / Biome 2.5. ADRs for choices.

**Security & ops**
- XSS: encode + CSP. CSRF: cookies ⇒ token/`SameSite` limits; Bearer ≠ CSRF. CORS ≠ authz.
- Injection: `$1` and Zod; `$ne` demo. OWASP **2025**: A03 supply chain, A05 injection, A10 fail-closed, SSRF in A01. API1 BOLA → 404.
- Secrets rotate first. Headers from MDN, not "Helmet". Node SSRF/pollution/ReDoS → [06](./06-nodejs-part3.md#323-security).
- SLI/SLO/error budget; Sentry 11 native spans (don't double OTel). a11y = AA + axe CI + role queries. Perf = CI budgets + field RUM; CWV in [05](./05-nextjs.md).

### Last-day checklist

- [ ] I can refactor a god `checkout` and name SRP + DIP in the diff.
- [ ] I can place a test on the trophy and say what I would *not* mock.
- [ ] I can debounce with fake timers and explain Vitest 5 `clearMocks`.
- [ ] I can recover a "lost" commit with reflog and sketch `git bisect`.
- [ ] I can explain checkout v7 vs `pull_request_target`.
- [ ] I can walk a multi-stage Dockerfile's cache.
- [ ] I can name OWASP 2025 A03 and A10 correctly.
- [ ] I can demo `{ email: { $ne: null } }` and the Zod fix.
- [ ] I can say when `SameSite=Lax` is not enough, and why CORS isn't a firewall.
- [ ] I can define an SLI/SLO/error budget and say what happens when the budget is gone.
- [ ] I can answer Q31–Q36 cold.

---

## Next Steps

- Update your Engineering Practices rows in the [Progress Tracker](./00-README.md#progress-tracker).
- Keep the Vitest 5 debounce + `$ne` tests as a sandbox; re-run them after a Vitest upgrade.
- ➡️ Continue to [09-system-design.md](./09-system-design.md) — capacity, the building blocks behind flags/rollouts/SLOs, and classic design prompts. This file stopped at how you *ship and secure* a service; 09 is how you *shape* it.
