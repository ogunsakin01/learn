# Craft reference: read once, apply throughout

Day files link into specific sections of this file when a topic comes up. Use the anchor links: `craft-reference.md#the-audit-log`, `craft-reference.md#solid`, etc.

## Contents

- [SOLID, mapped to this project](#solid)
- [Tactical DDD, mapped to this project](#tactical-ddd)
- [Validation: where it goes](#validation)
- [DTOs: where they earn their place](#dtos)
- [Eloquent vs Query Builder vs raw SQL](#eloquent-vs-query-builder-vs-raw-sql)
- [Cross-cutting concerns](#cross-cutting-concerns) — security, the audit log, dual-write, safe schema changes, observability, API design, PHP standards

---

## SOLID

Do not recite SOLID. Point at it in your own code:

- **Single responsibility**: the controller only coordinates, the Form Request only validates input shape, the service holds one use case, the value object holds one concept. If a class has two reasons to change, split it.
- **Open/closed**: adding Paystack next to Stripe without touching a single caller. New behaviour by adding a class, not editing existing ones.
- **Liskov substitution**: any PaymentGateway implementation, real or fake, is swappable without the caller knowing or breaking.
- **Interface segregation**: the gateway interface stays minimal. No client is forced to depend on methods it does not use. No fat "do everything" interfaces.
- **Dependency inversion**: your code depends on the gateway interface and the repository interface, never on the concrete Stripe class or Eloquent directly. The container wires the concretes in.

The review and grill prompts already check these. Make yourself able to point at a real line for each letter.

---

## Tactical DDD

Full strategic DDD (multiple bounded contexts, context maps) is overkill for a solo project, and saying so in an interview is itself a sign of maturity. What applies here is tactical DDD, and it maps cleanly:

- **Ubiquitous language**: name everything in domain terms and use those same words in code, tests, and DESIGN.md. A "Bill", a "contribution", a "settlement". Not "record" and "row".
- **Aggregate root**: the Bill (the pooled balance) is your aggregate root and your consistency boundary. It owns the invariant that contributions cannot exceed the target and that a settled bill takes no more money. This is not decoration: it is exactly what the concurrency weeks protect with locking.
- **Value objects**: Money (amount in minor units plus currency), and an idempotency key, immutable and compared by value, not identity.
- **Domain events**: the Bill raises PaymentReceived and BillSettled. Listeners react. This is the events week, given a domain meaning.
- **Repositories**: the domain talks to a BillRepository interface, not to Eloquent. Persistence lives behind the interface. This is dependency inversion and DDD meeting in the same place.
- **Domain services**: logic that does not belong to a single entity lives in a domain service, not smeared across controllers.

The honest tension: Laravel's Eloquent is the Active Record pattern, where the model knows how to persist itself. Classic DDD prefers persistence-ignorant domain objects (the Data Mapper pattern, which Doctrine uses). A senior must be able to discuss this. For this project, stay pragmatic: keep Eloquent, but put domain logic in the aggregate and domain services, hide persistence behind repository interfaces, and keep models from becoming dumping grounds. Know why a purist would split the domain model from the persistence model, and what that costs.

---

## Validation

- **Input shape** (required, types, ranges, formats) belongs in a Form Request, one per endpoint. Not in the controller. Authorization can live there too.
- **Domain rules** that need database state or business logic ("this bill is already settled") belong in the domain, enforced by the aggregate or a domain service, not in the Form Request. The Form Request guards the shape, the aggregate guards the invariant. Knowing this split is a common interview probe.

---

## DTOs

A DTO is a typed object you pass across a boundary instead of an array. Three boundaries here: validated request into the service (a `PaymentData` DTO), service into gateway (a typed charge input), and gateway back into service (a normalized `ChargeResult`, so Stripe and Paystack return the same shape). The normalized result is what makes the two-provider design clean. Build your first DTOs as plain readonly PHP classes so you learn the concept, then look at `spatie/laravel-data` to see it at scale.

---

## Eloquent vs Query Builder vs raw SQL

Eloquent for domain logic and relationships, the query builder for complex aggregations and performance-critical reads where you do not need full models, raw SQL only when neither fits and always parameterized. The senior point is knowing the cost: Eloquent hydrates objects and can hide N+1s, the query builder is leaner. Pick deliberately. With repositories in place, this choice lives inside the repository and the domain never sees it.

---

## Cross-cutting concerns

These do not get their own week because they belong everywhere. A payments app that ignores them is not a senior project. Apply each where noted.

### Security

Apply in weeks 2 and 7. A money endpoint is a target. Never pass raw request input into Eloquent `create` or `update`, guard mass assignment with explicit assignment or DTOs — this is the most common Laravel hole. Keep queries parameterized. Keep Stripe and Paystack keys in the environment, never in git. Verify webhook signatures (Stripe's signature, Paystack's `x-paystack-signature` HMAC SHA512) before trusting any payload — an unverified webhook lets anyone mark a bill paid. Rate-limit the payment endpoint with throttle middleware. Never log card data or secrets, and know why pushing card handling to the provider keeps you out of PCI scope. Be able to walk the OWASP Top 10 at a high level.

### The audit log

Design in week 1, write to it from every week that changes bill state. A payments domain needs an append-only record of every state change on a bill for reconciliation and disputes, and retrofitting one after the aggregate exists guarantees you miss events. Design the table alongside Bill and Contribution in week 1, then treat "write the audit entry inside the same transaction as the state change" as a rule from the first mutation onwards. Weeks 2, 3, 4, and 7 all mutate state, so all of them write to it. It sits at the aggregate boundary, which is exactly where DDD wants it.

### The dual-write problem

Name it in weeks 2 and 7. You cannot atomically commit a database transaction and call an external payment API in the same breath. If one succeeds and the other fails, your state diverges. This is the deep reason idempotency and ordering matter: commit local state first, make the foreign call retry-safe with an idempotency key, and reconcile through webhooks. The pattern that generalizes it is the transactional outbox. You need not build the full outbox, but be able to explain the problem and the shape of the fix. Brandur's article is exactly this.

### Safe schema changes

Apply in week 5. A migration that is fine on an empty table can lock a production one. On Postgres, `CREATE INDEX CONCURRENTLY` builds an index without taking a write lock, and additive migrations (add a nullable column, backfill, then enforce) are how you ship without downtime. Be able to explain why a naive migration is dangerous and how you would do it safely.

### Observability

Apply in weeks 7 and 8. Seniors are expected to talk about running the thing. Add structured logging around payments, know where an error tracker like Sentry fits, and be able to discuss logs versus metrics versus traces.

### API design

Apply in week 2. Correct status codes, which HTTP methods are idempotent by definition, a consistent error response shape, and a versioning strategy. Small things, but a sloppy API reads as junior.

### PHP language and standards

Throughout. The project is framework-heavy, but interviews probe pure PHP. Follow PSR-12 formatting and PSR-4 autoloading, understand Composer, and be ready for language questions outside Laravel: generators, traits, late static binding, readonly and enums, and the type system.
