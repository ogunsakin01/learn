# Week 4, Day 3: Force the conflict in a test

## Start-of-day prompt

None. Continuation of the optimistic-lock arc.

## Today's work

1. **Write the conflict test.** Two writers, same Bill, both start from `version = N`. The first commits and moves the row to `N+1`. The second attempts to commit with `WHERE version = N`, matches zero rows, and is rejected.

2. **Assert both sides.**
   - The first writer succeeds; the Bill's state reflects its change.
   - The second writer is rejected with the domain exception you raised on Day 2 (or with a specific HTTP status if you tested through the endpoint).
   - The audit log contains exactly one entry for this change, not two.

   What you are asserting is that the aggregate invariant survived a real conflict — the version check on the aggregate root is what makes that true. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Force determinism.** Optimistic conflict tests are easier than the pessimistic race test — you do not need real concurrency, you need controlled interleaving. Load the Bill in one transaction, mutate and commit in a second, then try to commit the first. The version check does the rest.

4. **Prove the pessimistic race test from Week 3 still passes** with the pessimistic path. Both strategies live in the same codebase; both work.

5. **Commit.** `week 4: optimistic lock conflict test`.

## Cross-cutting reminders

- **Tactical DDD**: the conflict test proves the aggregate invariant holds under real interleaving. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: exactly one audit row for one accepted state change. The rejected writer produces none. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Compare-and-write notes tomorrow.
