# Week 12, Day 4: Deploy to a real host with secrets managed properly

## Start-of-day prompt

None.

## Today's work

1. **Pick a host.** Options in order of "one-command deploy" to "you own everything":
   - **Fly.io** — Dockerfile-native, global by default, `fly deploy` from the CLI. Good for a small app.
   - **Railway** — Git-driven, provisioned Postgres and Redis add-ons, less to configure.
   - **A VPS** (DigitalOcean, Hetzner, Linode) — you own the OS, the reverse proxy, the TLS certs. More work, more understanding.
   
   Pick one. Defend it. For this project the goal is a live URL and a real deploy story, not infrastructure bragging rights.

2. **Configure environment variables at the host, never in git.** Every credential — `APP_KEY`, `DB_PASSWORD`, `STRIPE_SECRET`, `PAYSTACK_SECRET_KEY`, `REDIS_PASSWORD` — is set through the host's secrets interface (Fly secrets, Railway variables, or `/etc/environment` and systemd `EnvironmentFile` on a VPS). A leaked gateway key on a payments app is a same-day incident; treat the secrets store as a security boundary, not a config convenience. See [craft-reference.md → security](../craft-reference.md#security).

3. **Never commit `.env` to git.** Confirm `.env` is in `.gitignore`. `.env.example` with keys but no values is what belongs in the repo.

4. **Provision Postgres and Redis on the host side.** Fly Postgres, Railway Postgres add-on, or a managed Postgres from your VPS provider. Do not run production Postgres in the app container.

5. **First deploy.** Push, watch the deploy log, hit the live URL, confirm `/up` or a healthcheck endpoint returns 200. Run one manual migration against the deployed database if the pipeline is not yet wired to run them (that comes tomorrow).

6. **Verify secrets are not leaking into logs.** Search the deploy log for anything that looks like a token. If it is there, rotate it and fix the log source.

## Cross-cutting reminders

- **Security via secrets**: secrets live in the host's secrets store, never in git, never in the image, never in logs. See [craft-reference.md → security](../craft-reference.md#security).

## End-of-day prompt

None. Zero-downtime and safe migrations tomorrow.
