# Week 13, Day 6: Finalize DESIGN.md across the whole project

## Start-of-day prompt

None.

## Today's work

1. **Finalize DESIGN.md across the whole project.** You have been appending to it since Week 1. Today it becomes the single defensible document.

2. **For every feature, the four-part shape:** the problem, the option you chose, the option you rejected, and why. Written in the ubiquitous language from Week 1. This is the interview cheat sheet in your own words.

3. **Cover every week:**
   - Week 1: schema, aggregate boundary, audit log design, JSONB vs typed columns.
   - Week 2: idempotency approach, where validation lives, DTOs.
   - Weeks 3 and 4: MVCC, isolation, pessimistic vs optimistic locking, the invariant the Bill protects.
   - Week 5: repository pattern, N+1 fix, indexing choices, keyset pagination.
   - Week 6: gateway interface, Active Record vs Data Mapper tension, where DDD is overkill for this app.
   - Week 7: queues, `SKIP LOCKED`, domain events, webhook idempotency.
   - Week 8: test pyramid, system-design scaling document.
   - Weeks 9 to 12 (whichever you did): auth, caching, tooling, CI/CD.
   - Week 13: load-test findings, observability, audit hardening.

4. **Add the through-line paragraph.** One page: how the pieces fit together and what senior signal each carries. The interviewer reads this first.

5. **Commit.** `week 13: finalize DESIGN.md`.

## Cross-cutting reminders

- **The audit log**: DESIGN.md documents the retention policy and the "no bypass" enforcement. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Observability**: DESIGN.md documents the logs-metrics-traces split and where the error tracker slots in. See [craft-reference.md → observability](../craft-reference.md#observability).

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

Point it at DESIGN.md and the OpenAPI spec if it will read documents. Read what it flagged. Fix in the morning.
