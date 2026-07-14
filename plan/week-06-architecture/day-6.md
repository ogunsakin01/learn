# Week 6, Day 6: Review of the architecture

## Start-of-day prompt

None. Today is finish-and-commit, then Prompt 2.

## Today's work

1. **Finish the tidy pass from Day 5.** Everything wired through the container, no `new StripeClient()` in a service, no Eloquent call in the domain, no fat controller. The domain boundary is the whole point — if any persistence or provider concern has bled across it, that is what this pass exists to catch. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

2. **Commit.** Small, focused. Something like `week 6: gateway interface, Stripe and Paystack providers, tactical DDD layer in place`.

3. **Run Prompt 2 after the commit** (see below).

## Cross-cutting reminders

- **Tactical DDD**: today's fix pass polices the domain boundary — the aggregate, the repository interface, and the services. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

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
