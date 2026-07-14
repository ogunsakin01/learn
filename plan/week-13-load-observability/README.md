# Week 13: Load testing, observability, and polish

**Goal:** prove it under load, see inside it, and make it presentable.

## Days

- [ ] [Day 1: Load-test concurrent contributions with k6 or ab](day-1.md) — Prompt 1 at start on load testing and observability.
- [ ] [Day 2: Read the results, find the bottleneck, tune](day-2.md) — no prompt.
- [ ] [Day 3: Structured logging and the error tracker](day-3.md) — no prompt.
- [ ] [Day 4: Harden the audit log, retention policy, basic metrics](day-4.md) — no prompt.
- [ ] [Day 5: OpenAPI spec and README polish](day-5.md) — no prompt.
- [ ] [Day 6: Finalize DESIGN.md across the whole project](day-6.md) — Prompt 2 at end on the docs.
- [ ] [Day 7: Recorded walkthrough and a full mock interview](day-7.md) — Prompt 3 as a full mock, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on load testing and observability. Day 6 end: Prompt 2 on the docs. Day 7 end: Prompt 3 as a full mock, then Prompt 4 on anything still weak.

## Threads

Observability, performance, system design made concrete.

## Reading

k6 docs, your error tracker's docs, OpenAPI, Laravel logging. Full list in [resources.md → extension](../resources.md#extension).

## You must be able to answer

- How you load-test and what you look for beyond requests per second.
- How you find a bottleneck once numbers say something is wrong.
- Logs versus metrics versus traces, and when you reach for each.
- How you would debug a production incident given only logs and metrics.
- Why the audit log must be verified as unbypassable, and how you would prove it.

## Done when

You have load-test numbers, instrumentation, an OpenAPI spec, and a recorded walkthrough you would be proud to show.
