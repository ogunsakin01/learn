# Week 4: Concurrency part two, optimistic locking and the first real tests

**Goal:** ship optimistic locking and prove both strategies.

## Days

- [ ] [Day 1: Optimistic locking, the version column as guard](day-1.md) — Prompt 1 at start on optimistic locking.
- [ ] [Day 2: Implement the version-column check](day-2.md) — no prompt.
- [ ] [Day 3: Force the conflict in a test](day-3.md) — no prompt.
- [ ] [Day 4: Compare strategies, advisory locks as the third tool](day-4.md) — no prompt.
- [ ] [Day 5: Learn Pest, refactor the test suite](day-5.md) — no prompt.
- [ ] [Day 6: Review the tests, then fix](day-6.md) — Prompt 2 at end on your tests.
- [ ] [Day 7: Grill pessimistic vs optimistic](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on optimistic locking. Day 6 end: Prompt 2 on your tests. Day 7 end: Prompt 3 to grill the pessimistic-versus-optimistic tradeoff, then Prompt 4.

## Threads

DDD (protecting the invariant). Postgres (advisory locks). Testing.

## Reading

As Week 3 plus Pest docs and the Postgres docs on advisory locks. Full list in [resources.md → concurrency](../resources.md#concurrency) and [resources.md → testing](../resources.md#testing).

## You must be able to answer

- Pessimistic versus optimistic and when each is right.
- What advisory locks are for and why they are the third tool.
- At what contention level optimistic becomes the wrong choice.
- How the version column enforces the same invariant the row lock did.
- How you write a test that forces the conflict deterministically.

## Done when

Both strategies are built and tested and you can argue the tradeoff.
