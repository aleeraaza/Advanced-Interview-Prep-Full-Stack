# 15 — Behavioral & Career (Part 1 of 3): 90-Second Pitch & STAR Bank

> **Parts:** **Part 1 — Pitch & STAR** · [Part 2 — Deep-Dive, Incidents, Product, Questions](./15-other-interview-questions-part2.md) · [Part 3 — Resume, Negotiation, Leadership, Interview](./15-other-interview-questions-part3.md)
>
> These are **your** stories. Do not invent metrics. Replace every `{{placeholder}}`. Formats: [Tech Interview Handbook — behavioral](https://www.techinterviewhandbook.org/behavioral-interview/), [self-introduction](https://www.techinterviewhandbook.org/self-introduction/). Amazon uses **16** [Leadership Principles](https://www.amazon.jobs/content/en/our-workplace/leadership-principles) as a **prompt list**, not a religion — map stories even if you never interview there. Estimation math stays in [09](./09-system-design-part1.md). SLOs/error budgets: [08](./08-engineering-practices-part4.md#328-slis-slos-and-sentry).

## Table of Contents

- [1. Overview](#1-overview)
- [2. Topic Map](#2-topic-map)
- [3. Detailed Explanations (Part 1)](#3-detailed-explanations-part-1)
  - [3.1 Tell Me About Yourself (90 seconds)](#31-tell-me-about-yourself-90-seconds)
  - [3.2 STAR (and what interviewers actually score)](#32-star-and-what-interviewers-actually-score)
  - [3.3 Story Bank: Eight Slots](#33-story-bank-eight-slots)
  - [3.4 Amazon Leadership Principles as Prompts](#34-amazon-leadership-principles-as-prompts)
- [Next: Part 2](#next-part-2)

---

## 1. Overview

**What this file covers.** The non-LeetCode loop: 90-second intro, a **reusable STAR bank**, a 10-minute project deep-dive, a blameless incident, product sense, questions *you* ask, resume bullets, negotiation, senior-scope signals.

**Why it fails seniors.** Strong code, vague stories: "we migrated to microservices" with no **your** action, no number, no conflict. Behavioral is a **competency interview**. They are hiring judgment.

| Junior | Senior |
|--------|--------|
| Chronological CV recitation, 4 minutes | 90 s: present role → two quantified beats → why *this* team |
| "We" the whole time | I owned X; the team did Y; I asked Z |
| "It went well" | p95, $ , weeks, error rate, people unblocked |
| One story stretched to every prompt | Eight labeled stories; you pick the closest |
| No questions at the end | Five prepared; two used |

> 💡 Interview Tip: Record the 90-second pitch. If you cannot say it walking, it is not ready. Cut adjectives first.

---

## 2. Topic Map

**Part 1 — Voice and the bank**
- [ ] 90-second intro — [3.1](#31-tell-me-about-yourself-90-seconds)
- [ ] STAR mechanics — [3.2](#32-star-and-what-interviewers-actually-score)
- [ ] Eight story slots — [3.3](#33-story-bank-eight-slots)
- [ ] LP mapping — [3.4](#34-amazon-leadership-principles-as-prompts)

**[Part 2](./15-other-interview-questions-part2.md)** — Project deep-dive, incidents, "improve this app," questions to ask.

**[Part 3](./15-other-interview-questions-part3.md)** — Estimation (points at 09), negotiation, resume, leadership, ~15 h path, 36 questions.

---

## 3. Detailed Explanations (Part 1)

### 3.1 Tell Me About Yourself (90 seconds)

Almost every loop starts here ([TIH self-introduction](https://www.techinterviewhandbook.org/self-introduction/)). It is **not** your life story. It is a trailer so they know which deep-dive to pull.

**Shape (3+ years, full-stack):**

1. **Present (15 s).** Role, domain, stack in *their* nouns if true (`Next.js`, payments, B2B).
2. **Past, two beats (50 s).** Each beat: problem → what *you* did → one number. School drops off unless it is the only signal.
3. **Why here (25 s).** One sentence on the team/product + one sentence on the gap you want (scope, domain, staff-shaped work). Not "I love your mission" with no evidence you read it.

**Template (fill, then time):**

> I'm a full-stack engineer with {{N}}+ years, currently {{title}} at {{company}}, mostly {{Node / Next / React}} in {{domain}}.  
> Last year I {{action}} on {{system}}, which {{metric: p95 / conversion / cost / incidents}}. Before that I {{action}} so {{metric}}.  
> I'm talking to you because {{specific team or problem}} and I want {{scope: own a surface, staff-shape, domain X}}.

**Cuts.** No hobby list unless they ask. No "passionate about code." No 2019 internship. If they already have the resume, **do not read it**.

**Why this company.** Recruiter vs hiring manager: recruiter gets logistics + excitement; HM gets *product/tech* fit. "You're hiring for {{X}} and I spent {{Y}} doing the same failure mode."

> ⚠️ Pitfall: Ending on "so yeah." End on **why here**, then stop. Silence is their turn.

### 3.2 STAR (and what interviewers actually score)

**STAR** ([TIH](https://www.techinterviewhandbook.org/behavioral-interview/)):

| Letter | You say | Time |
|--------|---------|------|
| **S** Situation | Context in one breath (team size, constraint, year) | 15–20 s |
| **T** Task | What *you* were on the hook for (not the epic title) | 10–15 s |
| **A** Action | Decisions, alternatives you rejected, who you pulled in | **50–60% of the answer** |
| **R** Result | Number + what you would do differently (reflection) | 15–20 s |

**They score.** Ownership (I vs we), **scope** (one function vs a surface vs org), **ambiguity** (did you wait to be told?), **conflict without villains**, **learning**. Senior: you changed how the *team* works, not only a PR.

**Follow-up drill.** After every story, answer: What did *you* write? What did you not know at the start? Who disagreed? What is still on fire?

**Anti-patterns.** Hypotheticals ("I would…") when they asked "tell me about a time." Stolen team credit. Blame. Stories from 8 years ago with no recent one.

### 3.3 Story Bank: Eight Slots

Prepare **eight**, 90–150 seconds each, from **real** work. Reuse across companies; retarget the last sentence. Draft one per week ([00](./00-README.md#recommended-study-order)).

| # | Slot | Prompts that pull it | Must include |
|---|------|----------------------|--------------|
| 1 | **Impact** | Favorite project, proudest work | Metric + your slice of the architecture ([Part 2](./15-other-interview-questions-part2.md#35-project-deep-dive)) |
| 2 | **Ownership** | "Not my job," went beyond, drove a decision | You created the task, not only executed |
| 3 | **Conflict** | Disagreement with peer / PM / manager | Disagreed, data, **committed** or escalated cleanly |
| 4 | **Failure** | Mistake, missed deadline, incident you caused | What *you* missed; the fix that **stayed** fixed |
| 5 | **Ambiguity** | Vague spec, missing owner | How you created a spec / spike / RFC |
| 6 | **Tight deadline** | Ship date, incident window | What you cut and why; quality bar you would not cut |
| 7 | **Mentoring** | Junior, peer review, design review | Their outcome, not "I was patient" |
| 8 | **Influence without authority** | Other team, no reports | What you needed from them; how you earned it |

**Card template (keep in a private note, not this repo if it is identifying):**

```text
Slot: {{conflict}}
Headline: {{one line}}
S: {{context}}
T: {{my job}}
A: {{3 bullets, decisions}}
R: {{metric}} | learned: {{one line}}
LPs / values: {{Ownership, Backbone}}
Stack hooks: {{so they can pivot to a deep-dive}}
```

**Labeled EXAMPLE (replace entirely — not your bio):**

> **Conflict.** S: PM wanted to stream 2 GB uploads through Next.js. T: I owned the upload API. A: I wrote a one-pager: ALB idle timeout, instance RAM, pointed at pre-signed S3 ([11](./11-deployment-aws-s3.md) / [09](./09-system-design-part4.md#315-design-file-upload--storage)). Offered a spike of two days. They disagreed; we time-boxed the spike; timeout reproduced. R: Browser PUT shipped; zero 504s on that path; PM used the spike template later. Learned: show the failure, don't win the argument.

If you have **no** conflict story, you have not been paying attention — pick a smaller one (review comment, on-call page ownership). Inventing one is worse than a small true one.

### 3.4 Amazon Leadership Principles as Prompts

Amazon publishes **16** principles on [amazon.jobs](https://www.amazon.jobs/content/en/our-workplace/leadership-principles) (also [aboutamazon.com](https://www.aboutamazon.com/about-us/leadership-principles)). Recruiters treat them as **equal**; a loop may emphasize a subset from the JD. Use them to **tag** your eight stories — useful at Amazon **and** as a coverage checklist anywhere.

| Principle | Story you need |
|-----------|----------------|
| Customer Obsession | You changed work because of a user/metric, not a framework fad |
| Ownership | You crossed a team boundary; "not my job" never appeared |
| Invent and Simplify | You deleted complexity, or borrowed instead of NIH |
| Are Right, A Lot | You sought disconfirming data |
| Learn and Be Curious | You picked up a system that was not assigned |
| Hire and Develop the Best | Mentoring, bar-raising in reviews |
| Insist on the Highest Standards | You stopped a bad ship |
| Think Big | Multi-quarter bet, not a ticket |
| Bias for Action | Reversible decision, shipped a slice |
| Frugality | Cost/egress/NAT ([10](./10-deployment-aws-ec2.md), [11](./11-deployment-aws-s3.md)) |
| Earn Trust | You were wrong publicly and repaired it |
| Dive Deep | You did not stop at "the API is slow" |
| Have Backbone; Disagree and Commit | Slot 3 |
| Deliver Results | Slot 1 with a date |
| Strive to be Earth's Best Employer | How you treated people on the team |
| Success and Scale Bring Broad Responsibility | Second-order effect (privacy, on-call load, climate-of-work) |

Do **not** name-drop LPs in a non-Amazon loop ("per Customer Obsession…"). Do **do** the behaviors.

> 💡 Interview Tip: Bar-raiser style follow-ups: "What was *your* code?", "What would you do differently?", "Who disagreed?" If you cannot answer, the story is too borrowed.

---

## Next: Part 2

➡️ [Part 2 — Deep-Dive, Incidents, Product, Questions](./15-other-interview-questions-part2.md): 10-minute architecture walk, blameless postmortem, "improve this app," and questions you ask by interview stage.
