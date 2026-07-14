# Week 2, Day 3: Idempotency, the retry problem, and unique constraints

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning idempotency (idempotent HTTP endpoints, the retry problem, and the
unique-constraint approach versus check-then-insert) by building it myself in a
Laravel project on PostgreSQL. Do not write any code, do not design my solution,
and do not edit any files. Explain the concept from first principles, the two or
three standard approaches with the tradeoffs between them, and the specific failure
each approach prevents or causes. Where it is relevant, explain how PostgreSQL
handles it and how that differs from MySQL, and how it relates to SOLID principles
and to tactical DDD (aggregates, value objects, repositories, domain services,
domain events). Then list the exact things I should be able to explain out loud
once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Understand the retry problem.** A client sends `POST /payments`. The response is lost — network drop, timeout, browser reload. The client retries with the same intent. Without idempotency, you charge twice. Money is where this matters most. HTTP method semantics matter here: GET, PUT, and DELETE are idempotent by definition; POST is not, which is why the endpoint has to enforce it. See [craft-reference.md → API design](../craft-reference.md#api-design).

2. **Read the canonical sources.**
   - Stripe idempotent requests: https://docs.stripe.com/api/idempotent_requests
   - Stripe blog on the design: https://stripe.com/blog/idempotency
   - Brandur Leach's Postgres write-up (read this twice): https://brandur.org/idempotency-keys

3. **Compare the two approaches on paper.**
   - **Check-then-insert.** `SELECT ... WHERE key = ?` then `INSERT` if missing. Broken under concurrency: two requests can both see "missing" and both insert. This is a lost-update pattern in a different costume.
   - **Insert with a unique constraint.** `INSERT` and let Postgres reject the duplicate on the unique index. The database is the arbiter. Under concurrency, exactly one wins, the other gets a constraint violation you catch and translate to "return the stored result".

4. **Sketch the idempotency key as a value object.** Immutable, compared by value. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

5. **Name the dual-write problem out loud.** You cannot atomically commit a database row and call Stripe in the same breath. Read [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem). You will not solve it this week, but you must be able to state it.

## Cross-cutting reminders

- **API design**: idempotency is a method-semantics decision — POST is not idempotent by default, so the endpoint enforces it. See [craft-reference.md → API design](../craft-reference.md#api-design).
- **Dual-write problem**: state it. Commit local first, make the foreign call retry-safe with the key, reconcile through webhooks in Week 7. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).
- **Audit log**: the endpoint you build tomorrow writes an audit entry inside the same transaction as the state change. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. You will build tomorrow and review on Day 6.
