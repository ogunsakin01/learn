# Week 3, Day 3: Postgres isolation levels vs MySQL

## Start-of-day prompt

None. Still under Day 1's Prompt 1 session.

## Today's work

1. **Read the Postgres isolation docs.** https://www.postgresql.org/docs/current/transaction-iso.html. Every word. This is a text an interviewer expects you to know.

2. **Write the four levels down in your own words.**
   - **READ UNCOMMITTED** — Postgres treats it as READ COMMITTED (it has no dirty reads at all). MySQL InnoDB actually permits dirty reads here.
   - **READ COMMITTED** — Postgres default. Each *statement* sees a fresh snapshot of committed data. Lost updates are possible.
   - **REPEATABLE READ** — Postgres implements this as **snapshot isolation**: the whole transaction sees one snapshot taken at the first read. Prevents non-repeatable and phantom reads, but write skew is still possible.
   - **SERIALIZABLE** — Postgres uses **Serializable Snapshot Isolation (SSI)** to catch write skew by aborting one of the conflicting transactions at commit. Correct but expensive.

3. **Read MySQL InnoDB for the contrast.**
   - Isolation: https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html
   - Locking: https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html
   
   Write down the contrast, cold: MySQL InnoDB defaults to **REPEATABLE READ**, and uses **next-key locks** (index-record plus gap) to prevent phantoms. Postgres uses MVCC snapshots. Two very different mechanisms for adjacent problems.

4. **Update DESIGN.md** with a Postgres-vs-MySQL isolation and locking table. This is a direct interview question in almost every senior loop.

5. **The sentence that ties the week together, memorise it.** *The same MVCC that lets readers not block writers is exactly why the naive check-then-update loses the update under READ COMMITTED, because each transaction reads its own snapshot and neither sees the other's write until too late.* This is the mechanic that breaks the aggregate invariant without a lock. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## Cross-cutting reminders

- **Tactical DDD**: isolation choice and lock choice both exist to defend the aggregate invariant. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **Audit log**: the audit write will live inside the locked transaction from tomorrow. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

## End-of-day prompt

None. Fix the race tomorrow.
