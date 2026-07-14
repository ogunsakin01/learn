# Week 3, Day 4: Pessimistic locking with SELECT FOR UPDATE

## Start-of-day prompt

None. Build day.

## Today's work

1. **Wrap the contribution use case in a transaction.** In Laravel, `DB::transaction(...)`. Every write for this use case commits together or not at all.

2. **Acquire the row lock at the top of the transaction.** In Eloquent: `Bill::where('id', $id)->lockForUpdate()->firstOrFail()`. In the query builder: `->lock('FOR UPDATE')`. Read Postgres explicit locking: https://www.postgresql.org/docs/current/explicit-locking.html. Focus on what `FOR UPDATE` actually locks — the row, blocking any other `FOR UPDATE`, `FOR NO KEY UPDATE`, `UPDATE`, or `DELETE` on that row, until the transaction ends.

3. **Understand what you did.** Under Postgres MVCC, plain reads still do not block. But once you take the row lock, other writers who try to lock the same row wait until you commit. The invariant is now checked and enforced under a consistent view — no snapshot mismatch, no lost update. The lock lives on the aggregate root's row because that is where the invariant lives. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

4. **Write the audit entry inside the same transaction.** The state change and the audit row commit together. If either fails, both roll back. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

5. **Run the failing race test from Day 2.** It should now pass. If it does not, you probably held the lock in the wrong scope, or the transaction is not what you think it is. Do not skip to Day 5 until the race test passes.

6. **Say the tying sentence out loud** as you commit: the same MVCC that lets readers not block writers is exactly why the naive check-then-update loses the update under READ COMMITTED, because each transaction reads its own snapshot and neither sees the other's write until too late. This is a great interview answer.

7. **Commit.** `week 3: pessimistic locking on Bill via SELECT FOR UPDATE`.

## Cross-cutting reminders

- **Tactical DDD**: the row lock lives on the aggregate root because the invariant lives there. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: state change and audit row commit in the same transaction under the lock. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Deadlocks and retry tomorrow.
