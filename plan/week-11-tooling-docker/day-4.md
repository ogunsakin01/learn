# Week 11, Day 4: Pre-commit hook wiring all three

## Start-of-day prompt

None.

## Today's work

1. **Wire PHPStan, Pint, and (optionally) Rector into a pre-commit hook.** Options:
   - A hand-written `.git/hooks/pre-commit` shell script.
   - `captainhook/captainhook` or `brianium/paratest` style tooling for PHP-specific hook management.
   - A generic runner like `pre-commit` (the framework).
   
   Pick one and defend it. The point is that the hook runs on every commit, not the tool used to install it. The hook is where PSR-12 and PSR-4 stop being aspirations and start being conditions of commit. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).

2. **Order matters.** Pint first (formats), then PHPStan (analyses the formatted code), then tests if you want them in the hook (many teams keep tests in CI only for speed).

3. **Fail loudly.** A hook that exits 0 on error is worse than no hook. If PHPStan reports an error, the commit must not go through.

4. **Understand why local is better than CI-only.** Catching a formatting or typing error in a pre-commit hook takes seconds. Catching it in CI takes a push, a wait, a red build, a context switch, and another push. The hook is the fast feedback loop; CI is the safety net, not the primary check.

5. **Document the hook in the README or a `CONTRIBUTING.md`.** New checkouts need to know how to install it. A hook that only exists on your machine catches nothing.

## Cross-cutting reminders

- **PHP standards**: the hook is the enforcement point for PSR-12 and PSR-4 on every commit. See [craft-reference.md → PHP language and standards](../craft-reference.md#php-language-and-standards).

## End-of-day prompt

None. Docker starts tomorrow.
