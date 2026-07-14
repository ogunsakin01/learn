# Week 7, Day 6: Feature tests for jobs, events, and webhook dedupe

## Start-of-day prompt

None. Today is finish tests, commit, then Prompt 2.

## Today's work

1. **Feature test the queued jobs.** `Queue::fake()`, dispatch the code path that queues the job, assert the job was pushed with the right payload. Then, separately, drive the job's `handle()` directly and assert its side effects.

2. **Feature test domain events.** `Event::fake([PaymentReceived::class, BillSettled::class])`, run the flow that should raise them, assert they were raised with the right aggregate state. Then, separately, drive the listener directly and assert its side effect.

3. **Feature test webhook dedupe.** POST the same webhook payload twice (same event ID, valid signature). Assert one state change, one audit entry, two 200 responses. This is the test that proves idempotency on the ingress side.

4. **Feature test signature rejection.** POST a payload with a broken signature. Assert 400 (or your chosen rejection code), no state change, no audit entry.

5. **Commit.** Something like `week 7: queued jobs, domain events, idempotent Stripe and Paystack webhooks, tests`.

6. **Run Prompt 2 after the commit** (see below).

## Cross-cutting reminders

- **Audit log**: the dedupe test doubles as an audit-log test — exactly one entry should exist after a duplicate delivery. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

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
