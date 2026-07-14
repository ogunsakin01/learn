# Week 3, Day 7: Grill on isolation, MVCC, and locking

## Start-of-day prompt

None. Today is the mock interview for the centerpiece feature.

## Today's work

1. **Run Prompt 3.** Answer aloud, in full sentences, before you type. This is the week most likely to be probed hard in a real loop — treat this grill as an actual interview.

   ```
   I just built the pessimistic locking on Bill I just built (SELECT FOR UPDATE
   inside a transaction, the audit entry written in the same transaction, retry
   handling on serialization failure and deadlock, and a race test that fails
   without the lock and passes with it). Interview me like a skeptical senior
   interviewer who doubts my choices. Pick the real design decisions in my code
   and challenge them one at a time: why this over the alternative, what breaks
   under load or concurrency, what the tradeoff is. Push on my SOLID and DDD
   decisions (aggregate boundaries, where I put domain logic, why a value object
   here, why a repository there) and on my PostgreSQL choices (isolation level,
   lock type, index type, and how MySQL would differ). Ask one question, wait
   for my answer, then push harder or correct me before the next. Do not accept
   vague answers, force me to be specific. Do not write or fix any code. At the
   end, tell me which of my answers were weak and exactly what to study.
   ```

2. **Write down which answers were weak.** These become Week 4 morning reading.

3. **Run Prompt 4.** This is the topic most worth going deeper on. Do it today, before Week 4 opens with optimistic locking.

   ```
   I just finished building pessimistic locking on a PostgreSQL aggregate (MVCC,
   isolation levels, SELECT FOR UPDATE, deadlock retry, and the aggregate as
   the consistency boundary). Give me a structured reading path from
   fundamentals to advanced, naming the canonical books, official docs, and
   articles, and include the PostgreSQL, SOLID, and DDD angles where relevant.
   Then give me five questions a senior engineer must be able to answer about
   this topic, and tell me where each answer is found without answering them for
   me. Do not write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: kept, and it is your Week 4 morning reading.

## End-of-day prompt

None. Tick the week off.
