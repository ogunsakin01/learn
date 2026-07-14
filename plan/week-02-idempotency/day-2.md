# Week 2, Day 2: The line between input validation and domain invariants

## Start-of-day prompt

None. Continuation of yesterday's validation arc.

## Today's work

1. **Draw the line explicitly.** On paper or in `DESIGN.md`, list every check a contribution has to pass and mark each one as either **shape** (Form Request) or **invariant** (aggregate). Examples to work through:
   - "amount is a positive integer in minor units" — shape.
   - "currency is one of the ISO 4217 codes you support" — shape.
   - "this bill is not already settled" — invariant, needs database state.
   - "adding this contribution would not exceed the target" — invariant, owned by the Bill aggregate.
   - "the idempotency key is a UUID" — shape.
   - "the idempotency key has not been used before for a different payload" — invariant, needs state.

2. **Locate each invariant on the aggregate.** The Bill owns "cannot exceed target" and "settled bill takes no more money" — the same invariant you wrote in Week 1, Day 3. Sketch the method signature on the Bill that enforces it (e.g. `Bill::accept(Contribution $c)`). No code yet.

3. **Read [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd)** and [craft-reference.md → validation](../craft-reference.md#validation) side by side. The Form Request and the aggregate are not in competition; they guard different things.

4. **Update DESIGN.md** with the shape/invariant table. This is exactly the kind of decision an interviewer probes.

## Cross-cutting reminders

- **Validation**: the split — Form Request for input shape, aggregate for domain invariants — is drawn today. See [craft-reference.md → validation](../craft-reference.md#validation).
- **API design**: the response you return when an invariant fails (409 Conflict, 422 Unprocessable) is a real decision. Pick it today. See [craft-reference.md → api-design](../craft-reference.md#api-design).

## End-of-day prompt

None. Idempotency starts tomorrow with a fresh Prompt 1.
