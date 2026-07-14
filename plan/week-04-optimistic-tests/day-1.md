# Week 4, Day 1: Optimistic locking, the version column as guard

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning optimistic locking (the version-column approach as a guard on the
aggregate) by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain
the concept from first principles, the two or three standard approaches with the
tradeoffs between them, and the specific failure each approach prevents or causes.
Where it is relevant, explain how PostgreSQL handles it and how that differs from
MySQL, and how it relates to SOLID principles and to tactical DDD (aggregates,
value objects, repositories, domain services, domain events). Then list the exact
things I should be able to explain out loud once I have built it. Stop there. I
will build it and come back.
```

## Today's work

1. **Read Fowler on the offline lock patterns.**
   - Optimistic: https://martinfowler.com/eaaCatalog/optimisticOfflineLock.html
   - Pessimistic (for the contrast): https://martinfowler.com/eaaCatalog/pessimisticOfflineLock.html
   These two pages are short and worth memorising.

2. **Understand the mechanic.** Optimistic locking does not take a database lock. Instead, every write is conditional on the version the reader saw. The write reads `version = N`, computes, and does `UPDATE ... WHERE id = ? AND version = N SET version = N+1, ...`. If someone else committed first, `version` is now `N+1`, the `WHERE` matches zero rows, and your write is silently rejected. You detect it (`affected rows = 0`) and either retry or fail the request.

3. **The invariant is still the aggregate's.** Optimistic locking is not a different invariant; it is a different mechanism for protecting the same one. The Bill still owns "cannot exceed target". The version column is how the Bill notices that its state moved under it. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

4. **The tradeoff, in one paragraph.**
   - **Pessimistic** (Week 3): locks early, serialises contention, safe under high write conflict, but writers block and can deadlock.
   - **Optimistic** (this week): no lock, faster under low contention, but under high contention retry storms eat the throughput and the win disappears. Wrong choice for a hot row.

5. **You already added the `version` column in Week 1, Day 4.** Confirm it is there. If not, add it now.

## Cross-cutting reminders

- **Tactical DDD**: optimistic locking is another way of protecting the same aggregate invariant the pessimistic path guards. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: state changes under the optimistic-lock path also write audit entries inside the same transaction as the state change. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. You will build tomorrow.
