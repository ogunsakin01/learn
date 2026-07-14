# Week 6, Day 1: Service container, DI, and Active Record vs Data Mapper

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning dependency injection, the Laravel service container, and the Active Record versus Data Mapper tension in DDD by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Learn the service container and dependency injection.** The container is a factory that resolves classes and their dependencies. Constructor injection is the default. Bindings map an abstraction (interface) to a concrete. Singletons versus fresh instances. Contextual bindings when the same interface has different concretes per caller. This is dependency inversion made mechanical — your code depends on interfaces, the container wires the concretes in. See [craft-reference.md → SOLID](../craft-reference.md#solid).
   - Laravel service container: https://laravel.com/docs/container
   - Fowler on DI: https://martinfowler.com/articles/injection.html

2. **Understand the Active Record versus Data Mapper tension.** Eloquent is Active Record: the model knows how to persist itself. Doctrine is Data Mapper: the domain model does not know the database exists, and a separate mapper handles persistence. Classic DDD prefers Data Mapper because it keeps the domain persistence-ignorant. For this project you stay pragmatic — keep Eloquent, but put domain logic in the aggregate and hide persistence behind the repository interface. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

3. **Know the cost of each side.** A purist would split the domain model from the persistence model — two classes, a mapper between them, more code, more indirection, but a truly framework-independent domain. Keeping Eloquent buys you speed and less code at the cost of an aggregate that technically inherits from `Model`. Be able to say this out loud.

4. **Reading:**
   - Vaughn Vernon, *Implementing Domain-Driven Design*. Book.
   - Matthias Noback on DDD in PHP: https://matthiasnoback.nl

## Cross-cutting reminders

- **SOLID**: dependency inversion — the container is how DIP becomes concrete in Laravel. See [craft-reference.md → SOLID](../craft-reference.md#solid).
- **Tactical DDD**: the Active Record vs Data Mapper tension is the pragmatic call you are making by keeping Eloquent and hiding it behind repositories. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

None.
