# Week 9, Day 1: Concept first on auth and authz

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning authentication and authorization, stateless token versus session, and where authorization belongs by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Concept first on auth.** Authentication is who you are, authorization is what you can do. Confuse them and every explanation you give will be wrong. Say the difference out loud. Both halves are security concerns — a money endpoint that gets either wrong is the same size of bug. See [craft-reference.md → security](../craft-reference.md#security).

2. **Stateless token versus session.** Sessions keep state on the server (cookie carries an opaque ID, server looks up the user). Tokens (Sanctum's simple opaque tokens, or JWTs) can carry the identity themselves. Know the tradeoffs: revocation, scaling, CSRF surface, storage on the client, and what "stateless" actually means in practice (usually not fully stateless once you need revocation).

3. **Where authorization belongs.** Not in the controller. Policies (per-model authorization classes) and gates (closures for one-offs) are Laravel's answer, and they slot naturally into the aggregate-and-service picture from earlier weeks. A policy is a single-responsibility class — that is SOLID in a small, concrete form.

4. **Reading:**
   - Laravel Sanctum: https://laravel.com/docs/sanctum
   - Laravel authorization (policies and gates): https://laravel.com/docs/authorization
   - OWASP Top 10: https://owasp.org/www-project-top-ten/
   - Full lists in [resources.md → extension](../resources.md#extension) and [resources.md → security, operations](../resources.md#security-operations).

## Cross-cutting reminders

- **Auth is security**: this is not a feature-flag week, it is the security week. A money endpoint without auth is a bug the size of the whole app. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Review runs at the end of Day 6.
