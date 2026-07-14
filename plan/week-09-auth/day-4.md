# Week 9, Day 4: Authorization policies for view, contribute, settle

## Start-of-day prompt

None.

## Today's work

1. **Write a `BillPolicy`.** One class, one aggregate, one set of decisions. Methods: `view`, `contribute`, `settle`. Each returns true or false based on the acting user and the target Bill. This is where role- and relationship-based rules live. The policy holding exactly one aggregate's authorization rules is SRP in a concrete, testable form, and the policy layer itself is the security control on top of authentication. See [craft-reference.md → SOLID](../craft-reference.md#solid) and [craft-reference.md → security](../craft-reference.md#security).

2. **Wire the policy into the controllers via `authorize`.** The controller only asks the policy for permission — it does not encode the rule itself. That keeps the controller thin and lets the policy be tested in isolation.

3. **Think about the rules explicitly:**
   - View: creator or any contributor.
   - Contribute: any authenticated user the creator has invited (or, if you keep it open, any authenticated user, with a note in DESIGN.md about that choice).
   - Settle: creator only. And only if the Bill is not already settled — but note that the "already settled" check is a domain invariant, not an authorization rule. Keep the split clean: the policy answers "is this user allowed to settle?", the aggregate answers "can this Bill be settled right now?". See [craft-reference.md → validation](../craft-reference.md#validation).

4. **Reading:**
   - Laravel authorization (policies and gates): https://laravel.com/docs/authorization
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **Security**: authorization is the second half of the security posture; authentication only tells you who is asking. See [craft-reference.md → security](../craft-reference.md#security).
- **SOLID**: the policy is a single-responsibility class — one aggregate's authorization decisions, nothing else. See [craft-reference.md → SOLID](../craft-reference.md#solid).
- **Validation**: the "already settled" check is a domain invariant on the aggregate, not an authorization rule on the policy. The Form Request guards shape, the policy guards permission, the aggregate guards invariants — three layers, three responsibilities. See [craft-reference.md → validation](../craft-reference.md#validation).

## End-of-day prompt

None. Review runs at the end of Day 6.
