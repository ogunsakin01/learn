# Week 12, Day 7: Grill on CI/CD, twelve-factor, secrets, zero-downtime deploys

## Start-of-day prompt

None. Today is the mock interview for this week's work.

## Today's work

1. **Run Prompt 3.** Answer aloud, in full sentences, before you type. If you cannot say it out loud you do not know it.

   ```
   I just built a CI pipeline (GitHub Actions running Pest, PHPStan, Pint against real Postgres and Redis services) and a deploy to a real host with secrets managed at the host, safe migrations in the release step, and a rollback path. Interview me like a skeptical senior interviewer who doubts my
   choices. Pick the real design decisions in my code and challenge them one at a time:
   why this over the alternative, what breaks under load or concurrency, what the tradeoff
   is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic,
   why a value object here, why a repository there) and on my PostgreSQL choices (isolation
   level, lock type, index type, and how MySQL would differ). Ask one question, wait for my
   answer, then push harder or correct me before the next. Do not accept vague answers,
   force me to be specific. Do not write or fix any code. At the end, tell me which of my
   answers were weak and exactly what to study.
   ```

2. **Write down which answers were weak.** These become next week's morning reading.

3. **Optional (recommended): Prompt 4** to go deeper on deployment patterns, zero-downtime strategies, and secrets management at scale.

   ```
   I just finished building CI/CD and deployment for a Laravel payments app. Give me a structured reading path from fundamentals to
   advanced, naming the canonical books, official docs, and articles, and include the
   PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior
   engineer must be able to answer about this topic, and tell me where each answer is found
   without answering them for me. Do not write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: keep it. This is your Week 13 morning reading.

## End-of-day prompt

None. Tick the week off in the top README and take a break.
