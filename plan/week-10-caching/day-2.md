# Week 10, Day 2: Add Redis, cache a bill with cache-aside

## Start-of-day prompt

None.

## Today's work

1. **Add Redis.** Install locally or via Docker. Point Laravel at it. Confirm with a quick set/get through `Redis::` or `Cache::store('redis')`.

2. **Cache a Bill's read state with cache-aside.** The read path in the repository: check the cache by a stable key (`bill:{id}`), return on hit; on miss, load from Postgres, populate the cache with a TTL, return.

3. **Choose what you cache carefully.** Cache the read model of a Bill, not the aggregate you mutate. The aggregate must be reconstituted from the source of truth every time you are about to write, or you are one step from a lost-update bug.

4. **Pick a TTL you can defend.** Long enough to matter, short enough that a missed invalidation self-heals in a bounded time. Write the number and the reasoning into DESIGN.md.

5. **Reading:**
   - Laravel cache: https://laravel.com/docs/cache
   - Laravel Redis: https://laravel.com/docs/redis
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **The dual-write problem**: the cache is a second store. Writing to Postgres and the cache is a dual write. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

None. Review runs at the end of Day 6.
