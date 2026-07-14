# Week 3, Day 1: Lost updates, MVCC, and DDIA chapter 7

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning lost updates, MVCC, and transaction isolation on PostgreSQL by
building it myself in a Laravel project on PostgreSQL. Do not write any code,
do not design my solution, and do not edit any files. Explain the concept from
first principles, the two or three standard approaches with the tradeoffs between
them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and
how it relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should
be able to explain out loud once I have built it. Stop there. I will build it and
come back.
```

## Today's work

1. **Read DDIA chapter 7, first half.** Kleppmann on transactions, weak isolation, lost updates, and write skew. Book, no link. This is the single most valuable reading in the plan — take notes.

2. **Read PostgreSQL MVCC.** https://www.postgresql.org/docs/current/mvcc.html. Focus on why readers do not block writers and writers do not block readers, and what each transaction actually sees (its snapshot).

3. **Write down the specific anomalies** in your own words:
   - **Dirty read**: reading uncommitted data.
   - **Non-repeatable read**: same row, two different values within one transaction.
   - **Phantom read**: same query, different set of rows.
   - **Lost update**: two transactions read, one overwrites the other's write.
   - **Write skew**: two transactions read overlapping data, each writes without seeing the other, invariant violated.

4. **Sketch the shared-bill lost update on paper.** Two contributions arrive at once, both read `paid = 900`, both compute `paid + 100 = 1000` (target hit), both write. Bill now says `paid = 1000`, but two payments of `100` were charged. Money missing. This is the concrete race you will demonstrate tomorrow.

5. **Tie it to DDD.** The Bill is the aggregate root exactly because it owns the invariant that concurrency wants to break. The lock protects the aggregate. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## Cross-cutting reminders

- **Tactical DDD**: the Bill aggregate is the consistency boundary the concurrency work protects. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: every state change under the lock (starting this week) writes an audit entry inside the same transaction as the state change. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. You will build across the week and review on Day 6.
