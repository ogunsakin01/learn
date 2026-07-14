# Week 10, Day 3: Invalidate the cache correctly on every write

## Start-of-day prompt

None. This is the hard part of the week. Get it right.

## Today's work

1. **Invalidate the cache on every write path.** Every service or repository method that changes a Bill's state — contribution recorded, Bill settled, refund, anything — must invalidate the cache entry for that Bill.

2. **Pick a strategy and be consistent.**
   - Delete on write (simplest, safest default): the next read repopulates.
   - Update on write (write-through style): more code, tighter consistency, more failure modes.
   
   Delete-on-write is almost always the right default here. Know why: an update-on-write path that fails mid-flight leaves the cache with a lie; a delete-on-write that fails mid-flight leaves the cache with a miss, which is recoverable.

3. **Order matters.** Commit the database transaction first, then invalidate. If you invalidate before the commit, a concurrent read between the invalidation and the commit will repopulate the cache with the old value, and you have created a stale entry that survives until TTL. Say this rule out loud.

4. **The dual-write reality.** You cannot atomically commit to Postgres and delete from Redis in the same operation. If the invalidation call fails after the commit succeeds, the cache is stale until TTL. Acceptable? Usually yes, because TTL bounds the damage. Not acceptable? Then you are in transactional-outbox territory again — same shape as the webhook problem in Week 7. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

5. **Reading:**
   - Laravel cache tags and forgetting: https://laravel.com/docs/cache

## Cross-cutting reminders

- **The dual-write problem**: cache invalidation is exactly the shape of the dual-write problem, and the mitigations are the same (commit first, make the second step retry-safe, accept a bounded staleness window). See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

None. Review runs at the end of Day 6.
