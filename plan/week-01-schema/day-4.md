# Week 1, Day 4: Columns and Postgres types

## Start-of-day prompt

None. Continuation of the schema-design arc from Day 1.

## Today's work

Turn yesterday's sketch into columns and Postgres types. Decisions on every one.

1. **Identity columns.** Prefer `GENERATED ALWAYS AS IDENTITY` over `SERIAL`. Know why: `SERIAL` is a legacy pseudo-type that creates a sequence with subtly different ownership and permission semantics. `IDENTITY` is the SQL standard and gives you cleaner constraint enforcement. Reference: https://www.postgresql.org/docs/current/sql-createtable.html (search "IDENTITY").

2. **Enums for status.** Two options:
   - Native Postgres enum (`CREATE TYPE bill_status AS ENUM (...)`). Enforced at the database level, but adding a value requires a migration.
   - PHP backed enum stored as `text` or `varchar` with a `CHECK` constraint. More flexible, and Laravel-native.
   
   Pick one, defend it.

3. **UUIDs where they fit.** Not everywhere. Public-facing IDs (URLs, API responses) benefit from being non-sequential; internal-only rows do not need them. If you use UUIDs, know that `uuid` is a native Postgres type (not just `varchar(36)`).

4. **Version column for optimistic locking.** Add `version integer NOT NULL DEFAULT 0` (or `lock_version`) to the Bill now. You will use it in Week 4. Adding it now is trivial; adding it later means a migration on live data.

5. **Foreign keys, unique constraints, and NOT NULL rules.** Push integrity into the database. A `contributions.bill_id` without a foreign key is a bug waiting to happen. Unique on the idempotency key column (Week 2 will need it). NOT NULL everything unless nullability carries meaning.

6. **The audit log columns.** Design it append-only: **no updates, no deletes**, immutable rows.
   
   Required columns: event type (enum or text with check), the actor (user ID, "system", or webhook source), the bill ID it belongs to, before/after values where relevant, and a `timestamptz` (never `timestamp`; you want time zones).
   
   **The JSONB decision:** structured event data (the payload of each event type) either lives in a single `payload jsonb` column, or in typed columns per event type. Tradeoffs:
   - JSONB: one table, one shape, flexible. Weaker enforcement, slower to query on specific fields without expression indexes.
   - Typed columns: strict, cheap to query, but you either have many nullable columns per event type or you split into per-event tables.
   
   Pick one. Defend it. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log) and PostgreSQL JSONB docs: https://www.postgresql.org/docs/current/datatype-json.html.

7. **Timestamps.** Use `timestamptz` for every timestamp column. `created_at` on every table, `updated_at` where mutation is allowed (not on the audit log — it is immutable).

## Cross-cutting reminders

- **Audit log**: append-only, `timestamptz`, JSONB-vs-typed decision made today.
- **Foreign keys and CHECK constraints**: push integrity into the database, not the application. The application will forget; the database will not.

## End-of-day prompt

None. Migrations get written tomorrow, review comes then.
