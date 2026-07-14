# Week 9: Authentication and authorization

**Goal:** a properly secured API, authenticated and authorized, not an open endpoint.

## Days

- [ ] [Day 1: Concept first on auth and authz](day-1.md) — Prompt 1 at start on authentication and authorization.
- [ ] [Day 2: Token authentication with Sanctum](day-2.md) — no prompt.
- [ ] [Day 3: Scope bills and contributions to the authenticated user](day-3.md) — no prompt.
- [ ] [Day 4: Authorization policies for view, contribute, settle](day-4.md) — no prompt.
- [ ] [Day 5: Per-user rate limiting on the payment endpoint](day-5.md) — no prompt.
- [ ] [Day 6: Auth tests, then review](day-6.md) — Prompt 2 at end on the auth layer.
- [ ] [Day 7: Grill on auth versus authz, tokens, and access-control models](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on authentication and authorization. Day 6 end: Prompt 2 on the auth layer. Day 7 end: Prompt 3, then Prompt 4.

## Threads

Security. SOLID (authorization as policy objects).

## Reading

Laravel Sanctum. Laravel authorization (policies and gates). OWASP. Full list in [resources.md → extension](../resources.md#extension) and [resources.md → security, operations](../resources.md#security-operations).

## You must be able to answer

- Stateless versus session auth.
- Where authorization belongs.
- Role-based versus attribute-based access at a high level.
- How you test authorization.

## Done when

Endpoints reject the unauthenticated and forbid the wrong user, proven by tests.
