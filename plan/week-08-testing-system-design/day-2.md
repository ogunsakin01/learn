# Week 8, Day 2: What you fake and what you do not

## Start-of-day prompt

None. Continuation of Day 1's test work.

## Today's work

1. **Be able to explain what you fake versus what you do not, and why.** Fake the payment gateway (a fake implementation of the interface, not a mock). Do not fake the database — run tests against a real Postgres, because the whole point of weeks 3 and 4 was database behaviour that a fake would hide. Do not fake the queue in integration tests that cover the job path. Write the rule down: fake external boundaries you do not own, keep the parts whose behaviour you are actually asserting real.

2. **Refactor tests that fake too much.** Any test that mocks the repository or the aggregate is testing the mock, not the code. Any test that mocks Postgres is hiding the concurrency bugs the schema and locking exist to prevent.

3. **Commit** before running Prompt 2. Small, focused commits — the review is sharper on a tight diff.

## Cross-cutting reminders

- **DDD makes unit testing easy**: pure domain logic has no infrastructure dependencies. If a domain test needs the database, the boundary is wrong. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

Run this **after** you commit. Paste into Claude Code:

```
Review the code I just wrote in the latest git diff. Act as a senior engineer doing a strict review. Hard rules: do not write corrected code, do not show me the fix, do not edit any files.

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
