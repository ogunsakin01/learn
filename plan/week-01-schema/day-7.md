# Week 1, Day 7: Grill on the schema and aggregate boundary

## Start-of-day prompt

None. Today is the mock interview for this week's work.

## Today's work

1. **Run Prompt 3.** Answer aloud, in full sentences, before you type. If you cannot say it out loud you do not know it.

   ```
   I just built the initial schema for a shared-bill payment app on PostgreSQL,
   including the Bill (aggregate root), contributions, settlement state, and an
   append-only audit log. Interview me like a skeptical senior interviewer who
   doubts my choices. Pick the real design decisions in my code and challenge
   them one at a time: why this over the alternative, what breaks under load or
   concurrency, what the tradeoff is. Push on my SOLID and DDD decisions
   (aggregate boundaries, where I put domain logic, why a value object here, why
   a repository there) and on my PostgreSQL choices (isolation level, lock type,
   index type, and how MySQL would differ). Ask one question, wait for my
   answer, then push harder or correct me before the next. Do not accept vague
   answers, force me to be specific. Do not write or fix any code. At the end,
   tell me which of my answers were weak and exactly what to study.
   ```

2. **Write down which answers were weak.** These become next week's morning reading.

3. **Optional (recommended): Prompt 4** on PostgreSQL indexing, so you go into Week 5 already knowing what B-tree, GIN, partial, expression, and covering indexes are for.

   ```
   I just finished building the initial schema for a payments app on PostgreSQL.
   Give me a structured reading path from fundamentals to advanced on PostgreSQL
   indexing, naming the canonical books, official docs, and articles, and
   include the PostgreSQL, SOLID, and DDD angles where relevant. Then give me
   five questions a senior engineer must be able to answer about this topic,
   and tell me where each answer is found without answering them for me. Do not
   write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: keep it. This is your Week 2 morning reading.

## End-of-day prompt

None. Tick the week off in the top README and take a break.
