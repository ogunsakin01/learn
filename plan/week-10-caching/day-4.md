# Week 10, Day 4: Move the idempotency store and rate limiter to Redis

## Start-of-day prompt

None.

## Today's work

1. **Move the idempotency store from Postgres to Redis.** From Week 2, you stored the idempotency key with a unique constraint in Postgres. Redis with `SET NX EX` is the natural equivalent: atomic check-and-set on the key, with a TTL that matches the retry window.

2. **Argue the durability tradeoff.** Postgres persists the idempotency record with the same durability guarantees as the money row. Redis persists based on how you configured it (AOF, RDB, or nothing) — and its default is not the same as Postgres. If Redis loses the last few seconds of writes on a crash, an idempotent-request replay could double-charge. Know what your Redis persistence config is and what it costs. Write the choice into DESIGN.md. The moment the money commit lives in Postgres and the idempotency record lives in Redis, you are back in dual-write territory — same problem shape as the gateway call in Week 7. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

3. **Move the rate limiter to Redis.** Laravel's rate limiter already supports Redis as a driver; the point is to understand what changes. Redis atomic increments (`INCR` with `EXPIRE`) make the counter cheap and cluster-friendly, which is why every rate limiter of scale is Redis-backed.

4. **Do not delete the Postgres idempotency table yet.** Keep it as the reference implementation. Talking about "I moved it and here is the tradeoff" is exactly the senior signal DESIGN.md is for.

5. **Reading:**
   - Laravel Redis: https://laravel.com/docs/redis
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **The dual-write problem again**: moving the idempotency store to Redis raises the same dual-write question — now the money commit is in Postgres and the idempotency record is in Redis. Say out loud what a Redis crash between the two writes would let happen, and why the ordering and TTL choices matter. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

None. Review runs at the end of Day 6.
