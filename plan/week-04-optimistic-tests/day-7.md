# Week 4, Day 7: Grill pessimistic vs optimistic

## Start-of-day prompt

None. Today is the mock interview for the concurrency fortnight.

## Today's work

1. **Run Prompt 3.** Answer aloud, in full sentences, before you type. This is the tradeoff question interviewers love — hedging or waffling here reads as junior.

   ```
   I just built the pessimistic-versus-optimistic tradeoff I just built
   (pessimistic locking via SELECT FOR UPDATE in Week 3, optimistic locking via a
   version column this week, both against the same Bill aggregate, both proven
   with tests, plus notes on advisory locks as the third tool). Interview me like
   a skeptical senior interviewer who doubts my choices. Pick the real design
   decisions in my code and challenge them one at a time: why this over the
   alternative, what breaks under load or concurrency, what the tradeoff is.
   Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain
   logic, why a value object here, why a repository there) and on my PostgreSQL
   choices (isolation level, lock type, index type, and how MySQL would differ).
   Ask one question, wait for my answer, then push harder or correct me before
   the next. Do not accept vague answers, force me to be specific. Do not write
   or fix any code. At the end, tell me which of my answers were weak and
   exactly what to study.
   ```

2. **Write down which answers were weak.** These become Week 5 morning reading.

3. **Run Prompt 4.** The concurrency fortnight is over; this is the natural moment to deepen the reading path.

   ```
   I just finished building the pessimistic-versus-optimistic locking tradeoff
   on a PostgreSQL aggregate (row locks with SELECT FOR UPDATE, version-column
   optimistic locking, advisory locks as the third tool, and tests that prove
   both strategies). Give me a structured reading path from fundamentals to
   advanced, naming the canonical books, official docs, and articles, and
   include the PostgreSQL, SOLID, and DDD angles where relevant. Then give me
   five questions a senior engineer must be able to answer about this topic,
   and tell me where each answer is found without answering them for me. Do not
   write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: kept, into Week 5.

## End-of-day prompt

None. Tick the week off. The concurrency fortnight is done — this is the spine of the whole project.
