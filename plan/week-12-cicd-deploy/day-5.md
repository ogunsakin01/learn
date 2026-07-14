# Week 12, Day 5: Safe migrations in the deploy pipeline, zero-downtime and rollback

## Start-of-day prompt

None.

## Today's work

1. **Wire migrations into the deploy.** A "release" step (Fly release command, Railway pre-deploy, or a systemd `ExecStartPre` on a VPS) runs `php artisan migrate --force` before the new app version starts serving traffic. Never let the app boot against an unmigrated database.

2. **Apply the safe-migration rules from Week 5.** Every migration that hits production must be safe on a live table:
   - `CREATE INDEX CONCURRENTLY` for new indexes so writes are not blocked.
   - Additive migrations: add a nullable column, backfill in a separate migration, then enforce `NOT NULL` in a third. Never add a non-nullable column with a default in one step on a big table.
   - Rename columns via the two-write pattern (write to both old and new, backfill, cut over reads, then drop old). Never a straight `RENAME` in a live system with active writers.
   
   See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).

3. **Zero-downtime deploys, understand the model.** The host runs the new version alongside the old, health-checks the new one, then shifts traffic. Any migration that ships must be compatible with both the old and new app version running against the database simultaneously. This is why additive migrations matter — a `DROP COLUMN` shipped with the code that stopped writing to it will break the old version that is still serving requests during the cutover.

4. **Set up a rollback path.** Either:
   - Redeploy the previous image tag (Fly, Railway, most container hosts store the last N releases).
   - Keep migrations reversible where the state allows, so `php artisan migrate:rollback` is safe. Not every migration is reversible; when it is not, say so in the migration comment.
   
   Rollback that is not tested is not rollback. Do it once now in a lower environment.

5. **Commit.** `week 12: pipeline, deploy, safe migrations`.

## Cross-cutting reminders

- **Safe schema changes**: additive migrations, `CREATE INDEX CONCURRENTLY`, and the old-and-new-app-version compatibility rule. See [craft-reference.md → safe schema changes](../craft-reference.md#safe-schema-changes).
- **Security via secrets**: deploy credentials (deploy tokens, SSH keys) live in the CI Secrets store, not the workflow file. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Review runs tomorrow after the fix cycle.
