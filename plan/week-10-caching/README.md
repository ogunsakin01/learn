# Week 10: Caching and Redis

**Goal:** a cache layer you can reason about, with correct invalidation.

## Days

- [ ] [Day 1: Concept first on caching](day-1.md) — Prompt 1 at start on caching strategy and invalidation.
- [ ] [Day 2: Add Redis, cache a bill with cache-aside](day-2.md) — no prompt.
- [ ] [Day 3: Invalidate the cache correctly on every write](day-3.md) — no prompt.
- [ ] [Day 4: Move the idempotency store and rate limiter to Redis](day-4.md) — no prompt.
- [ ] [Day 5: Redis as queue driver, compared to SKIP LOCKED](day-5.md) — no prompt.
- [ ] [Day 6: Tests proving no stale data, then review](day-6.md) — Prompt 2 at end on the cache layer.
- [ ] [Day 7: Grill on invalidation, stampede, and when not to cache](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on caching strategy and invalidation. Day 6 end: Prompt 2 on the cache layer. Day 7 end: Prompt 3, then Prompt 4.

## Threads

Performance. Reliability.

## Reading

Laravel cache and Redis docs. Articles on cache invalidation and cache stampede. Full list in [resources.md → extension](../resources.md#extension).

## You must be able to answer

- Cache-aside versus write-through.
- How you invalidate correctly.
- What a cache stampede is and how to prevent it.
- When caching makes things worse.

## Done when

Reads are cached and correctly invalidated, with a test that proves no stale read.
