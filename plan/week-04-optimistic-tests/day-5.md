# Week 4, Day 5: Learn Pest, refactor the test suite

## Start-of-day prompt

None. Continuation of the week's arc.

## Today's work

1. **Read the Pest docs.** https://pestphp.com. Focus on: `it()` / `test()`, datasets, `beforeEach`, higher-order tests, expectations, the difference between Pest and PHPUnit under the hood.

2. **Refactor the tests you have.** The race test from Week 3, the optimistic conflict test from Day 3, and whatever ad-hoc coverage exists around the endpoint from Week 2. Turn them into clean Pest tests. One behaviour per test, descriptive names in domain language ("a contribution above the remaining target is rejected", not "test bill 3"). Tests read this cleanly because DDD kept the domain testable in isolation — the aggregate can be exercised without dragging in HTTP or persistence. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Introduce factories.** Laravel model factories (`BillFactory`, `ContributionFactory`) so tests read like the domain and not like fixture bookkeeping. https://laravel.com/docs/testing (factories section).

4. **Fresh database per test.** Use `RefreshDatabase` or `DatabaseTransactions`. Know the difference (`RefreshDatabase` migrates and rolls back per test; `DatabaseTransactions` wraps in a transaction and rolls back). Pick and defend. Note that `DatabaseTransactions` does not work for the pessimistic race test — a test inside a transaction cannot exercise concurrent transactions.

5. **Commit.** `week 4: Pest refactor with factories and clean fixtures`.

## Cross-cutting reminders

- **Tactical DDD**: the aggregate is testable in isolation because domain logic never leaked into controllers or persistence. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: tests assert the audit row is written for accepted changes and not written for rejected ones. Coverage of the log is coverage of the invariant. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Review tomorrow.
