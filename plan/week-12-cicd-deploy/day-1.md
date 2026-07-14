# Week 12, Day 1: CI vs CD and the twelve-factor app

## Start-of-day prompt

Paste this into Claude Code before you start:

```
I am learning CI/CD and deployment for a Laravel payments app by building it myself in a Laravel project on PostgreSQL. Do not
write any code, do not design my solution, and do not edit any files. Explain the
concept from first principles, the two or three standard approaches with the tradeoffs
between them, and the specific failure each approach prevents or causes. Where it is
relevant, explain how PostgreSQL handles it and how that differs from MySQL, and how it
relates to SOLID principles and to tactical DDD (aggregates, value objects,
repositories, domain services, domain events). Then list the exact things I should be
able to explain out loud once I have built it. Stop there. I will build it and come back.
```

## Today's work

1. **Concept first on CI versus CD.**
   - **CI (continuous integration)**: every push triggers automated builds and tests. The pipeline is a quality gate. If it is red, the branch is not shippable.
   - **CD (continuous delivery)**: every green build produces a deployable artefact, and shipping is a click.
   - **CD (continuous deployment)**: every green build actually deploys to production. The click is automated.
   
   Know the distinction cold. Interviewers conflate them; you should not.

2. **Read the twelve-factor app.** All twelve. Not a skim.
   - The Twelve-Factor App: https://12factor.net
   - Focus especially on III (Config), IV (Backing services), V (Build, release, run), VI (Processes), VIII (Concurrency), and X (Dev/prod parity). These are the ones a payments app is judged on.

3. **Understand the pipeline as a quality gate that runs without you.** A senior engineer does not run tests locally to check work — the pipeline does. Local runs are a fast loop. The pipeline is the authoritative check because it runs on a clean environment every time.

4. **Reading:**
   - GitHub Actions docs: https://docs.github.com/actions
   - Full list in [resources.md → extension](../resources.md#extension).

## Cross-cutting reminders

- **Security via secrets**: config and credentials belong in the environment, never in git. This is twelve-factor III and the security cross-cutting concern in one. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. You have not written code yet.
