# Changelog
Semantic versioning. Public beta is planned as v0.1.0.

## 0.0.3
- Docker images for the API and the web app (Caddy serving the PWA and proxying /api).
- Production compose stack: Postgres, Redis, one-shot migrations, API, web, Cloudflare Tunnel. No published ports, internal-only backend network, hardened containers.
- Encrypted nightly backup script (age + SSH to your backup server) and a restore script.
- docs/DEPLOYMENT.md: Cloudflare, Brevo and backup setup.

## 0.0.2
- Auth: register, email verification (Brevo, console fallback in dev), login, rotating refresh tokens, logout.
- Ledger service with daily claim (300 coins, rolling 24h), wallet endpoints.
- Tests (Vitest, real Postgres) for the ledger rules, claim timing and concurrency, and the auth flow.

## 0.0.1
- Monorepo scaffold: Fastify API, React + Vite PWA shell, shared package.
- Migration 001: users, refresh/email tokens, append-only double-entry ledger.
- Dev infrastructure (Postgres 18, Redis) and CI.
