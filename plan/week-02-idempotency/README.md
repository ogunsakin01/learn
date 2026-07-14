# Week 2: Validation and the idempotent endpoint

**Goal:** a validated, idempotent payment endpoint with the domain layer started.

## Days

- [ ] [Day 1: Form Requests and where validation lives](day-1.md) — Prompt 1 at start on validation layering.
- [ ] [Day 2: The line between input validation and domain invariants](day-2.md) — no prompt.
- [ ] [Day 3: Idempotency, the retry problem, and unique constraints](day-3.md) — Prompt 1 at start on idempotency.
- [ ] [Day 4: Build the idempotent endpoint](day-4.md) — no prompt.
- [ ] [Day 5: PaymentData DTO and the domain service](day-5.md) — no prompt.
- [ ] [Day 6: Review the endpoint, then fix](day-6.md) — Prompt 2 at end on the endpoint.
- [ ] [Day 7: Grill on idempotency and layering](day-7.md) — Prompt 3, then Prompt 4 to go deeper.

## Prompt rhythm

Day 1 start: Prompt 1 on validation layering. Day 3 start: Prompt 1 on idempotency. Day 6 end: Prompt 2 on the endpoint. Day 7 end: Prompt 3 to grill idempotency, then Prompt 4 to go deeper.

## Threads

SOLID (SRP across controller, request, service). DDD (value objects, domain service). DTOs. Apply the security and API design items from the cross-cutting section (mass assignment, rate limiting, secrets, status codes). Name the dual-write problem out loud even if you do not solve it.

## Reading

Laravel validation and Form Requests. Stripe idempotency docs. Brandur Leach's idempotency article. PHP readonly classes. Full list in [resources.md → idempotency](../resources.md#idempotency) and [resources.md → validation, async, webhooks](../resources.md#validation-async-webhooks).

## You must be able to answer

- What idempotent means.
- Why you store the key before processing, not after.
- Why check-then-insert breaks under concurrency and how a unique constraint fixes it.
- Which validation belongs in the Form Request versus the aggregate.
- Which HTTP methods are idempotent by definition and which status codes go with which outcome.
- What the dual-write problem is and why it forces the idempotency-plus-webhook shape.

## Done when

The same request twice produces one charge, and the logic sits in the right layer.
