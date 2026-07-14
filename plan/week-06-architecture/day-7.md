# Week 6, Day 7: Grill on DI, SOLID, aggregate design, and Active Record vs Data Mapper

## Start-of-day prompt

None. Today is the mock interview for this week's work, after you have fixed what Prompt 2 flagged.

## Today's work

1. **Fix the top three issues Prompt 2 flagged.** By yourself. Commit them separately.

2. **Run Prompt 3.** Answer aloud, in full sentences, before you type.

   ```
   I just built a two-provider payment gateway architecture on a shared-bill payments
   app on PostgreSQL: a minimal PaymentGateway interface with a fake, a Stripe, and
   a Paystack implementation; normalized ChargeInput and ChargeResult DTOs; a full
   tactical DDD layer with the Bill aggregate, domain services, repositories, and
   value objects; wired through the Laravel container. Interview me like a skeptical
   senior interviewer who doubts my choices. Pick the real design decisions in my
   code and challenge them one at a time: why this over the alternative, what breaks
   under load or concurrency, what the tradeoff is. Push on my SOLID and DDD
   decisions (aggregate boundaries, where I put domain logic, why a value object
   here, why a repository there) and on my PostgreSQL choices (isolation level, lock
   type, index type, and how MySQL would differ). Ask one question, wait for my
   answer, then push harder or correct me before the next. Do not accept vague
   answers, force me to be specific. Do not write or fix any code. At the end, tell
   me which of my answers were weak and exactly what to study.
   ```

   Push yourself on the Active Record versus Data Mapper question, on which SOLID letter each part of the architecture demonstrates, and on where the tactical DDD layer is overkill for an app this size.

3. **Write down which answers were weak.** These become next week's morning reading.

4. **Then Prompt 4 for depth on architecture patterns.**

   ```
   I just finished building a two-provider payment gateway with the full tactical
   DDD layer in a Laravel project on PostgreSQL. Give me a structured reading path
   from fundamentals to advanced, naming the canonical books, official docs, and
   articles, and include the PostgreSQL, SOLID, and DDD angles where relevant.
   Then give me five questions a senior engineer must be able to answer about this
   topic, and tell me where each answer is found without answering them for me. Do
   not write code.
   ```

## Cross-cutting reminders

- **Weak answers list**: keep it. This is next week's morning reading.

## End-of-day prompt

None. Tick the week off in the top README.
