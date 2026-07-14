# Week 5, Day 5: Postgres indexing and EXPLAIN ANALYZE

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Learn the Postgres index types.** B-tree is the default and handles equality and range on ordered columns. Partial (`WHERE ...` in the index definition) skips rows that never need to be found. Expression (`ON (lower(email))`) indexes the result of a function. Covering (`INCLUDE (...)`) tacks extra columns onto a B-tree so index-only scans work without touching the heap. GIN is for JSONB, arrays, and full-text search. Read: https://www.postgresql.org/docs/current/indexes.html

2. **Add the indexes your feed and cursor need.** Every new index must have a justification. If you cannot say why a query needs it, do not add it — an index is not free, writes pay for it.

3. **Run `EXPLAIN ANALYZE` on the feed query before and after.** Read the plan. Look for:
   - `Seq Scan` on a large table where an `Index Scan` should be.
   - Actual rows dramatically off from estimated rows (statistics may be stale — `ANALYZE`).
   - The chunks of the plan where time is actually spent (bottom-up).
   - Reference: https://www.postgresql.org/docs/current/using-explain.html

4. **Learn the leftmost-prefix rule.** A composite index on `(a, b, c)` can serve queries filtering on `a`, on `a, b`, or on `a, b, c` — but not on `b` alone. Design composite indexes with the leading column being the one you always filter on.

5. **Note where GIN and JSONB would apply.** If your audit log payload is JSONB and you query into it, a GIN index on the JSONB column (or on a specific expression inside it) is what makes those queries fast.

## Cross-cutting reminders

- **Safe schema changes**: `CREATE INDEX CONCURRENTLY` in production builds the index without a write lock on the table. A plain `CREATE INDEX` on a live table blocks writes for the duration. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).
- **Audit log**: any mutation path you touched this week (repository writes) still writes an audit entry inside the same transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Review of the whole week's work comes tomorrow.
