# Week 8, Day 7: Full mock interview across the whole project

## Start-of-day prompt

None. Today is the final mock and, if you want it, the deeper reading path.

## Today's work

1. **Run Prompt 3 as a full mock interview across the whole project.** This is the point everything since Week 1 has been building toward. Answer aloud, in full sentences. If you cannot say it out loud you do not know it.

2. **Write down which answers were weak.** These are the topics to close before you start applying — and they are exactly what Prompt 4 opens tonight.

3. **Optional (recommended): Prompt 4** on whichever topic came out weakest. Isolation, DDD tradeoffs, indexing, queues, system design — pick the one that hurt most in the mock and go deeper.

4. **Tick the core plan off in the top README.** Weeks 1 through 8 done. From here on out, weeks 9 through 13 are the menu — do the two that match the jobs you are targeting, skim the rest. See [defense-and-through-line.md](../defense-and-through-line.md).

## Cross-cutting reminders

- **Observability**: if the mock exposed that you cannot talk about logs, metrics, and traces cleanly, do the Prompt 4 reading there. See [craft-reference.md → observability](../craft-reference.md#observability).
- **Testing at the aggregate boundary**: if the mock exposed weak answers on what you fake and why, revisit [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

Paste this into Claude Code as the full mock:

```
I just built the entire shared-bill payment app on PostgreSQL: schema and audit log, validated and idempotent endpoints, pessimistic and optimistic locking on the Bill aggregate, the repository layer, keyset pagination and index tuning, the Stripe and Paystack gateway behind a normalized DTO, queued jobs and domain events, idempotent webhooks, a full test suite, and a scaling document. Interview me like a skeptical senior interviewer who doubts my choices. Pick the real design decisions in my code and challenge them one at a time: why this over the alternative, what breaks under load or concurrency, what the tradeoff is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic, why a value object here, why a repository there) and on my PostgreSQL choices (isolation level, lock type, index type, and how MySQL would differ). Ask one question, wait for my answer, then push harder or correct me before the next. Do not accept vague answers, force me to be specific. Do not write or fix any code. At the end, tell me which of my answers were weak and exactly what to study.
```

Then, if you want the deeper reading:

```
I just finished building the entire shared-bill payment app on PostgreSQL end to end. Give me a structured reading path from fundamentals to advanced, naming the canonical books, official docs, and articles, and include the PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior engineer must be able to answer about this topic, and tell me where each answer is found without answering them for me. Do not write code.
```
