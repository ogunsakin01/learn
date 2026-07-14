# Week 2, Day 7: Grill on idempotency and layering

## Start-of-day prompt

None. Today is the mock interview for this week's feature.

## Today's work

1. **Run Prompt 3.** Answer aloud, in full sentences, before you type. If you cannot say it out loud you do not know it.

   ```
   I just built the idempotent payment endpoint I just built (Form Request for
   shape, PaymentData DTO across the boundary, domain service holding the use
   case, Bill aggregate enforcing invariants, idempotency key stored before
   processing and guarded by a unique constraint, audit entry written in the same
   transaction). Interview me like a skeptical senior interviewer who doubts my
   choices. Pick the real design decisions in my code and challenge them one at a
   time: why this over the alternative, what breaks under load or concurrency,
   what the tradeoff is. Push on my SOLID and DDD decisions (aggregate
   boundaries, where I put domain logic, why a value object here, why a
   repository there) and on my PostgreSQL choices (isolation level, lock type,
   index type, and how MySQL would differ). Ask one question, wait for my
   answer, then push harder or correct me before the next. Do not accept vague
   answers, force me to be specific. Do not write or fix any code. At the end,
   tell me which of my answers were weak and exactly what to study.
   ```

2. **Write down which answers were weak.** These become next week's morning reading.

3. **Run Prompt 4** to build the reading path for idempotency, since this is a topic worth going deeper on before you move into the concurrency fortnight.

   ```
   I just finished building idempotency (idempotent HTTP endpoints, the
   unique-constraint approach, request fingerprinting, and the audit entry inside
   the same transaction). Give me a structured reading path from fundamentals to
   advanced, naming the canonical books, official docs, and articles, and include
   the PostgreSQL, SOLID, and DDD angles where relevant. Then give me five
   questions a senior engineer must be able to answer about this topic, and tell
   me where each answer is found without answering them for me. Do not write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: keep it. This is your Week 3 morning reading, and Week 3 is the centerpiece.

## End-of-day prompt

None. Tick the week off in the top README.
