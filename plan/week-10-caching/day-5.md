# Week 10, Day 5: Redis as queue driver, compared to SKIP LOCKED

## Start-of-day prompt

None.

## Today's work

1. **Switch the queue driver to Redis.** `QUEUE_CONNECTION=redis`. Run the same jobs you built in Week 7 through it, and verify they work end to end.

2. **Compare to the Postgres SKIP LOCKED queue you already built.**
   - Postgres SKIP LOCKED: same durability as your business data, transactional guarantees, one fewer moving part. Slower under high throughput, and the queue lives in your primary database (contention).
   - Redis queue: faster, purpose-built, isolated from the primary database. Weaker durability by default, and one more component to run.
   
   Write the tradeoff into DESIGN.md. Neither is wrong — the right answer is the one you can defend.

3. **Notice what does not change.** Your jobs, listeners, and idempotent handlers work the same on either driver. That is the abstraction paying off.

4. **Reading:**
   - Laravel queues: https://laravel.com/docs/queues
   - PostgreSQL SELECT and SKIP LOCKED: https://www.postgresql.org/docs/current/sql-select.html
   - Full lists in [resources.md → extension](../resources.md#extension) and [resources.md → validation, async, webhooks](../resources.md#validation-async-webhooks).

## Cross-cutting reminders

- **The dual-write problem**: writing to Postgres and enqueueing to Redis in the same request is a dual write. If the Postgres commit succeeds and the enqueue fails, the job is lost. The transactional-outbox pattern is the general answer. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

None. Review runs at the end of Day 6.
