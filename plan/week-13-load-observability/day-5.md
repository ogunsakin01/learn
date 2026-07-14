# Week 13, Day 5: OpenAPI spec and README polish

## Start-of-day prompt

None.

## Today's work

1. **Write an OpenAPI spec for the API.** By hand. It is not much of a surface — a handful of endpoints for bills, contributions, settlements, plus the webhook receivers. Writing the YAML yourself teaches you what OpenAPI can and cannot express (request bodies, response schemas, auth schemes, error shapes, versioning). This is the Week 2 API-design work made formal — status codes, idempotency semantics, error shape, versioning — all promoted from convention into contract. See [craft-reference.md → API design](../craft-reference.md#api-design).
   - Alternatively, generate from PHP attributes with a tool like `zircote/swagger-php`, but read the generated output before you ship it.

2. **Nail the error response shape.** Every endpoint returns errors in one consistent shape (this was the Week 2 API design item). Document it once in the spec, reference it from every operation.

3. **Document authentication.** Sanctum tokens (Week 9, if you did it) or whatever you settled on. Which header, what token format, what a 401 looks like versus a 403.

4. **Polish the README.** The reader is either an interviewer skimming your GitHub for 90 seconds or a future you re-reading in six months. Both need:
   - One paragraph on what the project is and why it exists.
   - A quick-start (`docker compose up`, `php artisan migrate`, `php artisan test`).
   - A link to DESIGN.md for the decisions.
   - A link to the OpenAPI spec.
   - A link to the deployed URL if it is up.
   - The load-test numbers from Day 2.
   
   Do not oversell. Do not undersell either.

5. **Commit.** `week 13: openapi spec, readme polish`.

## Cross-cutting reminders

- **API design**: the OpenAPI spec is the formal statement of the API — status codes, error shape, auth, versioning, idempotency. See [craft-reference.md → API design](../craft-reference.md#api-design).

## End-of-day prompt

None. DESIGN.md finalization and review tomorrow.
