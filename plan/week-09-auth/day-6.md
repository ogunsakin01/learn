# Week 9, Day 6: Auth tests, then review

## Start-of-day prompt

None.

## Today's work

1. **Write the tests that prove the auth layer works.**
   - Unauthenticated requests to protected endpoints get 401.
   - A user acting on another user's Bill gets 403.
   - A contributor cannot settle a Bill they did not create.
   - A user hitting the rate limit gets 429 with `Retry-After`.
   - A revoked token can no longer authenticate.

2. **These are feature tests, not unit tests.** They exercise the middleware, the policy, and the controller together, because that is what would break in production.

3. **Commit** before running Prompt 2. Small, focused commit — the review is sharper on a tight diff.

## Cross-cutting reminders

- **Security**: an untested auth rule is an unowned auth rule. See [craft-reference.md → security](../craft-reference.md#security).

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
