# Week 13, Day 7: Recorded walkthrough and a full mock interview

## Start-of-day prompt

None. Today is the final mock across everything, plus the recorded walkthrough.

## Today's work

1. **Record yourself walking through the project as if to an interviewer.** Twenty to thirty minutes. Screen share, camera optional. Cover:
   - What the project is and why (the shared-bill payment app, the concurrency reason).
   - The schema and the aggregate boundary.
   - The idempotent endpoint and where validation lives.
   - The concurrency work — the invariant, MVCC, `FOR UPDATE`, optimistic version column, the tradeoff.
   - The two-provider gateway and where SOLID shows up.
   - Queues, `SKIP LOCKED`, domain events, webhook idempotency.
   - The load-test numbers and the bottleneck you fixed.
   - Observability: logs, metrics, error tracking, the audit log.
   - What you would do next with more time.
   
   Watch it back. Note where you were vague. Those are the areas to prepare for real interviews.

2. **Run Prompt 3 as a full mock across the whole project.** This is not one feature — it is the entire senior interview.

   ```
   I just built a complete shared-bill payments app on Laravel and PostgreSQL: schema with an aggregate root and an append-only audit log, idempotent payment endpoint with DTOs, pessimistic and optimistic locking, a repository layer, a two-provider gateway (Stripe and Paystack) behind one interface, queues with SKIP LOCKED, domain events, idempotent webhooks, a full test suite, tooling (PHPStan, Pint, Rector) in a pre-commit hook, docker compose for the stack, a CI/CD pipeline deploying to a real host, load tests, structured logging with an error tracker, metrics, and a hardened audit log. Interview me like a skeptical senior interviewer who doubts my
   choices. Pick the real design decisions in my code and challenge them one at a time:
   why this over the alternative, what breaks under load or concurrency, what the tradeoff
   is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic,
   why a value object here, why a repository there) and on my PostgreSQL choices (isolation
   level, lock type, index type, and how MySQL would differ). Ask one question, wait for my
   answer, then push harder or correct me before the next. Do not accept vague answers,
   force me to be specific. Do not write or fix any code. At the end, tell me which of my
   answers were weak and exactly what to study.
   ```

3. **Prompt 4 on anything still weak.** Use it for the topics you fumbled in the mock or the walkthrough. Do not skip this — the whole point of the extension weeks was breadth, and gaps here are the ones a loop will find.

   ```
   I just finished building a complete shared-bill payments app on Laravel and PostgreSQL and want to close any remaining gaps. Give me a structured reading path from fundamentals to
   advanced, naming the canonical books, official docs, and articles, and include the
   PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior
   engineer must be able to answer about this topic, and tell me where each answer is found
   without answering them for me. Do not write code.
   ```

4. **Start applying to real roles.** The last stretch of readiness does not come from another project — it comes from interviewing. Treat the first few loops as practice. What they expose is where to go deeper next.

## Cross-cutting reminders

- **Weak answers list**: this final list is your reading queue for the next few weeks while you interview.

## End-of-day prompt

None. The project is done. Push the video, push the README, apply.
