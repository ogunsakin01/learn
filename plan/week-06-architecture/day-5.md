# Week 6, Day 5: Pull the tactical DDD layer into shape, and know where it is overkill

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Pull everything into shape.** Thin controllers that only coordinate. Domain services for use cases. The aggregate enforcing invariants. Repositories for persistence. DTOs at every boundary. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd) and [craft-reference.md → SOLID](../craft-reference.md#solid).

2. **Walk through each SOLID letter and point at a real line.**
   - **S**: the controller only coordinates; the Form Request only validates shape; the service holds one use case; the value object holds one concept.
   - **O**: adding Paystack next to Stripe changed no caller.
   - **L**: `FakePaymentGateway`, `StripePaymentGateway`, `PaystackPaymentGateway` are all swappable.
   - **I**: the `PaymentGateway` interface is minimal, no fat methods.
   - **D**: the service depends on `PaymentGateway` and `BillRepository`, never on Stripe SDK or Eloquent directly.

3. **Then, with the full tactical layer in front of you, articulate where it is overkill and say so out loud.**

   > A shared-bill app has essentially one aggregate. Wheeling in repositories, domain services, domain events, and value objects on ground this thin risks learning to *perform* DDD ceremony rather than feel where it earns its place, and a good interviewer smells cargo-culting instantly. You built the full layer here because the point is to learn the moves, not because an app this size demands them. The senior signal is being able to say exactly that: "I applied the whole pattern to learn it, but for a service this small a single service class over the model would ship the same behaviour with less machinery, and here is the size and team at which the machinery starts paying for itself." Knowing when *not* to reach for DDD is as much a senior signal as knowing the patterns.

   Write that thought into `DESIGN.md` in your own words. It is one of the highest-value paragraphs in the whole document.

4. **Reading, alongside the work:**
   - Refactoring Guru, Strategy pattern: https://refactoring.guru/design-patterns/strategy
   - `spatie/laravel-data`: https://github.com/spatie/laravel-data — compare against your hand-built DTOs.

## Cross-cutting reminders

- **SOLID**: today's job is being able to point at a real line for each letter — that is the interview payoff. See [craft-reference.md → SOLID](../craft-reference.md#solid).
- **Tactical DDD**: the honest paragraph about where the full layer is overkill on an app this size is itself a senior signal. See [craft-reference.md → tactical DDD](../craft-reference.md#tactical-ddd).

## End-of-day prompt

None.
