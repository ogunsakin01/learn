# Week 11: Code quality tooling and Docker

**Goal:** a codebase a machine keeps honest, running entirely in containers.

## Days

- [ ] [Day 1: The three tooling jobs — static analysis, linting, formatting](day-1.md) — Prompt 1 at start on tooling and containers.
- [ ] [Day 2: PHPStan with Larastan, level by level](day-2.md) — no prompt.
- [ ] [Day 3: Pint and Rector](day-3.md) — no prompt.
- [ ] [Day 4: Pre-commit hook wiring all three](day-4.md) — no prompt.
- [ ] [Day 5: Dockerfile for the app](day-5.md) — no prompt.
- [ ] [Day 6: docker compose for the full stack](day-6.md) — Prompt 2 at end on the Dockerfile and compose.
- [ ] [Day 7: Grill on tooling and containers](day-7.md) — Prompt 3, then Prompt 4.

## Prompt rhythm

Day 1 start: Prompt 1 on tooling and containers. Day 6 end: Prompt 2 on the Dockerfile and compose. Day 7 end: Prompt 3, then Prompt 4.

## Threads

Code quality, operations.

## Reading

PHPStan, Larastan, Laravel Pint, Rector, Docker docs (Dockerfile and compose). Full list in [resources.md → extension](../resources.md#extension).

## You must be able to answer

- The difference between static analysis, linting, and formatting.
- What PHPStan levels mean and why you raise them one at a time.
- An image versus a container.
- What a Dockerfile layer is and why layer order matters for build caching.
- Why catching quality issues in a pre-commit hook is better than catching them in CI.

## Done when

PHPStan passes at a high level, Pint reports clean, and `docker compose up` runs the entire stack.
