# Week 13, Day 2: Read the results, find the bottleneck, tune

## Start-of-day prompt

None. Continuation of the load-testing arc from Day 1.

## Today's work

1. **Read yesterday's results carefully.** Not just the summary. Look at:
   - Latency distribution shape. A long tail with a compact body means the average case is fine and something specific is stalling — likely lock contention or a slow query.
   - Error rate by endpoint and status. Deadlocks (Postgres error `40P01`), serialization failures (`40001`), rejected-by-invariant `409`s all mean different things.
   - Throughput as concurrency scales. If it plateaus, that is the ceiling of your slowest resource.

2. **Find the bottleneck.** Systematic, not guessing:
   - Enable Laravel query logging or use `debugbar` on a single request to see what queries the contribution endpoint runs.
   - `EXPLAIN ANALYZE` the slowest one (Week 5's tool, applied for real).
   - Check `pg_stat_activity` during a load run for long-held locks and waiting queries.
   - Check application logs for exceptions and retry counts.

   You can only find a bottleneck you can see — the query log, `pg_stat_activity`, and the app logs are your instrumentation surfaces. See [craft-reference.md → observability](../craft-reference.md#observability).

3. **Tune one thing.** Pick the biggest single win from the evidence:
   - A missing index, added with `CREATE INDEX CONCURRENTLY` (Week 5's safe schema change, applied for real).
   - A query that fetches too much, rewritten as a targeted select.
   - An eager-load pair you missed and are paying N+1 for.
   - A transaction held open across an external call (the dual-write problem showing up as lock time).
   
   Do not change more than one thing at a time. You will not know which change moved the numbers. Dropping an Eloquent read into the query builder is a common win here — object hydration is not free, and hot paths sometimes do not need full models. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).

4. **Rerun the same load test.** Compare the numbers to yesterday's baseline. Write down what changed and by how much. This is a paragraph in DESIGN.md — a real "here is a bottleneck I found and fixed" story.

5. **Commit.** `week 13: tune {the thing} based on load test`.

## Cross-cutting reminders

- **Observability**: bottlenecks are only findable through the instrumentation you already have — query log, `pg_stat_activity`, application logs. See [craft-reference.md → observability](../craft-reference.md#observability).
- **Eloquent vs query builder**: hot-path reads often move from Eloquent to the query builder for the throughput win. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).

## End-of-day prompt

None. Instrumentation tomorrow.
