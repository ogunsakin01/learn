# Week 12: CI/CD and deployment

**Goal:** every push is checked automatically, and the app runs in production.

## Days

- [ ] [Day 1: CI vs CD and the twelve-factor app](day-1.md) — Prompt 1 at start on CI/CD and deployment.
- [ ] [Day 2: GitHub Actions workflow for Pest, PHPStan, Pint](day-2.md) — no prompt.
- [ ] [Day 3: Postgres and Redis as workflow services](day-3.md) — no prompt.
- [ ] [Day 4: Deploy to a real host with secrets managed properly](day-4.md) — no prompt.
- [ ] [Day 5: Safe migrations in the deploy pipeline, zero-downtime and rollback](day-5.md) — no prompt.
- [ ] [Day 6: Fix review of the pipeline and deploy config](day-6.md) — Prompt 2 at end on the pipeline.
- [ ] [Day 7: Grill on CI/CD, twelve-factor, secrets, zero-downtime deploys](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on CI/CD and deployment. Day 6 end: Prompt 2 on the pipeline. Day 7 end: Prompt 3, then Prompt 4.

## Threads

Operations, safe migrations, security (secrets).

## Reading

GitHub Actions docs, your host's docs, the twelve-factor app. Full list in [resources.md → extension](../resources.md#extension).

## You must be able to answer

- CI versus CD, and where the line falls.
- What twelve-factor says about config, dependencies, and process model.
- How you manage secrets in the pipeline and at runtime, and why never in git.
- How you deploy without downtime and how you roll back.
- Why running tests against real Postgres and Redis in CI matters over mocks.

## Done when

A green pipeline on every push and a live URL deployed automatically.
