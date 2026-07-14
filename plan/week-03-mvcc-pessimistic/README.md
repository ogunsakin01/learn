# Week 3: Concurrency part one, MVCC, isolation, pessimistic locking (the centerpiece)

**Goal:** understand isolation deeply on Postgres and ship pessimistic locking. The most important fortnight.

## Days

- [ ] [Day 1: Lost updates, MVCC, and DDIA chapter 7](day-1.md) — Prompt 1 at start on lost updates and MVCC.
- [ ] [Day 2: Write the failing race test](day-2.md) — no prompt.
- [ ] [Day 3: Postgres isolation levels vs MySQL](day-3.md) — no prompt.
- [ ] [Day 4: Pessimistic locking with SELECT FOR UPDATE](day-4.md) — no prompt.
- [ ] [Day 5: Deadlocks and retry handling](day-5.md) — no prompt.
- [ ] [Day 6: Review the locking, then fix](day-6.md) — Prompt 2 at end on your locking.
- [ ] [Day 7: Grill on isolation, MVCC, and locking](day-7.md) — Prompt 3, then Prompt 4 (this is the topic most worth the extra depth).

## Prompt rhythm

Day 1 start: Prompt 1 on lost updates, MVCC, and isolation. Day 6 end: Prompt 2 on your locking, then fix. Day 7 end: Prompt 3 to grill isolation and locking, then Prompt 4 (this is the topic most worth the extra depth).

## Threads

DDD (aggregate as consistency boundary). Postgres (MVCC, isolation, lock modes).

## Reading

DDIA chapter 7. PostgreSQL docs on concurrency control and transaction isolation. MySQL docs on InnoDB locking for the contrast. Fowler's offline lock patterns. Full list in [resources.md → concurrency](../resources.md#concurrency).

## You must be able to answer

- What anomaly each isolation level prevents.
- How Postgres SERIALIZABLE (SSI) differs from REPEATABLE READ (snapshot isolation).
- How Postgres and MySQL defaults and locking differ (Postgres READ COMMITTED by default and MVCC readers not blocking writers, MySQL InnoDB REPEATABLE READ default with next-key locks).
- What `FOR UPDATE` actually locks.
- The one sentence that ties the week together: the same MVCC that lets readers not block writers is exactly why the naive check-then-update loses the update under READ COMMITTED.
- Why the aggregate boundary is the right place to hold the lock.

## Done when

The race test fails without the lock and passes with it, and you can compare the two databases on isolation out loud.
