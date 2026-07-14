# Week 1, Day 3: Ubiquitous language, aggregate root, and the audit log

## Start-of-day prompt

None. This is design work, still under Day 1's Prompt 1 session.

## Today's work

1. **Establish the ubiquitous language.** Name the entities and *use those names in code, tests, and DESIGN.md from now on*. Not "record" or "row". A **Bill** (the pooled balance), **contributions** (money paid in), a **settlement** (the moment the target is covered). Write the list somewhere permanent.

2. **Sketch relationships only. No columns yet.** Bill has many contributions. A settlement is a state of the Bill, or its own row — decide and defend. Draw it. Boxes and lines.

3. **Identify the aggregate root.** The Bill is the aggregate root and your consistency boundary. It owns the invariant that contributions cannot exceed the target and that a settled bill takes no more money. Write down, in one sentence, the invariant the Bill owns. The concurrency weeks (3 and 4) exist to protect this exact sentence — get it right now.

   See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

4. **Include the audit log as a first-class table in the sketch.** Not a bolt-on later.

   > **Why now:** a payments domain needs an append-only record of every state change on a bill for reconciliation and disputes. Once the aggregate exists, any state change you ship without an audit write is a bug the log exists to catch. Retrofitting an audit log after the aggregate has been mutating for weeks guarantees you miss events. Design the table alongside Bill and contributions. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

5. **Reading, if you want it today:**
   - Domain-Driven Design Distilled (Vernon) — the vocabulary chapters. Book.
   - Full list in [resources.md → architecture, SOLID, DDD](../resources.md#architecture-solid-ddd).

## Cross-cutting reminders

- **Audit log**: designed today as a peer of Bill and contributions. From Week 2 onwards, every mutation writes to it inside the same transaction.

## End-of-day prompt

None. Still design.
