# Week 2, Day 6: Review the endpoint, then fix

## Start-of-day prompt

None. This is the review-and-fix day.

## Today's work

1. **Confirm you committed.** Prompt 2 works best on a small, focused diff. If you have not committed the endpoint and the DTO refactor, do that now.

2. **Run Prompt 2 (see below).** Read what it flagged. Do not fix inside the AI session.

3. **Research and fix the top three issues yourself.** Use the search terms and resources it gave you. If you catch yourself pasting anything, delete it and write it yourself.

4. **Re-commit the fixes** as a separate commit. `week 2: review fixes`.

## Cross-cutting reminders

- **Audit log**: if the review flagged that the audit write is not inside the same transaction as the state change, that is a blocker — fix it first. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Security**: mass assignment, rate limiting, secrets. See [craft-reference.md → security](../craft-reference.md#security).
- **API design**: status codes and error shape. See [craft-reference.md → api-design](../craft-reference.md#api-design).
- **Dual-write problem**: not solved this week, but the review may probe it. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

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
