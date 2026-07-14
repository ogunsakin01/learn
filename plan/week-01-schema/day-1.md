# Week 1, Day 1: Install the stack, learn normalization

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning data modeling and schema design on PostgreSQL for a shared-bill
payments app by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain
the concept from first principles, the two or three standard approaches with the
tradeoffs between them, and the specific failure each approach prevents or causes.
Where it is relevant, explain how PostgreSQL handles it and how that differs from
MySQL, and how it relates to SOLID principles and to tactical DDD (aggregates,
value objects, repositories, domain services, domain events). Then list the exact
things I should be able to explain out loud once I have built it. Stop there. I
will build it and come back.
```

## Today's work

1. **Install the stack.**
   - Laravel (fresh app).
   - PostgreSQL (local install or Docker).
   - Pest (`composer require pestphp/pest --dev`, then init).
   - Point Laravel at the `pgsql` driver in `config/database.php` and `.env`.
   - Confirm `php artisan migrate` runs cleanly against Postgres, even with nothing to migrate.

2. **Read normalization basics** until you know *why* you normalize and *when* you would not.
   - SQL Antipatterns (Karwin), the normalization chapters. Book, no link.
   - PostgreSQL docs on data types (skim, for later): https://www.postgresql.org/docs/current/datatype.html
   - Full list in [resources.md → schema, indexing](../resources.md#schema-indexing).

## Cross-cutting reminders

None today — setup and reading.

## End-of-day prompt

None. You have not written code yet.
