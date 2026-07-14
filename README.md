# The Senior PHP Engineer Build Plan

A guide to building one project that forces you to learn the core engineering depth a senior PHP engineer is tested on:

1. PHP and Laravel depth: architecture, SOLID, tactical Domain-Driven Design, DTOs, validation, dependency injection, design patterns.
2. SQL depth on PostgreSQL (the database you will build on) plus Eloquent: schema design, MVCC and isolation, locking, indexing, query performance, and the PostgreSQL-versus-MySQL comparisons interviewers love to probe.
3. Testing depth, the part most candidates are weak on, so it is where you stand out.
4. System design depth, the separate breadth-and-articulation muscle.

The project is a shared-bill payment app: several people pay into one pooled balance until a target amount is covered. Money plus concurrency is the densest training ground there is, because it forces idempotency, locking, isolation, transactional integrity, and a real aggregate boundary all at once. Keep the product boring and small. The hard parts are the only point.

## Why PostgreSQL

You build this on PostgreSQL, not the Laravel default. It keeps coming up in interviews, its concurrency model is the canonical teaching ground for the hardest topics here, and being able to compare it to MySQL out loud is itself a senior signal. Laravel speaks to Postgres through the same schema builder and Eloquent, so the switch costs you almost nothing and teaches you a lot. Throughout the plan you will learn the Postgres way and the MySQL contrast side by side.

## The one rule that makes this work

AI writes nothing for you. Not code, not the schema, not the migrations, not the design, not the fix. You design and write every part yourself.

AI gets exactly two jobs, and neither produces anything you keep:

1. Teach you a concept before you build it.
2. Review and interview you after you build it, pointing at what is wrong and where to learn the fix, never writing the fix.

If you catch yourself pasting code something else wrote, delete it and write it yourself. The understanding lives in the struggle. Let anything do the struggling for you and you are back where you started: a project full of things you cannot explain. Running framework commands that scaffold empty stubs is fine, because that is not a decision. The contents of every file are yours.

## The daily loop

Use Claude Code as a tutor and a hostile interviewer, never as an engineer. The loop for every piece of work:

1. Concept first. Run Prompt 1 to learn the idea and the tradeoffs before you build.
2. Build it yourself. No AI.
3. Review. Run Prompt 2 so it points at what is weak without fixing it.
4. Research and fix yourself, using the search terms it gave you.
5. Grill. Run Prompt 3 so it interviews you on your decisions.
6. Go deeper. Run Prompt 4 for a reading path.

Commit to git after every feature, before you run Prompt 2. A small, focused diff is what makes the review sharp, and the habit of clean commits is itself a senior signal.

The four prompts and when to run each are in **[plan/prompts.md](plan/prompts.md)**. Each day file in the week folders has that day's prompts already filled in and ready to paste — you should not need to open `prompts.md` day-to-day.

## Pace

"8 weeks" counts sessions, not calendar weeks. Every day here means designing and writing the thing yourself with no AI, on top of real reading (DDIA chapter 7, SQL Antipatterns, the Vernon books). At a sustainable part-time pace that is months, not weeks, and that is fine. Treat each day as a session, not a calendar rule. Miss a day, just continue. The number that matters is not how fast you finish, it is whether you can defend every line at the end.

---

## The build plan

Tick each week off when you finish it. Each week's folder has its own README with day-level checkboxes and one file per day.

### Weeks 1–8: the core

- [ ] **Week 1: [Design the schema yourself on PostgreSQL](plan/week-01-schema/README.md)** — a data model you designed and can defend, with the domain language set.
- [ ] **Week 2: [Validation and the idempotent endpoint](plan/week-02-idempotency/README.md)** — a validated, idempotent payment endpoint with the domain layer started.
- [ ] **Week 3: [Concurrency part one — MVCC, isolation, pessimistic locking](plan/week-03-mvcc-pessimistic/README.md)** — the centerpiece. Understand isolation deeply on Postgres and ship pessimistic locking.
- [ ] **Week 4: [Concurrency part two — optimistic locking and the first real tests](plan/week-04-optimistic-tests/README.md)** — ship optimistic locking and prove both strategies.
- [ ] **Week 5: [Queries, indexing, and the repository pattern](plan/week-05-queries-indexing/README.md)** — a fast, correct feed and real Postgres query knowledge.
- [ ] **Week 6: [Architecture, the two-provider gateway, SOLID and DDD in full](plan/week-06-architecture/README.md)** — defensible architecture serving Stripe and Paystack.
- [ ] **Week 7: [Async, queues, domain events, idempotent webhooks](plan/week-07-async-webhooks/README.md)** — async processing and reliable webhooks with domain events.
- [ ] **Week 8: [Testing, system design, and the defense document](plan/week-08-testing-system-design/README.md)** — a complete suite and a document that proves you can articulate it all.

### Weeks 9–13: the extension (menu, not queue)

Everything in weeks 9–13 is breadth, the exact thing the core plan argues against, so do not grind them completionist-style. Pick the two that match the roles you are actually targeting and go deep on those; skim or skip the rest. If a job description leans on infrastructure and deployment, do weeks 11 and 12. If it leans on performance and scale, do weeks 10 and 13. Auth (week 9) is the one most loops assume you already know, so it is the safest default pick.

- [ ] **Week 9: [Authentication and authorization](plan/week-09-auth/README.md)** — a properly secured API, authenticated and authorized.
- [ ] **Week 10: [Caching and Redis](plan/week-10-caching/README.md)** — a cache layer you can reason about, with correct invalidation.
- [ ] **Week 11: [Code quality tooling and Docker](plan/week-11-tooling-docker/README.md)** — a codebase a machine keeps honest, running entirely in containers.
- [ ] **Week 12: [CI/CD and deployment](plan/week-12-cicd-deploy/README.md)** — every push is checked automatically, and the app runs in production.
- [ ] **Week 13: [Load testing, observability, and polish](plan/week-13-load-observability/README.md)** — prove it under load, see inside it, make it presentable.

---

## Reference

- **[Prompts](plan/prompts.md)** — the four reusable prompt templates and when to run each.
- **[Craft reference](plan/craft-reference.md)** — SOLID, tactical DDD, validation, DTOs, Eloquent vs query builder, and the cross-cutting concerns (security, the audit log, dual-write, safe schema changes, observability, API design, PHP standards).
- **[Resources](plan/resources.md)** — the master link list, grouped by topic and mapped to the weeks.
- **[Defense document and through-line](plan/defense-and-through-line.md)** — how `DESIGN.md` becomes your highest-leverage artefact, the tradeoff signal interviewers listen for, what this plan does not cover, and the triage if you fall behind.
