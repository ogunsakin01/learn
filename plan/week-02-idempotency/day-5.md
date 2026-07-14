# Week 2, Day 5: PaymentData DTO and the domain service

## Start-of-day prompt

None. Continuation of the endpoint arc.

## Today's work

1. **Add the `PaymentData` DTO.** A plain readonly PHP class. Fields: amount (Money value object), currency (or fold into Money), idempotency key, bill ID, actor. Immutable, typed. Built once from the validated Form Request, then passed everywhere downstream. See [craft-reference.md → dtos](../craft-reference.md#dtos).

2. **Build the request-to-DTO boundary.** The Form Request validates; the controller pulls validated data and constructs the DTO; the DTO is what the domain service receives. No arrays crossing the boundary. Read up on PHP `readonly` classes if you have not: https://www.php.net/manual/en/language.oop5.basic.php#language.oop5.basic.class.readonly.

3. **Move the charge logic into a domain service.** A single class, one use case (`RecordContribution` or similar). It receives the DTO, loads the Bill through a (soon-to-exist) repository or Eloquent directly for now, calls the aggregate method that enforces the invariant, writes the audit entry, and returns the result. Nothing in the controller beyond coordination. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd) and [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

4. **Point at SRP.** After this refactor: the controller coordinates, the Form Request validates shape, the DTO carries typed data, the domain service holds the use case, the aggregate holds the invariant. Each class has one reason to change. See [craft-reference.md → solid](../craft-reference.md#solid).

5. **Commit.** `week 2: PaymentData DTO and domain service`.

## Cross-cutting reminders

- **DTOs**: `PaymentData` is the typed boundary from validated request into the domain. See [craft-reference.md → DTOs](../craft-reference.md#dtos).
- **Tactical DDD**: the domain service owns the use case; the aggregate owns the invariant. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).
- **SOLID**: SRP split across controller, Form Request, DTO, domain service, and aggregate. See [craft-reference.md → SOLID](../craft-reference.md#solid).
- **Audit log**: still one transaction. Moving code around does not change the rule. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Security**: with the DTO in place, mass assignment is closed off by construction. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Full-week review is tomorrow.
