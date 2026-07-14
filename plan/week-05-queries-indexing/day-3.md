# Week 5, Day 3: Fix the N+1 with eager loading

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Fix the N+1 with eager loading.** Use `with(['relation'])` on the query in the repository. Re-run the request and re-check the query log. You should now see a small constant number of queries (typically two: parent set, children set), not `1 + N`. Eager loading is Eloquent's answer to the hydration problem — you stay in Eloquent for the domain shape and pay a batched cost instead of a per-row one. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).
   - Laravel eager loading: https://laravel.com/docs/eloquent-relationships#eager-loading

2. **Understand why it happened.** Eloquent lazy-loads relationships by default. The moment you touch `$contribution->user` inside a loop, it fires a query per row. Eager loading batches those into a single `WHERE IN (...)`. Be able to say this out loud.

3. **Decide what belongs in the repository.** The repository method should return the data with the relationships already loaded — the caller should not have to know to `with()` anything. The alternative (leaking `with()` calls to the caller) is exactly the leaky-abstraction failure the repository exists to prevent.

4. **Consider selective column loading.** `select(['id', 'bill_id', 'amount'])` on the query if the caller does not need the whole row. Reads are cheaper when you fetch less.

## Cross-cutting reminders

- **Eloquent vs query builder**: eager loading is the Eloquent-side tool for the N+1 you produced yesterday. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).

## End-of-day prompt

None.
