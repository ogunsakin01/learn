# Week 4, Day 6: Review the tests, then fix

## Start-of-day prompt

None. Review-and-fix day.

## Today's work

1. **Confirm you committed.** The optimistic-lock code, the conflict test, the DESIGN.md comparison, and the Pest refactor should all be in the diff Prompt 2 will look at.

2. **Run Prompt 2 (see below).** Read what it flagged. Prompt 2 this week will probe test quality specifically — flaky race tests, tests that pass by accident, tests that do not actually assert the invariant.

3. **Research and fix the top three issues yourself.** No pasting.

4. **Re-commit the fixes.** `week 4: test review fixes`.

## Cross-cutting reminders

- **Audit log**: if a test does not assert audit-log behaviour on both success and rejection, that is a gap worth flagging in DESIGN.md. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

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
