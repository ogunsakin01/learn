# Week 2, Day 4: Build the idempotent endpoint

## Start-of-day prompt

None. Build day.

## Today's work

1. **Store the key before processing.** The first thing the endpoint does is `INSERT` the idempotency key row (with request fingerprint and a "pending" status) inside a transaction. Not after the charge. Before. This is the whole point: the record of "I have seen this request" must exist before you do anything that costs money.

2. **Rely on the unique constraint.** The idempotency key column has the unique index you added in Week 1. On a duplicate, Postgres raises a constraint violation. Catch it, look up the existing row, and return the stored result. Do not check first, insert second — that is the broken pattern from yesterday.

3. **Fingerprint the request.** Store enough of the request payload with the key that a repeat with the *same* key but a *different* body is caught and rejected (409 Conflict). Stripe does this. Brandur explains why.

4. **Write the audit entry in the same transaction as the state change.** Every mutation on the Bill writes an append-only audit row inside the same DB transaction. This is the rule from Week 1, Day 3. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

5. **Return the right status codes.** 200 or 201 on the first success, the same 200/201 with the stored body on a repeat, 409 on a key reuse with a different payload, 422 on shape failure. See [craft-reference.md → api-design](../craft-reference.md#api-design).

6. **Commit.** Small, focused commit. `week 2: idempotent payment endpoint`.

## Cross-cutting reminders

- **Audit log**: the state change and the audit write live in one transaction. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Security**: rate-limit the endpoint with throttle middleware, and never log the raw payload or any secret. See [craft-reference.md → security](../craft-reference.md#security).
- **API design**: status codes chosen today are the contract. See [craft-reference.md → api-design](../craft-reference.md#api-design).

## End-of-day prompt

None. The DTO and domain service go in tomorrow; review comes Day 6.
