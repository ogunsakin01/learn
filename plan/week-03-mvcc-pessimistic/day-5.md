# Week 3, Day 5: Deadlocks and retry handling

## Start-of-day prompt

None. Continuation of the locking arc.

## Today's work

1. **Read about deadlocks.** Two transactions each hold a lock the other needs. Postgres detects deadlocks and aborts one with `40P01`. You cannot prevent every deadlock; you can only make the deadlock-losing transaction retryable. Read: https://www.postgresql.org/docs/current/explicit-locking.html (deadlocks section).

2. **Avoid the obvious deadlock shapes.** Acquire locks in a consistent order (e.g. always lock Bills before contributions, always by ascending ID). If two writers can lock two resources in opposite order, they will deadlock. This is a design choice, not luck.

3. **Add retry handling.** Catch the serialization failure (`40001` for SSI) and the deadlock (`40P01`) at the boundary of the use case. Retry a small, bounded number of times (three is a common ceiling), with a short backoff. Never retry inside the transaction — retry the *whole* use case, from a fresh transaction, because a rolled-back transaction is dead.

4. **Note that the lock protects the aggregate invariant.** The DDD reason the boundary matters: the Bill owns the invariant, so the Bill row is what you lock. Locking anywhere else is the wrong shape — the invariant is not there. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

5. **Commit.** `week 3: deadlock retry handling`.

## Cross-cutting reminders

- **Tactical DDD**: deadlock retry preserves the aggregate invariant by re-running the whole use case against a fresh view. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: retries create multiple attempts, but only the successful transaction commits the audit row. Idempotency (from Week 2) prevents the retried request from being counted twice at the payment layer. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Review tomorrow.
