# Week 7, Day 5: Paystack webhook, same idempotency shape

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Build the Paystack webhook handler.** The same shape as Stripe's, on a different endpoint. Verify `x-paystack-signature` (HMAC SHA512 of the raw body with your secret key) before trusting the payload. Same rule as Stripe: no verification, no trust, no state change. See [craft-reference.md → security](../craft-reference.md#security).
   - Paystack webhooks: https://paystack.com/docs/payments/webhooks/

2. **Same idempotency idea, keyed on Paystack's event identifier.** Insert into the same `webhook_events` table with `provider = 'paystack'` and the event ID; on a unique-violation, return 200 and do nothing.

3. **Map into the same domain language.** A Paystack `charge.success` and a Stripe `payment_intent.succeeded` are the same domain event to the Bill: `PaymentReceived`. The webhook handler is the translator; the Bill does not know or care which provider it came from. This is the ubiquitous language paying off.

4. **Write the audit entry inside the same transaction as the state change**, with the actor `webhook:paystack:<event_id>`. Same rule as the Stripe path — the provider changes, the audit invariant does not. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

5. **Confirm you changed no domain code.** Adding a second webhook provider should have touched the webhook layer only — the Bill aggregate, the domain services, and the repository stayed identical. This is open/closed applied to the ingress side of the two-provider design.

## Cross-cutting reminders

- **Security**: Paystack's HMAC SHA512 verification, secret in the environment. See [craft-reference.md → security](../craft-reference.md#security).
- **Audit log**: written inside the same transaction as the state change. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Observability**: same structured log shape as Stripe, tagged with `provider=paystack`. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None.
