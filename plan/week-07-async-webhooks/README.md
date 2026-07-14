# Week 7: Async, queues, domain events, idempotent webhooks

**Goal:** async processing and reliable webhooks, with events given domain meaning.

## Days

- [ ] [Day 1: Queues, jobs, and SKIP LOCKED](day-1.md) — Prompt 1 at start on queues, events, and domain events.
- [ ] [Day 2: Failed jobs and retries](day-2.md) — no prompt.
- [ ] [Day 3: Domain events on the Bill aggregate](day-3.md) — no prompt.
- [ ] [Day 4: Stripe webhook, idempotent and signature-verified](day-4.md) — no prompt.
- [ ] [Day 5: Paystack webhook, same idempotency shape](day-5.md) — no prompt.
- [ ] [Day 6: Feature tests for jobs, events, and webhook dedupe](day-6.md) — Prompt 2 at end.
- [ ] [Day 7: Grill on async, SKIP LOCKED, duplicate webhooks, and domain events](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on queues, events, and domain events. Day 6 end: Prompt 2 on jobs and webhooks. Day 7 end: Prompt 3 to grill async and webhook handling, then Prompt 4.

## Threads

DDD (domain events). Postgres (`SKIP LOCKED`). Reliability. Webhook signature verification and secrets. The audit log continues to receive every state change. Observability starts here — structured logging around payment and webhook paths.

## Reading

Laravel queues and events. PostgreSQL docs on `SKIP LOCKED`. Stripe and Paystack webhook docs. Full list in [resources.md → validation, async, webhooks](../resources.md#validation-async-webhooks).

## You must be able to answer

- Why you queue notifications instead of sending them inline in the request.
- What `SKIP LOCKED` does, and why a database-backed job queue needs it on Postgres.
- What happens on a duplicate webhook, and how you make delivery-twice a no-op.
- The difference between a Laravel event and a DDD domain event.
- Why webhook signature verification is non-negotiable and how each provider signs.
- The dual-write problem: why you cannot atomically commit a local transaction and call an external API, and the shape of the fix (idempotency plus reconciliation).

## Done when

A webhook delivered twice does nothing the second time, the aggregate raises real domain events, and you can explain `SKIP LOCKED`.
