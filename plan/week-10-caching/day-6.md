# Week 10, Day 6: Tests proving no stale data, then review

## Start-of-day prompt

None.

## Today's work

1. **Write the tests that prove no stale data serves.**
   - Read a Bill (populates cache), mutate it, read again — the second read reflects the mutation, not the cached snapshot.
   - Concurrent read and write: force a read to happen during a write and assert the eventual read is not stale beyond the TTL.
   - The idempotency store on Redis rejects a duplicate key within the TTL, exactly like the Postgres version did in Week 2.
   - The rate limiter on Redis produces the same 429 with `Retry-After` behaviour as the Postgres-backed version.

2. **The cache-invalidation test is the important one.** If it does not fail without the invalidation call, it is not testing the right thing.

3. **Commit** before running Prompt 2. Small, focused commit.

## Cross-cutting reminders

- **The dual-write problem**: the tests are what prove your dual-write tradeoffs are within the staleness bounds you claimed. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

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
