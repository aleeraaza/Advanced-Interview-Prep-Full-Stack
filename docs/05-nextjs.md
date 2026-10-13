# 05 — Next.js

> This topic is split into four parts. Start with Part 1 and follow the "Next" links. Applies to **Next.js 16.4** with the App Router. Each section that differs between **Cache Components** (default for new apps since 16.4) and the **previous model** (most existing 14/15/16 codebases) shows both.

## Table of Contents

| Part | Sections | Covers |
|------|----------|--------|
| [Part 1 — Routing, Server Components, Rendering & Data](./05-nextjs-part1.md) | 1. Overview · 2. Topic Map · 3.1–3.6 Detailed Explanations | Version landscape 13.4 → 16.4, App vs Pages Router, file conventions, parallel + intercepting routes (modal), Server/Client boundary in Next, SSR/SSG/ISR/PPR in both models, data-fetching patterns and waterfalls, streaming, status codes and bots |
| [Part 2 — Caching, Server Actions, Route Handlers, Proxy, Auth, Env & Runtimes](./05-nextjs-part2.md) | 3.7–3.13 Detailed Explanations | The four previous-model caches, `'use cache'`/`cacheLife`/`cacheTag`, invalidation APIs and migration, secure Server Actions (notes app), Route Handlers (REST, webhooks, SSE), `proxy.ts` and CVE-2025-29927, auth with a Data Access Layer and Auth.js, env vars, Node vs Edge runtime |
| [Part 3 — Optimization, SEO, Web Vitals, Errors, Deployment & Full Example](./05-nextjs-part3.md) | 3.14–3.18 Detailed Explanations · 4. Full Example · 5. Diagrams Index | `next/image`/`font`/`script`, Metadata API and OG images, Core Web Vitals, error boundaries and `instrumentation.ts`, standalone Docker, the self-hosting checklist, adapters, security patching, and a full blog with optimistic comments |
| [Part 4 — Resources, Practice, Interview Questions & Revision](./05-nextjs-part4.md) | 6. Resources · 7. How to Learn It · 8. Hands-on Practice · 9. Interview Questions · 10. Common Mistakes · 11. Quick Revision | 20 curated resources, a ~29 h learning path, 10 graded exercises, 36 interview questions with model answers, red flags, one-page recap and last-day checklist |

> 💡 Interview Tip: All path-labelled code in Parts 1–3 was built together into one app with `next build` on 16.4 (Cache Components on, `strict` TypeScript) and exercised with `next start`. That included HTTP smoke tests (Proxy, APIs, webhooks, SSE, metadata, OG images, sitemap) and browser tests (Server Action forms, optimistic comments, the intercepted modal). Several "Pitfall" callouts are behaviors observed during those runs, not claims copied from the docs.

## Related Files

- React model behind all of this (RSC, Suspense, Actions, `<Activity>`) → [04-react Part 2](./04-react-part2.md)
- Typing `PageProps`, Route Handlers and env → [03-typescript Part 2](./03-typescript-part2.md)
- Node.js internals, auth flows (JWT, OAuth2, refresh tokens), observability → [06-nodejs.md](./06-nodejs.md)
- Databases, REST/GraphQL/tRPC, pagination, idempotency → [07-databases-and-apis.md](./07-databases-and-apis.md)
- Docker, CI/CD, monorepos, security practices → [08-engineering-practices.md](./08-engineering-practices.md)
- Self-hosting on EC2 with nginx/PM2 → [10-deployment-aws-ec2.md](./10-deployment-aws-ec2.md); S3 + CloudFront → [11-deployment-aws-s3.md](./11-deployment-aws-s3.md); Cloudflare → [12-cloudflare.md](./12-cloudflare.md)
- Compact revision → [17-cheatsheets.md](./17-cheatsheets.md)

## Next Steps

➡️ Start with [Part 1](./05-nextjs-part1.md), then continue to [06-nodejs.md](./06-nodejs.md).
