# Week 6, Day 3: Stripe implementation with the normalized ChargeResult

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Write the `StripePaymentGateway` implementation.** Against the interface you defined on Day 2. Use the official Stripe SDK for the HTTP work; the SDK is the concrete detail, not your interface. Stripe's secret key lives in the environment, never in code or git — this is the single most common way secrets leak. See [craft-reference.md → security](../craft-reference.md#security).

2. **Map Stripe's response into your normalized `ChargeResult` DTO.** Stripe returns its own object shape — status codes, `payment_intent` IDs, `client_secret`. That shape does not leak into your service layer. The mapping is the whole point of the DTO: your caller sees `ChargeResult`, not `Stripe\PaymentIntent`. See [craft-reference.md → DTOs](../craft-reference.md#dtos).

3. **Handle failure modes explicitly.** Network errors, declined cards, rate limits — each maps to a defined `ChargeResult` status or throws a domain exception. The service layer should never have to `try { } catch (Stripe\Exception\...)`.

4. **Pass the idempotency key through.** Stripe supports its own idempotency header. Use it. The key you generated in Week 2 rides on the outgoing HTTP call, so a retry from your side does not produce two charges on their side. This is the dual-write problem in the flesh: your DB commit and the Stripe HTTP call are two writes that cannot be atomically bound — the idempotency key is what makes retrying the second half safe. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).
   - Stripe idempotent requests: https://docs.stripe.com/api/idempotent_requests

## Cross-cutting reminders

- **DTOs**: `ChargeResult` normalizes Stripe's shape so the caller never touches `Stripe\PaymentIntent`. See [craft-reference.md → DTOs](../craft-reference.md#dtos).
- **Dual-write problem**: DB commit plus Stripe HTTP call are the two writes; the idempotency key on the outgoing request is what makes retrying safe. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).
- **Security**: Stripe secret keys live in the environment, never in code or git. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None.
