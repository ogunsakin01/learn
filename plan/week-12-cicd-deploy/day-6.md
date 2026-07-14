# Week 12, Day 6: Fix review of the pipeline and deploy config

## Start-of-day prompt

None.

## Today's work

1. **Trigger a full pipeline run.** Push a small change. Watch every job — Pest, PHPStan, Pint, deploy — go green end to end. If any is red, fix it before running Prompt 2.

2. **Commit any last cleanup** to the workflow file, Dockerfile, or deploy config. Small, focused commits.

## Cross-cutting reminders

- **Security via secrets**: one last sweep — no tokens in workflow files, no `.env` in git, no secrets in commit messages. See [craft-reference.md → security](../craft-reference.md#security).
- **Safe schema changes**: confirm the deploy runs migrations before serving traffic and that they follow the additive pattern. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).

## End-of-day prompt

Run this **after** you commit. Paste into Claude Code:

```
Review the code I just wrote in the latest git diff. Act as a senior
engineer doing a strict review. Hard rules: do not write corrected code, do not show me
the fix, do not edit any files.

Check specifically for:
- SOLID violations (name the principle and where it breaks).
- DDD problems: domain logic leaking into controllers or models, anemic domain objects,
  missing or wrong aggregate boundaries, persistence concerns bleeding into the domain,
  repositories that are just pass-throughs.
- PostgreSQL-specific issues: wrong isolation level for the operation, wrong lock type,
  wrong or missing index type, queries that will not scale, misuse of transactions.
- Laravel craft: fat controllers, validation in the wrong layer, missing DTOs at
  boundaries, N+1 queries, Eloquent used where the query builder fits better.

For each issue: name it, explain why it matters at a senior level, rate it (blocker /
important / minor), and give me the search terms or the exact resource to learn the
correct approach myself. End with the top three things to fix first, in order. I will
research and fix them on my own.
```

Read what it flagged. Fix in the morning, by yourself.
