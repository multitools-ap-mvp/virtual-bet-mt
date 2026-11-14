# V0.2.0 Changes
Auth and the ledger with daily claim are written and in apex-betting-platform-v0.0.2-dev. I haven't run any of it. The tests exist, but nobody has executed them or the typecheck yet.

**What's in it**

Auth:
Register sends a Brevo verification email (printed to the API console if no key is set).
Verify, login, rotating refresh tokens and logout all work.
Passwords use argon2id and the refresh token lives in an httpOnly cookie.
If an already-used refresh token is presented again, all of that user's sessions end.

Wallet: GET /api/wallet and POST /api/wallet/claim pay 300 coins once per rolling 24h. A row lock on the user means double taps pay once.

Tests (Vitest, real Postgres):
claim timing and 5 simultaneous claims;
unbalanced ledger transactions are rejected, both in the app and in the database;
ledger rows can't be edited or deleted;
the full register → verify → login → refresh → claim flow.

One change: argon2 and jose directly instead of Passport.js. Under Fastify, Passport adds a dependency without helping a password + JWT flow. 

To run it, create the test database first. The README has the three commands, starting with docker compose exec postgres createdb -U apex apex_test.
Package versions are still ranges from my memory, so check the first install and fix any version mismatches. If the tests or typecheck fail, paste the output and I'll fix it.

## V0.3.0-dev

v0.0.3 is packaged as a complete release zip. I haven't run any of it, including the Docker builds, the compose file and the shell scripts, so the first run on your server is the real test. I can't create the git tag from here, so run git tag v0.0.3 yourself after unpacking.

**What's new**

Docker images: the API image runs as a non-root user. The web image is Caddy serving the built PWA and proxying /api to the API, with the live-update (SSE) path unbuffered.

Production stack (docker-compose.prod.yml): Postgres, Redis, one-shot migrations, API, web, and the Cloudflare Tunnel. No ports are published, and Postgres and Redis sit on a network with no internet access. Containers run with all Linux capabilities dropped.

Backups: a nightly script encrypts each dump with age and uploads it to your backup server over SSH, keeping 14 days. The server only holds the public key, and the private key stays with you. There's also a restore script that refuses to touch a non-empty database.

DEPLOYMENT.md: step-by-step Cloudflare, Brevo and backup setup.
Versioning: all packages are bumped to 0.0.3. The changelog also covers 0.0.2 (auth and ledger). The public beta stays reserved for v0.1.0.
Before the first deploy
Copy all your existing DNS records into Cloudflare before switching nameservers, because your other subdomains depend on them.
In the Cloudflare tunnel, point betting.apexmultitools.se at http://web:8080.

Verify your sender domain in Brevo and add its DNS records as DNS-only.
Pin the cloudflared image version once it works.
Run a restore drill on a spare machine before launch.

Next is Phase 2, the betting engine: events, matches and teams, then markets, bets, locking, settlement and voiding, with tests for the pool math and edge cases. 

---

### Created By Apex Multi Tools 

**Gateway @ https://apexmultitools.se/**

**Contact @ info@apexmultitools.se**


---

