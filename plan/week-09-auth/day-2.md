# Week 9, Day 2: Token authentication with Sanctum

## Start-of-day prompt

None. Continuation of Day 1's auth arc.

## Today's work

1. **Add token authentication with Laravel Sanctum.** Install, publish config and migrations, run them. Understand what tables Sanctum adds (`personal_access_tokens`) and what the token string actually is.

2. **Protect the payment endpoints.** `auth:sanctum` middleware on the routes that touch money. Verify with a curl request that no token gets 401, a valid token gets 200 (or the appropriate response). This is the concrete security control on the highest-value surface in the app. See [craft-reference.md → security](../craft-reference.md#security).

3. **Understand the token lifecycle.** How you issue one, how you revoke one, and where the hashed token lives in the database. Never log the plaintext token.

4. **Reading:**
   - Laravel Sanctum: https://laravel.com/docs/sanctum
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **Security**: the token is a credential. Treat it like a password: hashed at rest, never in logs, transmitted over TLS only. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Review runs at the end of Day 6.
