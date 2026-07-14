# Week 13, Day 1: Load-test concurrent contributions with k6 or ab

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning load testing and observability for a Laravel payments app by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Pick a tool.**
   - **k6** — scriptable in JavaScript, thresholds and stages built in, good output. The default choice today.
     - k6 docs: https://k6.io
   - **ab (ApacheBench)** — one command, no scripting. Fine for a first burst-of-requests smoke test, useless for anything shaped.
   - **wrk** — high-throughput, Lua scripting.

2. **Design the scenario around the concurrency you built.** The two-writer race test in Week 3 was a unit-level proof of the locking. Load testing is where you watch it under real concurrency — dozens or hundreds of virtual users all contributing to the same Bill, hitting `SELECT FOR UPDATE`, queueing behind each other, some getting rejected by the invariant (target reached).

3. **What to measure.**
   - Requests per second (throughput).
   - Latency at p50, p95, p99. The tail matters more than the mean.
   - Error rate broken down by status code. A `409` from the aggregate rejecting an over-target contribution is not the same failure as a `500` from a deadlock the retry logic missed.
   - Database connections used at peak (this becomes the Week 8 pooling conversation made real).

   Load tests are the demand side of observability — they show what your instrumentation must be able to answer under pressure. See [craft-reference.md → observability](../craft-reference.md#observability).

4. **Run against the deployed environment, not localhost.** Loopback numbers lie because there is no network. Point k6 at your Week 12 deploy.

5. **Watch your locking and isolation behave under real concurrency.** This is the payoff of Weeks 3 and 4. If pessimistic locking serializes correctly, throughput plateaus but the balance stays exact. If optimistic locking hits high contention, retries spike and effective throughput falls. Both are correct outcomes with different shapes — know which one you built and why.

6. **Reading:**
   - k6 docs: https://k6.io
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **Observability**: today is the "seeing what happens under load" side. The instrumentation side lands on Day 3 and Day 4. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None. You have not written code yet.
