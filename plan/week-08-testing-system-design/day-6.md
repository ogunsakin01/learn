# Week 8, Day 6: Write DESIGN.md across the project

## Start-of-day prompt

None. Today is documentation.

## Today's work

1. **Finalize DESIGN.md across the whole project.** You have been appending to it since Week 1. Today it becomes complete. For every feature: the problem, the option you chose, the option you rejected, and why. Written in the ubiquitous language (Bill, contribution, settlement — not "record" and "row").

2. **Cover every week:**
   - Week 1: schema, types, the audit log, the aggregate root.
   - Week 2: Form Requests versus aggregate invariants, idempotency store, the DTO boundary.
   - Weeks 3 and 4: MVCC, isolation levels, pessimistic and optimistic locking, and the Postgres-versus-MySQL contrast.
   - Week 5: Eloquent versus query builder, the repository, N+1, keyset pagination, index choices with EXPLAIN ANALYZE evidence.
   - Week 6: the gateway interface, SOLID pointed at real lines, and the honest "when tactical DDD is overkill" paragraph.
   - Week 7: queues, SKIP LOCKED, domain events, idempotent webhooks, the dual-write problem.
   - Week 8: the test pyramid, what you fake, the scaling document.

3. **Document the ubiquitous language** at the top. One-paragraph glossary: Bill, contribution, settlement, payment received, idempotency key, audit entry. Same words as the code. This is where tactical DDD stops being theory and becomes the vocabulary your DESIGN.md, code, and tests all share. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

4. **Document the one bounded context.** State that this project has a single bounded context (payments), and that a real system would carve out notifications, reporting, and identity as their own contexts. Saying so is the maturity signal — do not pretend you have multiple contexts when you do not.

5. **See** [defense-and-through-line.md](../defense-and-through-line.md) for why this document is the highest-value artefact.

## Cross-cutting reminders

- **DESIGN.md is the defense document**: this is the artefact interviews reward. Every decision, the rejected alternative, and why. See [defense-and-through-line.md](../defense-and-through-line.md).
- **Tactical DDD**: the ubiquitous language glossary at the top of DESIGN.md is where DDD becomes documentation, not decoration. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

None. Prompt 2 already ran on the code on Day 2. Tomorrow is the full mock across everything.
