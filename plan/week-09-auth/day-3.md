# Week 9, Day 3: Scope bills and contributions to the authenticated user

## Start-of-day prompt

None.

## Today's work

1. **Scope bills and contributions to the authenticated user.** A user should only see and act on their own bills and their own contributions. This is not a UI concern — it is enforced server-side, in the query and in the authorization layer. Scoping is the concrete way you enforce "a user can only act on their own bills"; a missing scope is a data-leak vulnerability. See [craft-reference.md → security](../craft-reference.md#security).

2. **Prefer global scopes or explicit `where user_id = ?` in the repository** over relying on controller filters. The repository is the right place because the domain already talks through it (from Week 5). Anything that bypasses the repository must also enforce the scope; keep the escape hatches few and named.

3. **Distinguish ownership from participation.** A Bill has a creator and it has contributors. Read access for a contributor is not the same as settle access for the creator. Write down the rule per resource before you code it.

4. **Verify the scope with a query log.** Every read of a Bill or contribution must include the user filter. If you find one that does not, that is a data leak.

## Cross-cutting reminders

- **Security**: scoping bugs are the most common cause of "one user reads another user's data" incidents. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Review runs at the end of Day 6.
