# Week 8, Day 5: Drill replication, sharding, queues, estimation

## Start-of-day prompt

None. Second day of out-loud system-design drilling.

## Today's work

1. **Drill replication out loud.** Synchronous versus asynchronous, single-leader versus multi-leader versus leaderless, replication lag and read-after-write consistency, failover, and what breaks in each mode. Postgres streaming replication as the concrete example.

2. **Drill sharding versus Postgres partitioning.** Sharding splits data across machines by a shard key; Postgres declarative partitioning splits a single table across multiple physical tables on one machine (or with foreign-data-wrapper trickery, across machines). Know the difference. Know when you reach for each. Read https://www.postgresql.org/docs/current/ddl-partitioning.html.

3. **Drill queues.** SKIP LOCKED on Postgres (what you built in Week 7) versus a purpose-built broker like Redis, Rabbit, or Kafka. When the Postgres queue is fine, when you outgrow it, and what "at-least-once" costs the consumer (idempotent handlers, again).

4. **Drill back-of-the-envelope estimation.** Requests per second, storage per year, bandwidth, cache hit ratios. Talk through numbers for your app: pick a plausible user count, derive contributions per second, size the audit log at that rate, size Postgres and any cache.

5. **Run Prompt 3** at the end, on replication, sharding, queues, and estimation for your app.

6. **Reading, if you need refreshers:**
   - DDIA, chapters on replication and partitioning. Book.
   - System Design Interview vol 1 and 2 (Alex Xu). Books.
   - Full list in [resources.md → system design](../resources.md#system-design).

## Cross-cutting reminders

- **Observability**: replication lag is a metric you need to see; a healthy system tells you when it is not healthy. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

Paste this into Claude Code:

```
I just built replication, sharding versus Postgres partitioning, queues, and back-of-the-envelope estimation (as system-design drilling for a shared-bill payment app on PostgreSQL). Interview me like a skeptical senior interviewer who doubts my choices. Pick the real design decisions in my code and challenge them one at a time: why this over the alternative, what breaks under load or concurrency, what the tradeoff is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic, why a value object here, why a repository there) and on my PostgreSQL choices (isolation level, lock type, index type, and how MySQL would differ). Ask one question, wait for my answer, then push harder or correct me before the next. Do not accept vague answers, force me to be specific. Do not write or fix any code. At the end, tell me which of my answers were weak and exactly what to study.
```

Weak answers become tomorrow's reading and go into DESIGN.md as open items.
