# Week 7, Day 1: Queues, jobs, and SKIP LOCKED

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning queues, jobs, Laravel events, and DDD domain events by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Learn queues and jobs.** The queue defers slow or unreliable work off the request. The web request commits fast; a worker picks the job up asynchronously.
   - Laravel queues: https://laravel.com/docs/queues

2. **Move notifications into a queued job.** Anything currently sent inline (an email confirmation, a downstream notification) becomes `dispatch(new SendPaymentConfirmation(...))`. The controller stays thin, the request returns fast, and the notification runs on a worker. Any job that mutates bill state still writes to the append-only audit log inside the same transaction as the mutation — the async path does not get to skip the record. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

3. **Learn why `SKIP LOCKED` is the right tool for a job queue.** Laravel's database queue driver on Postgres uses `SELECT ... FOR UPDATE SKIP LOCKED` when a worker pulls the next job. Without `SKIP LOCKED`, two workers competing for the same head-of-queue row would either block each other or accidentally take the same job. `SKIP LOCKED` lets each worker say "give me the next row that no other worker has already locked" — that is exactly what a job queue needs.
   - PostgreSQL SELECT and the locking clause: https://www.postgresql.org/docs/current/sql-select.html

4. **Run a worker locally.** `php artisan queue:work`. Watch the job move from `pending` to running to done. Kill the worker mid-job — the row stays locked until the transaction ends, then another worker picks it up.

## Cross-cutting reminders

- **Audit log**: the queue worker's `SKIP LOCKED` pull is how state changes get made asynchronously, and every such change still writes to the append-only audit log inside the same transaction as the mutation. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Observability**: async paths are where things silently fail. Add a structured log line at the start and end of each job — job name, correlation ID, duration. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None.
