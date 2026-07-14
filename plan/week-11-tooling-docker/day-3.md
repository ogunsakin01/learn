# Week 11, Day 3: Pint and Rector

## Start-of-day prompt

None.

## Today's work

1. **Add Laravel Pint for PSR-12 formatting.** Pint is an opinionated PHP-CS-Fixer wrapper with a Laravel-flavoured preset. This is the mechanical enforcement of PSR-12 on this project — no arguments, no drift. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).
   - Laravel Pint: https://laravel.com/docs/pint
   - Run `./vendor/bin/pint` and read the diff before accepting. Then run it again — clean.

2. **Pick a preset and commit to it.** `laravel`, `psr12`, or a custom `pint.json`. Do not oscillate. The value of a formatter is that nobody argues about style ever again.

3. **Try Rector.** Rector performs automated refactors — deprecations, upgrades, mechanical rewrites. Run it in dry-run mode first.
   - Rector: https://getrector.com

4. **Read Rector's suggestions before accepting any.** Automated refactors that touch domain code deserve human review. This is a tool, not a licence to skip understanding. If a suggested refactor changes behaviour rather than shape, reject it.

5. **Decide which Rector rulesets you actually want on all the time.** The `dead-code` and `code-quality` sets are usually safe. Framework-upgrade sets are one-shot, not standing.

## Cross-cutting reminders

- **PHP standards**: Pint is the enforcement mechanism for PSR-12 in this project. See [craft-reference.md → PHP language and standards](../craft-reference.md#php-language-and-standards).

## End-of-day prompt

None. Pre-commit hook tomorrow.
