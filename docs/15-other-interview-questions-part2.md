# 15 — Behavioral & Career (Part 2 of 3): Deep-Dive, Incidents, Product & Questions You Ask

> **Parts:** [Part 1 — Pitch & STAR](./15-other-interview-questions-part1.md) · **Part 2 — Deep-Dive, Incidents, Product, Questions** · [Part 3 — Resume, Negotiation, Leadership, Interview](./15-other-interview-questions-part3.md)
>
> Deep-dive is a **system-design interview about work you actually shipped**. Use [09](./09-system-design.md) for the drawing language, not as a fake design. Incidents: [Google SRE Workbook / Book — postmortem culture](https://sre.google/books/). Do not dump SLO definitions here ([08](./08-engineering-practices-part4.md#328-slis-slos-and-sentry)). Questions to ask: [TIH final questions](https://www.techinterviewhandbook.org/final-questions/).

## Table of Contents

- [3. Detailed Explanations (Part 2)](#3-detailed-explanations-part-2)
  - [3.5 Project Deep-Dive](#35-project-deep-dive)
  - [3.6 Debugging & Production Incidents](#36-debugging--production-incidents)
  - [3.7 Product Sense: "Improve This App"](#37-product-sense-improve-this-app)
  - [3.8 Questions to Ask](#38-questions-to-ask)
- [Next: Part 3](#next-part-3)

---

## 3. Detailed Explanations (Part 2)

### 3.5 Project Deep-Dive

**Prompt.** "Walk me through a project on your resume." You get **8–15 minutes** plus 5 levels of why. Pick the **impact** story ([Part 1](./15-other-interview-questions-part1.md#33-story-bank-eight-slots)) that you can draw.

**Spine (same boxes as [09](./09-system-design-part1.md), but facts not Fermi):**

1. **Users and constraint.** Who, how many, what hurts if it is down.
2. **Picture.** Clients → edge ([12](./12-cloudflare.md) / [11](./11-deployment-aws-s3.md)) → app ([10](./10-deployment-aws-ec2.md) / [05](./05-nextjs.md)) → data ([07](./07-databases-and-apis.md)). Your **bold** pieces.
3. **Your role.** IC vs lead vs "I wrote the worker." Lying about scope dies in follow-ups.
4. **Hard part.** One: uploads, auth, fan-out, migrations, p95, cost.
5. **Trade-off.** What you did *not* do (and the number that justified it).
6. **What you'd change.** 10× traffic, or "I'd add OAC / I'd not have used Flexible SSL." This is the senior tell.

**Five whys (prepare).** Why this store? Why this queue? Why this SLO? Why not serverless? Why that failure mode is acceptable?

**Numbers they believe.** QPS you measured, p95 you owned, table size, $ you moved, people on-call. If you don't remember, say the **order of magnitude** and that you'd check Grafana — better than three fake decimal places ([09](./09-system-design-part1.md) Fermi hygiene).

> ⚠️ Pitfall: Touring every microservice. One path, one bottleneck, one regret.

### 3.6 Debugging & Production Incidents

**Prompt.** "Tell me about a production issue." They want **method**, not heroics. Write **one blameless postmortem** from a real event before the loop ([SRE book — postmortem culture](https://sre.google/sre-book/postmortem-culture/), and the [SRE workbook](https://sre.google/workbook/blameless-postmortem/) if you want the template).

**Tell it in this order:**

| Beat | Content |
|------|---------|
| Detect | Who paged, what SLI moved ([08](./08-engineering-practices-part4.md#328-slis-slos-and-sentry), [06](./06-nodejs.md) RED) |
| Impact | Users / $ / duration — "checkout 5xx for 18 min, ~12k requests" |
| Mitigate | What you did **first** (rollback, flag, scale) before root cause |
| Diagnose | Logs → trace → one hypothesis you **killed** |
| Cause | Mechanism (not "Kubernetes was sad") |
| Fix that stays | Test, alert, runbook, ownership |
| Learn | What *you* missed; no teammate as villain |

**Debug method (live "how would you debug X").** Reproduce or capture. Bisect time (last deploy, flag). Split: client vs edge vs app vs DB. One change at a time. Write the timeline.

**EXAMPLE shape (replace):** "CF-Cache-Status HIT on `/account` after a Cache Everything rule ([12](./12-cloudflare.md)). Rolled the rule back in 4 minutes; then Cache Rule bypass `/api` and auth HTML. Added a check: HIT on `Set-Cookie` pages fails CI. I had approved the rule without reading 'eligible for cache'."

> 💡 Interview Tip: "I don't know yet" plus the **next instrument** is a hire. Guessing the root cause in sentence one is not.

### 3.7 Product Sense: "Improve This App"

**Prompt.** "How would you improve Instagram / our dashboard / this checkout?" You are not the PM. You are an engineer who can **see users, performance, reliability, a11y, cost**.

**3-app drill** (pick apps you actually use; 15 min each, notes only):

1. **Who and job.** Primary user, critical path.
2. **Four lenses** (say which you pick for *this* company):
   - **Performance** — LCP/INP ([05](./05-nextjs.md)); what you'd measure.
   - **UX / a11y** — keyboard, empty/error ([04](./04-react-part3.md), [08](./08-engineering-practices-part4.md#329-accessibility-as-a-release-practice)).
   - **Reliability** — single region, no `/readyz`, uploads through Node.
   - **Cost** — egress, NAT, polling vs WS.
3. **One bet.** 2-week slice, success metric, risk.
4. **What you would not do.** Rewrite, new framework, "AI" with no job-to-be-done.

They may ask first-day / first-six-months. Answer: **instrument and users first**, then one bet from the above — not "rewrite in Rust."

### 3.8 Questions to Ask

[TIH — final questions](https://www.techinterviewhandbook.org/final-questions/). Zero questions reads as zero interest. Bring **five**, use **two** that you could not Google.

**By stage**

| Stage | Ask | Avoid |
|-------|-----|-------|
| Recruiter | Loop shape, levels, timeline, remote, **comp process** if they open it | Bashing current employer |
| Engineer | What paged last month; deploy to prod; test/a11y bar; biggest tech debt | "What's your stack?" they already said |
| Hiring manager | Success at 6 months; how IC vs staff time splits; how disagreement with PM works | "How fast to promo?" as first question |
| Skip / exec | Why this team exists in 18 months; failure mode they fear | Pitching your side project |

**High-signal examples**

- "What broke in production last quarter, and what changed after?"
- "When product and eng disagree on a date, who actually decides?"
- "What does on-call look like for this team — load, compensation, whether ICs own the SLO?"
- "If I did this job well, what would be true in six months that isn't true now?"
- "What do people who fail in this role usually miss?"

**Comp and time-off.** Fine with recruiter or after they ask *your* expectations ([Part 3](./15-other-interview-questions-part3.md#310-salary-negotiation)). Not the closer of a coding round.

> ⚠️ Pitfall: Asking only about WFH and promo. Mix **work reality** with **growth**.

---

## Next: Part 3

➡️ [Part 3 — Resume, Negotiation, Leadership, Interview](./15-other-interview-questions-part3.md): impact bullets, McKenzie/Qureshi negotiation, estimation pointer to 09, staff-shaped influence, ~15 h, 36 questions.
