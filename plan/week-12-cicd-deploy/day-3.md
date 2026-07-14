# Week 12, Day 3: Postgres and Redis as workflow services

## Start-of-day prompt

None.

## Today's work

1. **Add Postgres and Redis as services in the Pest job.** GitHub Actions supports `services:` blocks that stand up Docker containers alongside the runner.
   - GitHub Actions services: https://docs.github.com/actions

2. **Match production versions.** If production runs Postgres 16, CI runs Postgres 16. Version drift is a class of bug that only shows up on Friday afternoons.

3. **Health checks.** Every service block gets a `--health-cmd` so the runner waits for the database to actually accept connections before starting tests. `pg_isready` for Postgres, `redis-cli ping` for Redis.

4. **Wire the app at the service hostnames.** In the runner, services are reachable on `localhost` at the exposed ports (a different networking model from `docker compose`). Set `DB_HOST=localhost`, `DB_PORT=5432`, `REDIS_HOST=localhost`, `REDIS_PORT=6379` in the job's env.

5. **Why real engines, not mocks.** All the Week 3 and 4 concurrency work — MVCC, `FOR UPDATE`, isolation levels, `SKIP LOCKED` from Week 7 — is Postgres-specific. Running against SQLite in CI would let a broken locking assumption pass green. The whole point of this project is the Postgres depth. Test it against Postgres.

6. **Run the migrations before tests.** `php artisan migrate --force` as the first step of the Pest job, or a Pest `TestCase` that uses `RefreshDatabase`. Pick one.

## Cross-cutting reminders

None new today.

## End-of-day prompt

None. Deploy tomorrow.
