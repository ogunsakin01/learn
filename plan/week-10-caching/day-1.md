# Week 10, Day 1: Concept first on caching

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning caching strategy and invalidation, cache-aside versus write-through, TTLs, and cache stampede by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Concept first on caching.** Read for depth today, do not code.

2. **Cache-aside versus write-through versus write-behind.**
   - Cache-aside: application reads the cache first, falls back to the database on a miss, populates the cache. Simple, common, and where every invalidation bug lives.
   - Write-through: writes go through the cache to the database; the cache is always consistent with the database on the write path.
   - Write-behind: writes go to the cache, flushed to the database asynchronously. Fast, and a durability trap.

3. **TTLs.** A TTL is not invalidation; it is admission that invalidation is hard. Know why: with a TTL you accept staleness for a bounded window. With true invalidation you accept complexity.

4. **The invalidation problem.** "There are only two hard things in computer science: cache invalidation and naming things." The clean version of the problem: you must invalidate the cache in the same logical unit as the write that made it stale, and you must do it in the correct order. Most stale-read bugs are the wrong order.

5. **Cache stampede.** When a hot key expires, N concurrent readers all miss and pile onto the database at once. Know the mitigations: request coalescing (single-flight), locks around the recompute, and probabilistic early expiration.

6. **Reading:**
   - Laravel cache: https://laravel.com/docs/cache
   - Laravel Redis: https://laravel.com/docs/redis
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **The dual-write problem returns**: caching the database is another form of "keep two stores in sync," and it has the same failure modes as the payment-gateway dual write. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

None. Review runs at the end of Day 6.
