# Week 8, Day 4: Drill load balancing and caching

## Start-of-day prompt

None. Today is out-loud drilling on system-design patterns.

## Today's work

1. **Drill load balancing out loud.** L4 versus L7, round robin versus least connections versus consistent hashing, sticky sessions and why they hurt scaling, health checks, and what a load balancer does not solve. Talk through it as if to an interviewer. Do not type answers — say them.

2. **Drill caching out loud.** Cache-aside versus write-through versus write-behind, TTL versus event-driven invalidation, cache stampede and how you prevent it (locks, request coalescing, early expiration), and where caching makes a system slower. Money reads are a good specific case to talk through — stale balance is a real product bug.

3. **Run Prompt 3** at the end of the drill. This is a mock interview specifically on load balancing and caching for your app.

4. **Reading, if you need refreshers before drilling:**
   - System Design Interview vol 1 (Alex Xu), the load balancing and caching chapters. Book.
   - The System Design Primer: https://github.com/donnemartin/system-design-primer
   - ByteByteGo: https://bytebytego.com
   - Full list in [resources.md → system design](../resources.md#system-design).

## Cross-cutting reminders

- **Observability**: metrics and traces are how you would see whether a cache is helping or hurting in production. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

Paste this into Claude Code:

```
I just built load balancing and caching (as system-design drilling for a shared-bill payment app on PostgreSQL). Interview me like a skeptical senior interviewer who doubts my choices. Pick the real design decisions in my code and challenge them one at a time: why this over the alternative, what breaks under load or concurrency, what the tradeoff is. Push on my SOLID and DDD decisions (aggregate boundaries, where I put domain logic, why a value object here, why a repository there) and on my PostgreSQL choices (isolation level, lock type, index type, and how MySQL would differ). Ask one question, wait for my answer, then push harder or correct me before the next. Do not accept vague answers, force me to be specific. Do not write or fix any code. At the end, tell me which of my answers were weak and exactly what to study.
```

Answer aloud, in full sentences, before you type. Write down the weak answers.
