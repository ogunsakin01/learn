# Week 13, Day 3: Structured logging and the error tracker

## Start-of-day prompt

None.

## Today's work

1. **Instrument structured logging around payments.** Every payment attempt writes a log line with a consistent set of fields: request ID, user ID, bill ID, contribution amount (never card data), idempotency key, gateway used, gateway response ID, outcome. JSON, not string interpolation. Structured logs are the queryable side of observability — the reason you can answer "what happened to this one payment" without a debugger. See [craft-reference.md → observability](../craft-reference.md#observability).
   - Laravel logging: https://laravel.com/docs/logging — use a JSON channel or the `Monolog\Formatter\JsonFormatter`.

2. **Correlate across the request.** Every log line for the same request carries the same correlation ID (request ID or trace ID), so you can pull the full story of one payment out of the log stream. Middleware sets it; a logger context propagates it.

3. **Never log secrets or card data.** This is not optional. Card handling is delegated to the gateway; the app must never see or log a full PAN. Redact `Authorization` headers, webhook signatures, and gateway API keys from every log path. See [craft-reference.md → security](../craft-reference.md#security).

4. **Wire an error tracker, or know exactly where it slots in.** Sentry is the default choice for Laravel; Bugsnag and Honeybadger are alternatives. Install it or write the integration plan in DESIGN.md — either counts, as long as you can explain where uncaught exceptions go, how PII is scrubbed, and how you would triage a spike.

5. **Know the difference between logs, metrics, and traces.**
   - **Logs** are events with context. Great for "what happened to this one request."
   - **Metrics** are aggregated numbers over time. Great for "is the system healthy right now."
   - **Traces** are causal chains across services. Great for "where did the latency come from."
   
   You will not build a full tracing pipeline this week, but you must be able to say when you would reach for each.

## Cross-cutting reminders

- **Observability**: today is logs and error tracking. Metrics tomorrow, audit hardening tomorrow. See [craft-reference.md → observability](../craft-reference.md#observability).

## End-of-day prompt

None. Audit log and metrics tomorrow.
