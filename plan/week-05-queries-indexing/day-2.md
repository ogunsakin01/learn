# Week 5, Day 2: Build the contribution feed and prove the N+1

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Build the contribution feed.** A list endpoint for contributions on a bill (or across bills, whichever your feed shape is). Go through the repository. Return the shape your API expects.

2. **Deliberately create an N+1.** Load a set of contributions, then in the loop touch a relationship on each one (the paying user, the bill title, whatever). Do not eager-load anything yet. This is intentional.

3. **Prove the N+1 with query logging.** Turn on Laravel's query log (`DB::enableQueryLog()` then `DB::getQueryLog()`, or use the debugbar / Telescope if you already have it). Count the queries. You should see one query for the parent set and N queries for the children. Write the number down. The N+1 is a symptom of Eloquent's lazy hydration — the query builder would not do this because it does not hydrate model relationships in the first place. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).

   - Laravel query logging is under the database docs: https://laravel.com/docs/database

4. **Do not fix it yet.** Seeing the failure is the lesson. Fix comes tomorrow.

## Cross-cutting reminders

- **Eloquent vs query builder**: the N+1 you just produced is the classic Eloquent hydration failure — knowing when to reach for the query builder instead is the whole point. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).

## End-of-day prompt

None.
