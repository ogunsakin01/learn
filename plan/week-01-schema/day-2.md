# Week 1, Day 2: Money handling and the Money value object

## Start-of-day prompt

None. Today is research and paper design, continuing from Day 1's Prompt 1 session.

## Today's work

1. **Research why floats are wrong for currency.** IEEE 754 rounding, accumulated error, and why `0.1 + 0.2 !== 0.3`. Know it well enough to explain in one sentence to an interviewer.

2. **Decide your money representation.** Two candidates:
   - Integer minor units (store cents / kobo / pesewas). Fast, exact, no surprise rounding, but you must remember the currency has 2 decimals (or 3, for currencies like KWD).
   - Postgres `numeric(precision, scale)`. Exact decimal arithmetic in the database, but slower and slightly awkward crossing the PHP boundary.
   - Read: PostgreSQL numeric types → https://www.postgresql.org/docs/current/datatype-numeric.html
   
   Pick one. Write down why. You will defend it later.

3. **Design a Money value object on paper.** Fields, invariants, operations you need (add, subtract, allocate across N shares, compare, format), and what it must reject (mixing currencies, negative amounts if that is your rule). Immutable. Compared by value, not identity.

   This is your first DDD value object. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd) for the pattern.

4. **Do not write code yet.** Paper only. Fowler's *Patterns of Enterprise Application Architecture* has the canonical Money pattern write-up — worth skimming if you have it.

## Cross-cutting reminders

None new today.

## End-of-day prompt

None. Still paper work.
