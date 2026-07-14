# Week 7, Day 2: Failed jobs and retries

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Configure `failed_jobs`.** The migration ships with Laravel. Run it. A failed job lands there with its payload, exception, and timestamp, so you can inspect and requeue.

2. **Set retry policy per job.** `public int $tries = 3;`, `public int $backoff = 30;` (or an array for exponential). Understand what each buys you and what it costs — retrying a non-idempotent job three times can produce three side effects.

3. **Handle transient versus terminal failures.** A network blip should retry. A validation error inside the job means the job is wrong forever — throw an exception that skips retries, or fail loudly on the first attempt. Distinguish them in your job code.

4. **Test failure explicitly.** Force a job to throw. Confirm it lands in `failed_jobs` after `$tries` attempts. Confirm `php artisan queue:retry <id>` reruns it. Log the failure with structured context — job name, attempt number, exception class, correlation ID — so the `failed_jobs` row is not the only place the failure is legible. See [craft-reference.md → observability](../craft-reference.md#observability).

5. **Think about idempotency of the job itself.** If a job runs twice (which it will, eventually — worker crash after doing the side effect but before marking done), what happens? The safe answer is that every job that mutates state carries the same idempotency thinking as the payment endpoint from Week 2. A failed job that already made an external call before crashing is the dual-write problem, exactly. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).

## Cross-cutting reminders

- **Dual-write problem**: this is exactly the shape of it. A job that both writes to your database and calls an external API can succeed at one and fail at the other on retry. Commit local state first, make the external call retry-safe with an idempotency key. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).
- **Observability**: structured logs on job failure (job name, attempt, exception class, correlation ID) are how you find out what actually broke. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None.
