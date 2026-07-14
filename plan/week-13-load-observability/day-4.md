# Week 13, Day 4: Harden the audit log, retention policy, basic metrics

## Start-of-day prompt

None.

## Today's work

1. **Harden the append-only audit log.** You have been writing to it since Week 1 (design) and Week 2 onwards (every state change). Today, verify:
   - **No state change path bypasses it.** Grep the codebase for every mutation of Bill and Contribution. Each must have a corresponding audit write inside the same transaction as the state change. If any path is missing an audit write, that is a bug — write the audit entry.
   - **No update or delete paths exist on the audit table.** No repository method, no Eloquent call, no migration that would enable one. The table itself should reject updates and deletes (database-level `REVOKE`, or a trigger that raises).
   - **The audit entry captures enough to reconstruct the change.** Actor, event type, before/after (or the delta), timestamp with time zone, correlation ID.

2. **Decide a retention policy.** Payments audit logs are usually kept for years — regulatory retention (varies by jurisdiction, commonly 5 to 7 years). Write the policy in DESIGN.md even if you do not implement archival. Options for actual retention:
   - Never delete (small volume, cheap storage).
   - Partition by month and detach old partitions to cold storage (Postgres native partitioning, the Week 8 topic applied for real).
   - Archive to object storage after N years.
   
   Pick and defend.

3. **Add basic metrics you can talk to.**
   - Request counts by endpoint.
   - Latency (p50, p95, p99) by endpoint.
   - Payment outcomes: charged, rejected by invariant, rejected by gateway, failed.
   - Queue depth and job failure rate (Week 7's queue infrastructure surfaced as metrics).
   
   Prometheus format via a `/metrics` endpoint is the interview-shaped answer. StatsD via the host's collector is the pragmatic one. Either is fine; be able to defend it.

4. **Commit.** `week 13: audit log hardening, metrics`.

## Cross-cutting reminders

- **The audit log**: today is the enforcement day. Every mutation writes, no update path exists, retention is decided. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Observability**: metrics land today. You now have logs, error tracking, and metrics — the three legs. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None. Docs polish tomorrow.
