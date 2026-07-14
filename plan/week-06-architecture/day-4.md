# Week 6, Day 4: Paystack implementation, open/closed live

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Write the `PaystackPaymentGateway` against the same interface.** Same interface, same DTOs, different HTTP calls, different response mapping. Paystack's shape is different from Stripe's — the mapping normalizes it into the same `ChargeResult` the caller already knows, and that normalization is the whole reason two providers cost you no branching upstream. See [craft-reference.md → DTOs](../craft-reference.md#dtos).

2. **Verify you changed no callers.** The service that used `PaymentGateway` on Day 3 still uses `PaymentGateway`. You added a new class; you did not edit any existing class that consumed the interface. This is open/closed live. See [craft-reference.md → SOLID](../craft-reference.md#solid).

3. **Wire the container to pick the right provider.** Contextual binding, a factory, or a config-driven resolver — whichever fits. The caller asks the container for `PaymentGateway` and gets whichever concrete configuration says.

4. **Confirm Liskov.** Swap `StripePaymentGateway` for `PaystackPaymentGateway` in a test that used Stripe. It should pass without any change to the test's assertions on the returned `ChargeResult`. If it does not, the interface or the DTO is leaky.

## Cross-cutting reminders

- **DTOs**: same `ChargeInput` and `ChargeResult`, second provider — this is where the normalization pays for itself. See [craft-reference.md → DTOs](../craft-reference.md#dtos).
- **SOLID**: open/closed proved by construction — adding Paystack touched no caller. See [craft-reference.md → SOLID](../craft-reference.md#solid).

## End-of-day prompt

None.
