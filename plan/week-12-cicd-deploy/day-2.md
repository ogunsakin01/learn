# Week 12, Day 2: GitHub Actions workflow for Pest, PHPStan, Pint

## Start-of-day prompt

None. Continuation of the CI/CD arc from Day 1.

## Today's work

1. **Write a GitHub Actions workflow** at `.github/workflows/ci.yml`. Triggers: `push` and `pull_request`.
   - GitHub Actions docs: https://docs.github.com/actions

2. **Jobs to run on every push and pull request:**
   - `pest` — the test suite.
   - `phpstan` — static analysis at the level you settled on in Week 11.
   - `pint` — formatting check in `--test` mode so it fails when files are unformatted rather than fixing them.

   CI is where the local pre-commit hook gets a second, non-optional enforcement pass — the standards apply the same on every push whether the hook ran or not. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).

3. **PHP setup.** Use `shivammathur/setup-php` — the canonical action. Cache Composer dependencies with `actions/cache` or the setup-php built-in cache. A cold pipeline is a slow one, and a slow one gets skipped.

4. **Fail loudly when any check fails.** Do not let a job succeed on a non-zero exit code. Do not swallow output. The value of a red build is that it is red.

5. **Concurrency control.** Add a `concurrency` block keyed on the branch, so a new push to a branch cancels the previous run. Saves minutes and mental load.

6. **Do not run the deploy yet.** This week the pipeline is checks only. Deploy comes Day 4.

## Cross-cutting reminders

- **PHP standards**: CI enforces Pest, PHPStan, and Pint on every push — the same standards the pre-commit hook enforces locally. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).
- **Security via secrets**: no secrets in the workflow file. `GITHUB_TOKEN` is auto-injected; anything else lives in repo Secrets. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Services against real engines tomorrow.
