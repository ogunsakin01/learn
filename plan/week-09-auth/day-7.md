# Week 9, Day 7: Grill on auth versus authz, tokens, and access-control models

## Start-of-day prompt

None. Today is the mock interview and the deeper reading path.

## Today's work

1. **Fix what Prompt 2 flagged.** By yourself. Commit the fixes.

2. **Run Prompt 3.** Answer aloud, in full sentences, before you type. Push yourself on the difference between authentication and authorization, on token versus session (especially revocation and CSRF), on role-based versus attribute-based access at a high level, and on how you actually test authorization.

3. **Run Prompt 4** on whichever piece came out weakest — most likely the access-control models, since RBAC versus ABAC is where people bluff.

## Cross-cutting reminders

- **Security**: everything this week was security. If the mock exposed a weak answer, it is a security gap. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

Paste this into Claude Code:

```
I just built authentication and authorization for a shared-bill payment app on PostgreSQL: Sanctum tokens, per-user scoping in the repository, a BillPolicy for view/contribute/settle, and per-user rate limiting on the payment endpoint. Interview me like a skeptical senior interviewer who doubts my choices. Pick the real design decisions in my code and challenge them one at a time: why this over the alternative, what breaks under load or concurrency, what the tradeoff is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic, why a value object here, why a repository there) and on my PostgreSQL choices (isolation level, lock type, index type, and how MySQL would differ). Ask one question, wait for my answer, then push harder or correct me before the next. Do not accept vague answers, force me to be specific. Do not write or fix any code. At the end, tell me which of my answers were weak and exactly what to study.
```

Then, for the deeper reading:

```
I just finished building authentication and authorization for a payments app on PostgreSQL. Give me a structured reading path from fundamentals to advanced, naming the canonical books, official docs, and articles, and include the PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior engineer must be able to answer about this topic, and tell me where each answer is found without answering them for me. Do not write code.
```
