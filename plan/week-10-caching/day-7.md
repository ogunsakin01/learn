# Week 10, Day 7: Grill on invalidation, stampede, and when not to cache

## Start-of-day prompt

None. Today is the mock interview and the deeper reading path.

## Today's work

1. **Fix what Prompt 2 flagged.** By yourself. Commit the fixes.

2. **Run Prompt 3.** Answer aloud, in full sentences. Push yourself on invalidation ordering (commit-then-delete, not delete-then-commit), on cache stampede mitigations (single-flight, locking, early expiration), on the durability tradeoff for the idempotency store, and on when caching makes a system slower (low hit rates, cheap queries, high write-to-read ratios, correctness-critical reads like account balances).

3. **Run Prompt 4** on whichever piece came out weakest.

## Cross-cutting reminders

- **The dual-write problem**: if the mock exposed a weak answer on cache invalidation or the Redis idempotency store, that is the dual-write concept coming due. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## End-of-day prompt

Paste this into Claude Code:

```
I just built a Redis cache layer for a shared-bill payment app on PostgreSQL: cache-aside on Bill reads with delete-on-write invalidation, the idempotency store moved from Postgres to Redis, a Redis-backed rate limiter, and the queue moved to Redis alongside the SKIP LOCKED Postgres queue for comparison. Interview me like a skeptical senior interviewer who doubts my choices. Pick the real design decisions in my code and challenge them one at a time: why this over the alternative, what breaks under load or concurrency, what the tradeoff is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic, why a value object here, why a repository there) and on my PostgreSQL choices (isolation level, lock type, index type, and how MySQL would differ). Ask one question, wait for my answer, then push harder or correct me before the next. Do not accept vague answers, force me to be specific. Do not write or fix any code. At the end, tell me which of my answers were weak and exactly what to study.
```

Then, for the deeper reading:

```
I just finished building caching and Redis for a payments app on PostgreSQL. Give me a structured reading path from fundamentals to advanced, naming the canonical books, official docs, and articles, and include the PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior engineer must be able to answer about this topic, and tell me where each answer is found without answering them for me. Do not write code.
```
