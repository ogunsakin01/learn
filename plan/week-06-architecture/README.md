# Week 6: Architecture, the two-provider gateway, SOLID and DDD in full

**Goal:** defensible architecture serving Stripe and Paystack, with the tactical DDD layer complete.

## Days

- [ ] [Day 1: Service container, DI, and Active Record vs Data Mapper](day-1.md) — Prompt 1 at start on dependency injection and Active Record versus Data Mapper.
- [ ] [Day 2: Define the gateway interface and the fake first](day-2.md) — no prompt.
- [ ] [Day 3: Stripe implementation with the normalized ChargeResult](day-3.md) — no prompt.
- [ ] [Day 4: Paystack implementation, open/closed live](day-4.md) — no prompt.
- [ ] [Day 5: Pull the tactical DDD layer into shape, and know where it is overkill](day-5.md) — no prompt.
- [ ] [Day 6: Review of the architecture](day-6.md) — Prompt 2 at end.
- [ ] [Day 7: Grill on DI, SOLID, aggregate design, and Active Record vs Data Mapper](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on dependency injection and Active Record versus Data Mapper. Day 6 end: Prompt 2 on the architecture. Day 7 end: Prompt 3 to grill SOLID and the DDD boundaries, then Prompt 4.

## Threads

SOLID (all five). DDD (aggregate, domain services, repositories, the persistence tension). DTOs. Strategy pattern.

## Reading

Laravel container, providers, and contracts. Refactoring Guru on strategy. Fowler on dependency injection. Vaughn Vernon's *Implementing Domain-Driven Design*. Matthias Noback's writing on DDD in PHP. `spatie/laravel-data` to compare against your hand-built DTOs. Full list in [resources.md → architecture, SOLID, DDD](../resources.md#architecture-solid-ddd).

## You must be able to answer

- What dependency injection is and why the container earns its keep.
- How you added Paystack without touching a single caller, and which SOLID letter that is.
- A real line in your code for each of the five SOLID principles.
- Why the Bill is the aggregate root, and what invariant it protects.
- The tradeoff between Active Record (Eloquent) and Data Mapper (Doctrine) for DDD, and what a purist would split.
- Where the tactical DDD layer is overkill for an app this size, and at what size and team it starts paying for itself.

## Done when

Adding Paystack touched no caller, the domain layer is clean, and you can both point at every SOLID letter and argue where the DDD machinery earns its place versus where it does not.
