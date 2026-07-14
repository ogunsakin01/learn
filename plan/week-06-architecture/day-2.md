# Week 6, Day 2: Define the gateway interface and the fake first

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Define the `PaymentGateway` interface.** Minimal. What does a caller actually need? A method to charge, a method to verify a webhook payload, and nothing else. Interface segregation applies — no fat "do everything" interface. See [craft-reference.md → SOLID](../craft-reference.md#solid).

2. **Design the input and output DTOs.** The input is a typed charge (`ChargeInput` or similar) carrying `Money`, an idempotency key, and any provider-agnostic metadata. The output is a normalized `ChargeResult` with the fields both Stripe and Paystack can populate: a status, a provider transaction ID, and any redirect or client-secret data the caller needs. The normalized result is exactly what makes the two-provider design clean. See [craft-reference.md → DTOs](../craft-reference.md#dtos).

3. **Write the fake implementation first.** `FakePaymentGateway` returns canned results without touching the network. Wire it up in tests. This is the payoff of the interface — the caller does not know whether it is real or fake. That is Liskov substitution in action: any implementation is swappable without the caller breaking. See [craft-reference.md → SOLID](../craft-reference.md#solid).

4. **Bind the interface in a service provider.** In `local` or `testing`, bind to the fake. In production, later, bind to whichever concrete you resolve at runtime (Stripe or Paystack). This is where Liskov substitution becomes concrete.

## Cross-cutting reminders

- **SOLID**: interface segregation on the gateway interface (nothing a caller does not need), Liskov substitution proved by the fake. See [craft-reference.md → SOLID](../craft-reference.md#solid).
- **DTOs**: the interface's input and output are DTOs — the whole two-provider design depends on that normalization. See [craft-reference.md → DTOs](../craft-reference.md#dtos).

## End-of-day prompt

None.
