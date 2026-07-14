# Prompts

Four reusable prompt templates. Each day file in the `week-XX-*/` folders already has the day-specific prompts filled in and ready to paste. This file is the source of truth for the templates themselves: reword a prompt here and the day files can be re-filled from it.

## When to run each

There is a rhythm. Prompt 1 opens new work, Prompts 2, 3, and 4 close it.

- **Prompt 1** (learn the concept): at the START of a day, before you write anything new. Never run it after you have already built the thing — that defeats the point.
- **Prompt 2** (review): at the END of a day on which you wrote code, after you have committed. Then spend the next morning fixing what it flagged, by yourself.
- **Prompt 3** (grill): at the END of the last day of a feature, once it works and you have already acted on the review. This is your mock interview for that feature.
- **Prompt 4** (go deeper): at the END of a topic, when you want mastery beyond passing. Good for a lighter day or a weekend.

Each day file tells you exactly which prompt to run and whether at the start or the end.

Commit to git after every feature, before you run Prompt 2. A small, focused diff is what makes the review sharp, and the habit of clean commits is itself a senior signal.

The prompts are written so Claude Code does not edit your files or hand you solutions, and so SOLID, DDD, and PostgreSQL are checked everywhere.

---

## Prompt 1: Concept first (learn before building)

Placeholder: `[TOPIC]`.

```
I am learning [TOPIC] by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

---

## Prompt 2: Code review (point, do not fix)

Placeholder: `[PATHS, or "in the latest git diff"]`.

```
Review the code I just wrote at [PATHS, or "in the latest git diff"]. Act as a senior
engineer doing a strict review. Hard rules: do not write corrected code, do not show me
the fix, do not edit any files.

Check specifically for:
- SOLID violations (name the principle and where it breaks).
- DDD problems: domain logic leaking into controllers or models, anemic domain objects,
  missing or wrong aggregate boundaries, persistence concerns bleeding into the domain,
  repositories that are just pass-throughs.
- PostgreSQL-specific issues: wrong isolation level for the operation, wrong lock type,
  wrong or missing index type, queries that will not scale, misuse of transactions.
- Laravel craft: fat controllers, validation in the wrong layer, missing DTOs at
  boundaries, N+1 queries, Eloquent used where the query builder fits better.

For each issue: name it, explain why it matters at a senior level, rate it (blocker /
important / minor), and give me the search terms or the exact resource to learn the
correct approach myself. End with the top three things to fix first, in order. I will
research and fix them on my own.
```

---

## Prompt 3: Grill me (interview on decisions and tradeoffs)

Placeholder: `[FEATURE]`.

```
I just built [FEATURE]. Interview me like a skeptical senior interviewer who doubts my
choices. Pick the real design decisions in my code and challenge them one at a time:
why this over the alternative, what breaks under load or concurrency, what the tradeoff
is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic,
why a value object here, why a repository there) and on my PostgreSQL choices (isolation
level, lock type, index type, and how MySQL would differ). Ask one question, wait for my
answer, then push harder or correct me before the next. Do not accept vague answers,
force me to be specific. Do not write or fix any code. At the end, tell me which of my
answers were weak and exactly what to study.
```

---

## Prompt 4: Where to learn more (reading path)

Placeholder: `[TOPIC]`.

```
I just finished building [TOPIC]. Give me a structured reading path from fundamentals to
advanced, naming the canonical books, official docs, and articles, and include the
PostgreSQL, SOLID, and DDD angles where relevant. Then give me five questions a senior
engineer must be able to answer about this topic, and tell me where each answer is found
without answering them for me. Do not write code.
```
