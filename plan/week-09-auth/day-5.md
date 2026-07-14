# Week 9, Day 5: Per-user rate limiting on the payment endpoint

## Start-of-day prompt

None.

## Today's work

1. **Add per-user rate limiting on the payment endpoint.** Laravel's `throttle` middleware with a `RateLimiter` keyed on the authenticated user ID, not the IP. IP-based limits punish shared networks; user-based limits are what a money endpoint actually needs. Rate limiting on a payment endpoint is a security control against retry and credential-stuffing abuse, not a stability knob. See [craft-reference.md → security](../craft-reference.md#security).

2. **Pick numbers you can defend.** Something like 60 requests per minute per user on the contribution endpoint. Write the reasoning in DESIGN.md — what attack you are limiting (credential stuffing, brute retry, accidental client loop), and what a legitimate high-frequency user would still be able to do.

3. **Return a proper 429 with `Retry-After`.** Not a bare error. This is API design showing up again from Week 2.

4. **Reading:**
   - Laravel rate limiting is documented under the routing and middleware sections: https://laravel.com/docs

## Cross-cutting reminders

- **Rate limiting reappears here as a security control** (against retry and credential-stuffing style abuse), not just as a stability control. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Review runs at the end of Day 6.
