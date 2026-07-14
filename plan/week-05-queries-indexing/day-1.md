# Week 5, Day 1: Eloquent vs query builder, and the BillRepository interface

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning Eloquent versus query builder, the repository pattern, and PostgreSQL indexing by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Learn where Eloquent, the query builder, and raw SQL each fit.** Eloquent hydrates full models and is right for domain logic and relationships. The query builder is leaner and right for complex aggregations and read-heavy paths where you do not need model behaviour. Raw SQL is a last resort, always parameterized. See [craft-reference.md → Eloquent vs Query Builder vs raw SQL](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).
   - Laravel query builder: https://laravel.com/docs/queries
   - Laravel Eloquent relationships: https://laravel.com/docs/eloquent-relationships

2. **Introduce a `BillRepository` interface.** The domain should stop touching Eloquent directly. Define the interface in domain terms (`findById`, `save`, whatever your aggregate needs), and implement it with an `EloquentBillRepository` in the infrastructure layer. The choice of Eloquent versus query builder now lives inside the repository; the domain never sees it.

   This is dependency inversion and DDD meeting in the same place. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd) and [craft-reference.md → SOLID](../craft-reference.md#solid).

3. **Bind the interface to the concrete in a service provider.** So the container wires it up, not your callers.

4. **Warn yourself against pass-through repositories.** A repository that only forwards `find($id)` to `Model::find($id)` is worse than no repository — it adds a layer without buying you the substitutability or the domain vocabulary. The interface should speak the domain, not the ORM.

## Cross-cutting reminders

- **Eloquent vs query builder**: choice lives inside the repository from today onwards; the domain never sees it. See [craft-reference.md → Eloquent vs query builder](../craft-reference.md#eloquent-vs-query-builder-vs-raw-sql).
- **Tactical DDD**: the `BillRepository` interface is a domain-side repository — persistence lives behind it. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **SOLID**: dependency inversion — the domain depends on the interface, not on Eloquent. See [craft-reference.md → SOLID](../craft-reference.md#solid).

## End-of-day prompt

None. Build the feed tomorrow, review comes on Day 6.
