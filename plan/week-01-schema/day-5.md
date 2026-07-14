# Week 1, Day 5: Write the migrations

## Start-of-day prompt

None.

## Today's work

1. **Write the migrations by hand.** One per table. `php artisan make:migration` scaffolds an empty stub — filling it in is your job, no AI.

2. **Run them.** `php artisan migrate:fresh` should build the full schema cleanly. `migrate:fresh` again should be idempotent.

3. **Verify in psql.** `\d+ bills`, `\d+ contributions`, `\d+ audit_log` (or whatever you named them). Read the actual DDL Postgres generated. Check that:
   - Types are what you intended (`integer` vs `bigint`, `timestamp` vs `timestamptz`).
   - Foreign keys, unique constraints, and NOT NULLs made it in.
   - Indexes on foreign key columns exist where you want them.
   - Defaults are what you expect.
   - The audit log table has no `updated_at` column and no update path. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

4. **Commit.** Small, focused commit. Message like `week 1: initial schema`. Clean commits are themselves a senior signal, and Prompt 2 works best on a small diff.

## Cross-cutting reminders

- **Audit log table**: exists in this migration set. It should have no `updated_at`, no update path.

## End-of-day prompt

Run this **after** you commit. Paste into Claude Code:

```
Review the code I just wrote in the latest git diff. Act as a senior engineer doing
a strict review. Hard rules: do not write corrected code, do not show me the fix,
do not edit any files.

Check specifically for:
- SOLID violations (name the principle and where it breaks).
- DDD problems: domain logic leaking into controllers or models, anemic domain
  objects, missing or wrong aggregate boundaries, persistence concerns bleeding
  into the domain, repositories that are just pass-throughs.
- PostgreSQL-specific issues: wrong isolation level for the operation, wrong lock
  type, wrong or missing index type, queries that will not scale, misuse of
  transactions.
- Laravel craft: fat controllers, validation in the wrong layer, missing DTOs at
  boundaries, N+1 queries, Eloquent used where the query builder fits better.

For each issue: name it, explain why it matters at a senior level, rate it
(blocker / important / minor), and give me the search terms or the exact resource
to learn the correct approach myself. End with the top three things to fix first,
in order. I will research and fix them on my own.
```

Read what it flagged. Do not fix anything tonight. Fix in the morning, by yourself.
