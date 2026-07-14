# Week 5, Day 4: Keyset pagination, window functions, and CTEs

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Learn why offset pagination is wrong at scale.** `LIMIT 20 OFFSET 10000` still has to walk 10000 rows the database will throw away, and the result is unstable when rows shift under the cursor. Read Winand's write-up: https://use-the-index-luke.com/no-offset

2. **Replace offset with a keyset (cursor) on an indexed column.** The cursor is the last seen row's sort key (typically `(created_at, id)` for stable ordering). The next page is `WHERE (created_at, id) < (?, ?) ORDER BY created_at DESC, id DESC LIMIT 21`. Do this inside the repository so the caller passes an opaque cursor, not raw SQL.
   - Laravel cursor pagination: https://laravel.com/docs/pagination

3. **Ensure the index supports the sort.** A keyset paginator without a matching index still scans the whole table. The index must cover the columns in the order they appear in `ORDER BY`.

4. **Look at Postgres window functions and CTEs for any reporting view.** If you have a "top contributors per bill" or a running total, `ROW_NUMBER() OVER (PARTITION BY bill_id ORDER BY ...)` or a `WITH totals AS (...)` CTE is cleaner than fetching everything into PHP and looping. This is exactly where Eloquent hurts and the query builder (or raw SQL) earns its place — you do not want models hydrated for a reporting read, and the SQL shape is what matters. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).
   - PostgreSQL window functions and CTEs are under the SQL docs: https://www.postgresql.org/docs/current/queries.html

## Cross-cutting reminders

- **Eloquent vs query builder**: window functions and CTEs are the query builder's territory — reach past Eloquent when the SQL shape is the point. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).
- **Safe schema changes**: any new index you add for the cursor sort must use `CREATE INDEX CONCURRENTLY` in production. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).

## End-of-day prompt

None.
