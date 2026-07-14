# Week 4, Day 4: Compare strategies, advisory locks as the third tool

## Start-of-day prompt

None. Continuation of the concurrency arc.

## Today's work

1. **Write comparison notes in DESIGN.md.** For each strategy, one paragraph:
   - How it works, in one sentence.
   - The failure mode it prevents.
   - The failure mode it introduces (deadlocks for pessimistic, retry storms for optimistic).
   - The contention level at which it is the right choice.
   - Which one you would pick for a shared-bill app *at scale*, and why.

   The tradeoff is about how to defend the same aggregate invariant under different contention profiles, not about which invariant to protect. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

2. **Read Postgres advisory locks.** https://www.postgresql.org/docs/current/explicit-locking.html (advisory locks section). Advisory locks are application-defined locks Postgres tracks for you — a named mutex living in the database. They do not lock any row.

3. **Understand when advisory locks earn their place.** Coordinating work that does not map to a single row: a nightly reconciliation job that must not overlap with itself, a rate-limiting counter, cross-row invariants where row locks would be too coarse or too fine. Not for the Bill aggregate — the row lock or version column is the right tool there.

4. **Write the third paragraph.** Advisory locks as the third tool: what they do, when you would reach for them, and why they are not what protects the Bill invariant.

5. **Commit** the notes. `week 4: pessimistic vs optimistic vs advisory notes in DESIGN.md`.

## Cross-cutting reminders

- **Tactical DDD**: pessimistic vs optimistic is a question about how to defend the aggregate invariant, not which one to defend. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: unchanged by today's paper work, but if you use advisory locks anywhere it still holds — every state change under any lock writes an audit entry in the same transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Pest and test refactor tomorrow.
