# Week 3, Day 6: Review the locking, then fix

## Start-of-day prompt

None. Review-and-fix day.

## Today's work

1. **Confirm you committed.** The locking, the retry, and the audit write in the same transaction should all be in the diff Prompt 2 will look at.

2. **Run Prompt 2 (see below).** Read what it flagged.

3. **Research and fix the top three issues yourself.** No pasting. This week is the centerpiece — the depth of your fix is exactly the depth an interviewer will probe on Day 7.

4. **Re-commit the fixes.** `week 3: locking review fixes`.

## Cross-cutting reminders

- **Audit log**: if the audit write is outside the locked transaction, that is a blocker — fix first. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

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
