# Week 5, Day 6: Review of queries, indexes, and the repository

## Start-of-day prompt

None. Today is build-and-commit, then Prompt 2.

## Today's work

1. **Tidy the week's work.** Repository interface and implementation, eager-loaded feed, keyset pagination, indexes added with justifications, `EXPLAIN ANALYZE` output captured in `DESIGN.md` for each query.

2. **Commit.** Small, focused. Something like `week 5: repository, feed, keyset pagination, indexes`. Clean commit, Prompt 2 works best on a small diff.

3. **Run Prompt 2 after the commit** (see below).

## Cross-cutting reminders

- **Safe schema changes**: your index migrations, in production, must be `CREATE INDEX CONCURRENTLY` and reversible. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).
- **Audit log**: any repository write path continues to write an audit entry inside the same transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

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

Read what it flagged. Do not fix anything tonight. Fix in the morning, by yourself.
