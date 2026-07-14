# Week 11, Day 2: PHPStan with Larastan, level by level

## Start-of-day prompt

None. Continuation of the tooling arc from Day 1.

## Today's work

1. **Install PHPStan with Larastan.** Larastan is the Laravel extension that teaches PHPStan about facades, Eloquent magic, and container bindings that vanilla PHPStan does not understand.
   - Larastan: https://github.com/larastan/larastan

2. **Start at a low level.** PHPStan runs at levels 0 through 9 (plus `max`). Start at level 0 or 1 and get to zero errors before raising. Do not skip levels.

3. **Fix every error yourself.** Understand each fix. Do not silence it with `@phpstan-ignore` unless you can defend why. A `baseline` is fine to freeze existing debt while you clean, but new code should not add to it. Every fix is a type-system lesson: nullable-handling, generics, variance. See [craft-reference.md → PHP standards](../craft-reference.md#php-language-and-standards).

4. **Raise the level one step at a time.** Each level introduces new checks. Read what each level adds before you jump — a level bump is a design conversation, not a config change. See the level table in the PHPStan docs.

5. **Common Laravel wins Larastan gives you:** correct Eloquent return types via generics, container-resolved facade types, and detecting missing relationship methods.

## Cross-cutting reminders

- **PHP standards**: PHPStan errors are often type-system violations that PSR-12 formatting alone cannot catch. See [craft-reference.md → PHP language and standards](../craft-reference.md#php-language-and-standards).

## End-of-day prompt

None. Formatting and refactoring tomorrow.
