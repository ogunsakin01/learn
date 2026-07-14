# Week 11, Day 5: Dockerfile for the app

## Start-of-day prompt

None.

## Today's work

1. **Write a Dockerfile for the app.** By hand. Do not copy a boilerplate you cannot explain line by line.
   - Docker docs: https://docs.docker.com

2. **Understand what each layer does.** A Dockerfile is a sequence of instructions, each producing a cached image layer. Ordering matters: put slow-changing steps (installing PHP extensions, `composer install --no-dev` on a locked `composer.lock`) above fast-changing ones (copying application source). Reorder them and every source change busts the composer cache.

3. **Decide on a base image.** Options:
   - Official `php:8.x-fpm` or `php:8.x-cli`.
   - Official `php:8.x-fpm-alpine` for size, with the Alpine pitfalls (musl libc, extension build differences).
   - A pre-built Laravel image like `serversideup/php`.
   
   Pick one, defend it.

4. **PHP extensions the app needs.** At minimum: `pdo_pgsql`, `bcmath` or `intl` depending on your Money handling, `redis` if you install the extension rather than using the pure-PHP client. Install them explicitly. Do not rely on defaults.

5. **Multi-stage build if you want the production image lean.** A build stage runs `composer install`, the final stage copies only the vendor directory and source it needs. This is where image size drops from hundreds of megabytes to tens.

6. **Do not bake secrets into the image.** Environment configuration comes at runtime, not build time. This is a twelve-factor rule you will apply properly in Week 12.

## Cross-cutting reminders

None new today.

## End-of-day prompt

None. Compose and review tomorrow.
