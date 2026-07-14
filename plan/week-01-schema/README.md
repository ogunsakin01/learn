# Week 1: Design the schema yourself on PostgreSQL

**Goal:** a data model you designed and can defend, on Postgres, with the domain language set.

## Days

- [ ] [Day 1: Install the stack, learn normalization](day-1.md) — Prompt 1 at start on data modeling and schema design.
- [ ] [Day 2: Money handling and the Money value object](day-2.md) — no prompt, paper work.
- [ ] [Day 3: Ubiquitous language, aggregate root, and the audit log](day-3.md) — no prompt.
- [ ] [Day 4: Columns and Postgres types](day-4.md) — no prompt.
- [ ] [Day 5: Write the migrations](day-5.md) — Prompt 2 at end, review of the migrations.
- [ ] [Day 6: Fix review findings, then defense paragraphs](day-6.md) — no prompt.
- [ ] [Day 7: Grill on the schema and aggregate boundary](day-7.md) — Prompt 3, then Prompt 4 on indexing if going deeper.

## Prompt rhythm

Day 1 start: Prompt 1 on data modeling and schema design. Day 5 end: Prompt 2 on your migrations, then fix on Day 6. Day 7: Prompt 3 to grill the schema, then Prompt 4 if you want to go deeper on indexing.

## Threads

DDD (ubiquitous language, aggregate root, first value object). Postgres types.

## Reading

SQL Antipatterns (Karwin), normalization chapters. Use The Index Luke, start. PostgreSQL docs on data types. Domain-Driven Design Distilled (Vernon) for the vocabulary. Full list in [resources.md → schema, indexing](../resources.md#schema-indexing).

## You must be able to answer

- Why floats are wrong for money and what you use instead.
- Why the Bill is the aggregate root and what invariant it protects.
- Why the audit log exists in the schema from day one instead of being added later.
- The tradeoffs of storing structured event data as JSONB versus typed columns.
- Every column, type, constraint, and index choice in your schema.

## Done when

Migrations exist, the aggregate root is named, the audit log table exists alongside the domain tables, and you can defend every column and type out loud.
