# Week 3, Day 2: Write the failing race test

## Start-of-day prompt

None. Continuation of yesterday's concurrency arc.

## Today's work

1. **Write a Pest test that fires two concurrent contributions into one Bill.** Two writers, same Bill, both trying to contribute the last unit under the target at the same time. The test should assert an outcome that only holds when the invariant is respected (e.g. total contributions equals `sum(amount)` and never exceeds target).

2. **Get real concurrency, not simulated.** Options:
   - Fork two processes with `pcntl_fork`.
   - Use `pthreads` or a parallel test runner.
   - Two separate DB connections, transactions started deliberately in overlapping order.
   Pick one, commit to it, and know why the alternative was rejected. Real concurrency, not `sleep()` between two sequential calls.

3. **Run the test and watch it fail.** Balance wrong. Double-counted contribution. Whatever the specific symptom, the invariant broke. Do not fix it. Seeing the race fail is the lesson — the whole week's mental model rests on this moment. The invariant is the aggregate's, and a failing race is proof it is unprotected without a lock. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

4. **Commit the failing test.** `week 3: failing race test on concurrent contributions`. Marked `->skip()` or `->group('race')` is fine so CI does not stop on it. The commit is the proof.

## Cross-cutting reminders

- **Tactical DDD**: the failing race is proof the aggregate invariant is unprotected without a lock. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: not touched by a failing test that never mutates cleanly, but keep the rule in mind — once the lock exists, the audit write joins the same transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Isolation theory tomorrow, fix on Day 4.
