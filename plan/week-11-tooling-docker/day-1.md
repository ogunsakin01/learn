# Week 11, Day 1: The three tooling jobs — static analysis, linting, formatting

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning code quality tooling and containers for a Laravel payments app by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Concept first on the three jobs.** They overlap in reputation and do not overlap in practice.
   - **Static analysis** (PHPStan) finds type and logic errors without running the code. It reads your codebase as a whole and flags what would crash or misbehave at runtime.
   - **Linting** flags suspect patterns and style-adjacent smells that are not strictly wrong but usually are.
   - **Formatting** (Pint) enforces a style. Not opinion. Rules.
   - **Refactoring tooling** (Rector) automates mechanical changes across the codebase — upgrades, deprecations, pattern rewrites.

2. **Know what each catches and what it cannot.** Static analysis will not catch a wrong SQL query. A formatter will not catch a null dereference. A linter will not catch a design mistake. Each is a narrow tool. Together, they are how PSR-12 formatting and PSR-4 autoloading get enforced instead of hoped for. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).

3. **Reading:**
   - PHPStan: https://phpstan.org
   - Larastan: https://github.com/larastan/larastan
   - Laravel Pint: https://laravel.com/docs/pint
   - Rector: https://getrector.com
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **PHP standards**: PSR-12 formatting and PSR-4 autoloading are what the tooling enforces. See [craft-reference.md → PHP language and standards](../craft-reference.md#php-language-and-standards).

## End-of-day prompt

None. You have not written code yet.
