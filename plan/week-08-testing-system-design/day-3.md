# Week 8, Day 3: The "survive 100x traffic" document

## Start-of-day prompt

None. This is a writing and system-design reading day.

## Today's work

1. **Fix what Prompt 2 flagged yesterday.** By yourself. Search terms from the review, not code from it. Commit the fixes.

2. **Write a "survive 100x traffic" document for your own app.** Not for anyone else — for you, to be able to talk to. Cover each of these with the specific choice you would make for this system and the tradeoff you accept:
   - **Postgres read replicas.** What you route to a replica, what stays on the primary, and how replication lag makes read-after-write a real problem.
   - **Connection pooling with PgBouncer.** Because Postgres uses a process per connection, unlike MySQL's thread per connection. Know the transaction, session, and statement pooling modes and which one breaks prepared statements. Pooling and partitioning both change how migrations behave at scale — an additive, backfill-then-enforce migration path is what keeps you shippable under load. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).
   - **Partitioning.** Postgres declarative partitioning on the audit log or the contributions table by time. Read https://www.postgresql.org/docs/current/ddl-partitioning.html.
   - **A faster idempotency store.** When you would move it from Postgres to Redis and what you give up (durability). This foreshadows Week 10.
   - **Scaled queue workers.** How more workers behave against SKIP LOCKED, where the bottleneck moves.
   - **Caching.** Where a cache-aside helps and where it hurts (money reads especially). Also foreshadows Week 10.
   - **Webhook reliability.** Provider retries, your idempotent handler, and reconciliation for the deliveries that never arrive.

   The document must also cover how you would run the thing: structured logging around payments, where an error tracker sits, and the logs-versus-metrics-versus-traces split. See [craft-reference.md → observability](../craft-reference.md#observability).

3. **Reading:**
   - DDIA, the chapters on replication and partitioning. Book.
   - System Design Interview vol 1 and 2 (Alex Xu). Books.
   - The System Design Primer: https://github.com/donnemartin/system-design-primer
   - ByteByteGo: https://bytebytego.com
   - Full list in [resources.md → system design](../resources.md#system-design).

## Cross-cutting reminders

- **Observability becomes a week-8 focus**: structured logging around payments, error tracker placement, and the difference between logs, metrics, and traces. See [craft-reference.md → observability](../craft-reference.md#observability).
- **Safe schema changes**: partitioning and PgBouncer both change what "a migration" costs at scale — the additive path matters more, not less. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).

## End-of-day prompt

None. Days 4 and 5 are the system-design drills.
