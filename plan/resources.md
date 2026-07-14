# Resources

Links verified against source docs, grouped by topic and mapped to the weeks. Books are named without links because they have no single canonical URL. One line each on what it is best for.

A caution on links: official docs (Laravel, PostgreSQL, MySQL, Stripe, Paystack) are the versions to trust and they stay current. Everything else is a named author or book you can find even if a URL ever moves.

Day files link into the specific subsection they need. This file is the master index.

## Contents

- [Concurrency, transactions, isolation](#concurrency) — weeks 3 and 4
- [Idempotency](#idempotency) — week 2
- [Schema, indexing, query performance](#schema-indexing) — weeks 1 and 5
- [Architecture, SOLID, DDD](#architecture-solid-ddd) — weeks 2, 5, 6
- [Validation, async, webhooks](#validation-async-webhooks) — weeks 2 and 7
- [Security and operations](#security-operations) — cross-cutting
- [Auth, caching, tooling, deployment, operations](#extension) — extension weeks 9 to 13
- [Testing](#testing) — weeks 4, 6, 8
- [System design](#system-design) — week 8

---

## Concurrency

Weeks 3 and 4.

- Designing Data-Intensive Applications, Martin Kleppmann, chapter 7. Book. The single best explanation of isolation, lost updates, and write skew. Read this above all else.
- PostgreSQL concurrency control: https://www.postgresql.org/docs/current/mvcc.html — how MVCC works and why readers do not block writers.
- PostgreSQL transaction isolation: https://www.postgresql.org/docs/current/transaction-iso.html — Read Committed, Repeatable Read as snapshot isolation, and Serializable as SSI.
- PostgreSQL explicit locking: https://www.postgresql.org/docs/current/explicit-locking.html — row locks (`FOR UPDATE`) and advisory locks.
- MySQL InnoDB isolation, for the contrast: https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html
- MySQL InnoDB locking, for the contrast: https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html
- Fowler, Optimistic Offline Lock: https://martinfowler.com/eaaCatalog/optimisticOfflineLock.html
- Fowler, Pessimistic Offline Lock: https://martinfowler.com/eaaCatalog/pessimisticOfflineLock.html

---

## Idempotency

Week 2.

- Stripe idempotent requests reference: https://docs.stripe.com/api/idempotent_requests — the clear, canonical behaviour.
- Stripe blog, designing robust APIs with idempotency: https://stripe.com/blog/idempotency — the why, in depth.
- Brandur Leach, idempotency keys in Postgres: https://brandur.org/idempotency-keys — the deepest practical write-up, with the failure modes.

---

## Schema, indexing

Weeks 1 and 5.

- SQL Antipatterns, Bill Karwin. Book. The best practical guide to schema mistakes and how to avoid them.
- Use The Index, Luke, Markus Winand: https://use-the-index-luke.com — indexing and query performance, from the ground up.
- No Offset (keyset pagination), Markus Winand: https://use-the-index-luke.com/no-offset — why offset pagination is wrong and what to use.
- PostgreSQL indexes: https://www.postgresql.org/docs/current/indexes.html — B-tree, partial, expression, and covering indexes.
- PostgreSQL EXPLAIN: https://www.postgresql.org/docs/current/using-explain.html — how to read a query plan.
- PostgreSQL data types: https://www.postgresql.org/docs/current/datatype.html — for your money, identity, and enum choices.
- Laravel Eloquent relationships and eager loading: https://laravel.com/docs/eloquent-relationships — the N+1 fix.
- Laravel query builder: https://laravel.com/docs/queries — when you drop below Eloquent.
- Laravel pagination: https://laravel.com/docs/pagination — including cursor pagination.

---

## Architecture, SOLID, DDD

Weeks 2, 5, 6.

- Domain-Driven Design Distilled, Vaughn Vernon. Book. The short, readable starting point. Read this first for DDD.
- Implementing Domain-Driven Design, Vaughn Vernon. Book. The deeper tactical reference.
- Learning Domain-Driven Design, Vlad Khononov. Book. A modern, approachable take.
- Matthias Noback's blog, DDD and architecture in PHP: https://matthiasnoback.nl — the best PHP-specific source.
- Fowler, Dependency Injection: https://martinfowler.com/articles/injection.html — the canonical explanation of DI and IoC containers.
- Refactoring Guru, Strategy pattern: https://refactoring.guru/design-patterns/strategy — plain-language patterns.
- Laravel service container: https://laravel.com/docs/container — DI and binding interfaces to implementations.
- `spatie/laravel-data`: https://github.com/spatie/laravel-data — compare against your hand-built DTOs.

---

## Validation, async, webhooks

Weeks 2 and 7.

- Laravel validation and Form Requests: https://laravel.com/docs/validation
- Laravel queues: https://laravel.com/docs/queues
- Laravel events: https://laravel.com/docs/events
- PostgreSQL SELECT and SKIP LOCKED: https://www.postgresql.org/docs/current/sql-select.html — the locking clause that makes a database job queue work.
- Stripe webhooks: covered in the Stripe docs alongside the API reference above.
- Paystack webhooks: https://paystack.com/docs/payments/webhooks/ — note the `x-paystack-signature` HMAC SHA512 verification.

---

## Security, operations

Cross-cutting.

- OWASP Top 10: https://owasp.org/www-project-top-ten/ — the baseline web security checklist.
- PostgreSQL CREATE INDEX (see `CONCURRENTLY`): https://www.postgresql.org/docs/current/sql-createindex.html — building indexes without locking the table.
- Laravel mass assignment (Eloquent docs) and rate limiting (routing and middleware docs), both under https://laravel.com/docs.

---

## Extension

Extension weeks 9 to 13.

- Laravel Sanctum (token auth): https://laravel.com/docs/sanctum
- Laravel authorization (policies and gates): https://laravel.com/docs/authorization
- Laravel cache and Redis: https://laravel.com/docs/cache and https://laravel.com/docs/redis
- PHPStan: https://phpstan.org — Larastan, the Laravel extension: https://github.com/larastan/larastan
- Laravel Pint (PSR-12 formatting): https://laravel.com/docs/pint
- Rector (automated refactoring): https://getrector.com
- Docker: https://docs.docker.com
- GitHub Actions: https://docs.github.com/actions
- The Twelve-Factor App: https://12factor.net — the baseline for config, deploys, and process model.
- k6 load testing: https://k6.io

---

## Testing

Weeks 4, 6, 8.

- Pest: https://pestphp.com — the modern Laravel test framework.
- Laravel testing: https://laravel.com/docs/testing — HTTP tests, mocking, factories.
- Fowler, The Practical Test Pyramid: https://martinfowler.com/articles/practical-test-pyramid.html

---

## System design

Week 8.

- Designing Data-Intensive Applications, Martin Kleppmann. Book. The foundation under most answers.
- System Design Interview volumes 1 and 2, Alex Xu. Books. The standard prep.
- The System Design Primer: https://github.com/donnemartin/system-design-primer — large, free, well organized.
- ByteByteGo: https://bytebytego.com — digestible pattern explainers.
- PostgreSQL partitioning: https://www.postgresql.org/docs/current/ddl-partitioning.html — for the scaling document.
