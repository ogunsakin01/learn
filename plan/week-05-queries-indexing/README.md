# Week 5: Queries, Eloquent vs query builder, pagination, indexing on PostgreSQL

**Goal:** a fast, correct feed and real Postgres query knowledge, with the repository pattern introduced.

## Days

- [ ] [Day 1: Eloquent vs query builder, and the BillRepository interface](day-1.md) — Prompt 1 at start on Eloquent versus query builder, repositories, and indexing.
- [ ] [Day 2: Build the contribution feed and prove the N+1](day-2.md) — no prompt.
- [ ] [Day 3: Fix the N+1 with eager loading](day-3.md) — no prompt.
- [ ] [Day 4: Keyset pagination, window functions, and CTEs](day-4.md) — no prompt.
- [ ] [Day 5: Postgres indexing and EXPLAIN ANALYZE](day-5.md) — no prompt.
- [ ] [Day 6: Review of queries, indexes, and the repository](day-6.md) — Prompt 2 at end.
- [ ] [Day 7: Grill on pagination, N+1, EXPLAIN, indexes, and the repository](day-7.md) — Prompt 3, then Prompt 4 on Postgres indexing depth.

## Prompt rhythm

Day 1 start: Prompt 1 on Eloquent versus query builder, repositories, and indexing. Day 6 end: Prompt 2 on queries, indexes, and the repository. Day 7 end: Prompt 3 to grill, then Prompt 4 on Postgres indexing depth.

## Threads

SOLID (DIP via repository). DDD (repository). Postgres (index types, EXPLAIN ANALYZE, window functions). Safe schema changes (`CREATE INDEX CONCURRENTLY`, additive migrations) apply from the cross-cutting section this week.

## Reading

Use The Index, Luke. PostgreSQL docs on indexes and on EXPLAIN. Laravel pagination and eager loading. Full list in [resources.md → schema, indexing](../resources.md#schema-indexing).

## You must be able to answer

- Why offset pagination is slow and unstable as the offset grows.
- What N+1 is, how you spot it in query logs, and how eager loading fixes it.
- How to read an `EXPLAIN ANALYZE` plan: sequential vs index scans, actual vs estimated rows, and where time is spent.
- When you would use a partial index, a covering (`INCLUDE`) index, an expression index, or a GIN index — and when the default B-tree is right.
- Why the repository sits between the domain and Eloquent, and what that buys you.
- Why `CREATE INDEX CONCURRENTLY` matters in production, and what an additive migration looks like.

## Done when

The feed uses keyset pagination, the N+1 is fixed and explained, every index is justified by EXPLAIN ANALYZE, and the domain talks to a repository.
