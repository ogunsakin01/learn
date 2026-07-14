# Week 4, Day 2: Implement the version-column check

## Start-of-day prompt

None. Build day.

## Today's work

1. **Add an optimistic-lock path alongside the pessimistic one.** Do not replace Week 3's `SELECT FOR UPDATE` code — the point is to have both, so you can argue the tradeoff and switch. Two branches, or two use-case classes, or one with a strategy — pick and defend.

2. **Read, compute, conditional-update.** The domain service:
   - Loads the Bill (no lock), captures the current `version`.
   - Calls the aggregate method that checks the invariant.
   - Writes with `UPDATE bills SET ..., version = version + 1 WHERE id = ? AND version = ?`, using the captured version.
   - Checks affected rows. Zero means the row moved; raise a domain exception (`OptimisticLockException`) and let the caller decide to retry or fail.

   The version-column check sits on the aggregate root because the invariant sits there. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Write the audit entry in the same transaction.** Same rule as Week 3. If the update rejects, the transaction rolls back and no audit row is written. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

4. **Wire retry at the boundary of the use case.** Bounded, small (three retries), reload the Bill (fresh version) each retry. Never retry inside a transaction — always the whole use case.

5. **Commit.** `week 4: optimistic locking via version column`.

## Cross-cutting reminders

- **Tactical DDD**: the version-column guard sits on the aggregate root, same place as the invariant. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: same transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. The proof test goes in tomorrow.
