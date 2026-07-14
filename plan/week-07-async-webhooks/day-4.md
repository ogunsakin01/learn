# Week 7, Day 4: Stripe webhook, idempotent and signature-verified

## Start-of-day prompt

None. Continuation of Day 1's Prompt 1 session.

## Today's work

1. **Build the Stripe webhook handler.** A POST endpoint that receives Stripe events (`payment_intent.succeeded`, `charge.refunded`, and whatever else you care about) and moves the Bill state accordingly.

2. **Verify the signature before trusting anything.** Stripe signs the request body with a shared secret and sends the signature in a header. Verify it in a middleware or the first line of the controller. An unverified webhook lets anyone POST a "payment succeeded" and mark a bill paid. This is not optional. See [craft-reference.md → security](../craft-reference.md#security).

3. **Idempotent on the event ID.** Stripe delivers the same event more than once when the network hiccups on the acknowledgement. The event has an ID — store it in a `webhook_events` table with a unique constraint on `(provider, event_id)`. Insert first; on a unique-violation, return 200 and do nothing. This is exactly the idempotency pattern from Week 2, applied to webhook delivery.

4. **Write the audit entry inside the same transaction as the state change.** Every webhook-driven mutation of the Bill writes to the append-only audit log with the event type, the actor (`webhook:stripe:<event_id>`), and the before/after. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).

5. **Return 200 quickly.** Do the state change synchronously in the transaction; queue anything non-essential (notifications, downstream sync). Stripe treats a slow response or a non-2xx as a delivery failure and retries — a slow handler multiplies your load.

## Cross-cutting reminders

- **Security**: webhook signature verification, and the secret lives in the environment, never in git. See [craft-reference.md → security](../craft-reference.md#security).
- **Audit log**: written inside the same transaction as the state change. See [craft-reference.md → the audit log](../craft-reference.md#the-audit-log).
- **Dual-write problem**: this is the reconciliation half of the fix. The payment endpoint (Week 2) committed local state and initiated the charge; the webhook is how the world tells you what actually happened. See [craft-reference.md → the dual-write problem](../craft-reference.md#the-dual-write-problem).
- **Observability**: structured log lines around the webhook path — event received, signature verified, state changed, event ID. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None.
