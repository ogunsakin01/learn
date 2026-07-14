# Week 2, Day 1: Form Requests and where validation lives

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning validation layering in Laravel (Form Requests versus domain
invariants) by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Learn Form Requests.** Read the Laravel docs: https://laravel.com/docs/validation. Focus on the Form Request class: `rules()`, `authorize()`, `messages()`, `prepareForValidation()`, and how it hooks into the controller through method injection.

2. **Scaffold one Form Request per endpoint.** `php artisan make:request StoreContributionRequest`. Filling it in is your job, no AI. Validate only input shape: required, types, ranges, formats, currency code, minimum amount. Do not touch anything that requires database state.

3. **Move validation out of the controller.** If any request-shape check lives in the controller, delete it and put it in the Form Request. The controller only coordinates.

4. **Read [craft-reference.md → validation](../craft-reference.md#validation).** Internalise the split. The Form Request guards the shape, the aggregate guards the invariant. That split is a common interview probe.

## Cross-cutting reminders

- **Validation**: Form Request guards input shape today; the aggregate invariant comes tomorrow. See [craft-reference.md → validation](../craft-reference.md#validation).
- **Security**: never pass raw request input into Eloquent `create` or `update`. Mass assignment is the most common Laravel hole. See [craft-reference.md → security](../craft-reference.md#security).
- **API design**: pick your error response shape today and stick to it — Form Request failures return 422 by default; know why. See [craft-reference.md → api-design](../craft-reference.md#api-design).

## End-of-day prompt

None. You will review at the end of Day 6, once the endpoint is built.
