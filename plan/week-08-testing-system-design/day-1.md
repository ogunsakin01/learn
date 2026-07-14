# Week 8, Day 1: Fill test gaps and the test pyramid

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning the test pyramid and unit-testing the domain in isolation by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Fill test gaps.** Go through what exists from weeks 2 through 7 and list what is not covered. Idempotent endpoint, pessimistic and optimistic locking races, the repository, the gateway swap, the queued job path, the domain event listeners, the webhook dedupe. Each should have at least one test that would catch a regression.

2. **Unit-test the domain in isolation.** The Bill aggregate, Money, the idempotency key value object, any domain service. No database, no HTTP, no queues in these tests. Pure PHP.

   Notice that good DDD made this easy: pure domain logic needs no database. That is the payoff. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Learn the test pyramid.** Many fast unit tests at the base, fewer integration tests in the middle, a small number of end-to-end tests at the top. Know why the shape matters (feedback speed, flakiness, cost of failure diagnosis) and what an "ice-cream cone" anti-shape looks like. Read Fowler's Practical Test Pyramid: https://martinfowler.com/articles/practical-test-pyramid.html.

4. **Reading:**
   - Pest docs: https://pestphp.com
   - Laravel testing: https://laravel.com/docs/testing
   - Full list in [resources.md → testing](../resources.md#testing).

## Cross-cutting reminders

- **Testing at the aggregate boundary**: unit-testing the domain is easy because the aggregate is the boundary. That is DDD paying off in the test suite. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

None. Prompt 2 runs at the end of Day 2, once the suite is filled out.
