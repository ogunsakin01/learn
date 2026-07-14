# Week 1, Day 6: Fix review findings, then defense paragraphs

## Start-of-day prompt

None. Today is the "fix what Prompt 2 flagged" morning, then defense writing.

## Today's work

1. **Fix the top three issues** Prompt 2 flagged yesterday. By yourself. Use the search terms and resources it gave you; do not paste code from it. If you catch yourself pasting, delete it and write it yourself.

2. **Commit the fixes** in a separate commit from the initial schema. Message like `week 1: schema fixes from review`.

3. **Write a defense paragraph for every table, column, constraint, and type choice.**
   
   One paragraph per table. For each column: why this type, why this constraint (or none), and what would break if you changed it. Explicitly answer:
   - Why `numeric` vs integer minor units (or the reverse).
   - Why `timestamptz` and not `timestamp`.
   - Why this is `NOT NULL` (or why it is nullable and what null means).
   - Why the foreign key, and what `ON DELETE` behaviour you chose and why.
   - Why the audit log has no `updated_at`.
   - Why the Bill has a `version` column even though nothing uses it yet.
   
   Put this in `DESIGN.md` at the repo root. This document grows every week — see [defense-and-through-line.md](../defense-and-through-line.md).

## Cross-cutting reminders

- **DESIGN.md**: started today, appended to every week. It is your interview cheat sheet in your own words.

## End-of-day prompt

None. Tomorrow is the grill.
