# 08 — Engineering Practices

> This topic is split into five parts. Start with Part 1 and follow the "Next" links. Applies to **Vitest 5.0** (verified 5.0.4; Node ≥ 22.12, Vite ≥ 6.4 peer), **Playwright 1.64**, **MSW 3.0** (`msw/http`), **ESLint 10** (flat config only), **Biome 2.5**, **Turborepo 2.11**, **GitHub Actions** `actions/checkout@v7` + `actions/setup-node@v7`, **`@sentry/node` 11**, **OWASP Top 10:2025** (API Top 10 still **2023**). Node stays on **24 LTS**. Debounce (fake timers) and NoSQL `$ne` tests were run on Vitest 5.0.4 in October 2026. Check each project's changelog before you quote a default.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — SOLID, Patterns, Clean Code & Architecture](./08-engineering-practices-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.4 | SOLID on a checkout service, patterns you already ship, smells/refactoring, hexagonal + DDD vocabulary |
| [Part 2 — Testing](./08-engineering-practices-part2.md) | 3.5–3.10 | Pyramid vs trophy, Vitest 5, RTL (details in 04), MSW 3, Playwright, doubles, flakes, k6/Pact skim |
| [Part 3 — Git, CI/CD, Docker, Monorepos](./08-engineering-practices-part3.md) | 3.11–3.19 | Trunk-based vs GitFlow, rebase/bisect/reflog, review, flags, GitHub Actions, multi-stage Docker, pnpm + Turborepo, ESLint 10 / Biome, ADRs |
| [Part 4 — Security, Observability, Accessibility](./08-engineering-practices-part4.md) | 3.20–3.30 · 4. Full Example · 5. Diagrams Index | XSS, CSRF/CORS, injection (`$ne`), OWASP 2025 + API 2023, secrets, headers, SLOs/Sentry, a11y as a gate, performance budgets |
| [Part 5 — Resources, Practice, Interview Questions & Revision](./08-engineering-practices-part5.md) | 6–11 | Curated resources, a ~34 h learning path, 10 graded exercises, 36 interview questions with model answers, red flags, one-page recap and last-day checklist |

> 💡 Interview Tip: Name the *edition*. "OWASP A03 is injection" is 2021. In 2025 A03 is **Software Supply Chain Failures**, injection is A05, SSRF sits under A01, and A10 is **Mishandling of Exceptional Conditions**. `actions/checkout@v7` refuses fork checkouts on `pull_request_target` — that is a 2026 interview question, not trivia.

## Related Files

- React Testing Library queries-by-role, component a11y → [04-react](./04-react.md) ([§3.8](./04-react-part2.md#38-accessibility-in-react), [§3.10](./04-react-part2.md#310-testing-react))
- Core Web Vitals mechanics, Next Dockerfile template → [05-nextjs](./05-nextjs.md) ([§3.16](./05-nextjs-part3.md#316-core-web-vitals))
- Pino/OTel internals, Node SSRF/prototype pollution/ReDoS, Supertest + Testcontainers, notes-service Dockerfile → [06-nodejs](./06-nodejs.md)
- Parameterized SQL, expand/contract migrations, idempotency → [07-databases-and-apis](./07-databases-and-apis.md)
- Capacity, rollouts at system-design granularity → [09-system-design.md](./09-system-design.md)
- Deploy jobs, OIDC to AWS, EC2/ECS → [10-deployment-aws-ec2.md](./10-deployment-aws-ec2.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./08-engineering-practices-part1.md), then continue to [09-system-design.md](./09-system-design.md).
