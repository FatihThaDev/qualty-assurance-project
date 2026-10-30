# Quality Assurance Project - Gitea (SUT)

## Overview

[Gitea](https://about.gitea.com/) is a lightweight, self-hostable Git forge that will serve as my **System Under Test (SUT)**. It provides repository hosting, issue tracking, pull requests, user management, and everything else you would expect from services like GitHub, but running locally.

**Local URL:** [http://localhost:3000](http://localhost:3000)  
**Default Port:** `3000` (configurable)  
**Type:** Self-hosted Git service (Go binary / Docker)  

## Prerequisites

Before getting started, make sure you have the following installed:

| Tool | Minimum Version | Notes |
|---|---|---|
| [Git](https://git-scm.com/) | 2.x+ | For cloning and version control |
| [Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/) | Latest stable | Recommended for a clean, reproducible setup |
| [Go](https://go.dev/) | 1.21+ | Only needed if building from source |
| [SQLite](https://www.sqlite.org/) / [Postgres](https://www.postgresql.org/) / [MySQL](https://www.mysql.com/) | As needed | Gitea supports multiple databases. SQLite works fine for local testing |

## Setup & Installation by Test Level

Testing strategy for this assignment covers different levels, each with its own setup considerations. Use whichever fits.

### 1. Unit Testing

Unit tests focus on isolated components and don't require a fully running Gitea instance. This is the lightest way to iterate.

**Environment/Data Config:**
- No external Gitea server required
- Use mocks/stubs for HTTP, DB, and Git operations
- Configuration can be in-memory or via test fixtures

**Setup:**
```bash
# Clone the repo
git clone https://github.com/go-gitea/gitea.git
cd gitea

# Install dependencies
go mod download

# Run unit tests
go test ./modules/... ./services/... -count=1
```

### 2. API/Integration Testing

For API-level tests, you will need a live Gitea instance with a predictable state (users, repos, tokens, etc.).

#### Option A: Docker Compose (Recommended)
This is the easiest way to spin up a fresh, isolated instance.

**Environment/Data Config:**
- Create a `.env` file for your local stack (or just use defaults)
- Use a fresh database for each test run to avoid state leakage
- Pre-seed test data via API calls or Gitea's admin setup

**Setup:**
```yaml
# docker-compose.yml (example)
version: "3"

services:
  gitea:
    image: gitea/gitea:latest
    container_name: gitea-sut
    environment:
      - USER_UID=1000
      - USER_GID=1000
      - GITEA__database__DB_TYPE=sqlite3
      - GITEA__database__PATH=/data/gitea/gitea.db
      - GITEA__server__DOMAIN=localhost
      - GITEA__server__HTTP_PORT=3000
      - GITEA__server__ROOT_URL=http://localhost:3000/
      - GITEA__security__INSTALL_LOCK=true  # lock after initial setup in automation
    restart: unless-stopped
    ports:
      - "3000:3000"
      - "222:22"
    volumes:
      - ./gitea-data:/data
```

```bash
# Start up
docker compose up -d

# Wait for it to be ready
curl http://localhost:3000/api/v1/version

# Stop when done
docker compose down -v  # -v clears volumes for a clean slate
```

#### Option B: Binary Installation
Great if you want to run against the exact build you're testing.

**Setup:**
1. Download the latest [Gitea binary](https://dl.gitea.com/gitea/) for your OS.
2. Create a working directory (e.g. `~/gitea`).
3. Copy `gitea` binary there and make it executable: `chmod +x gitea`.
4. Run it: `./gitea web` (on first run it'll guide you through the installer at `http://localhost:3000`).
5. Use SQLite for simplicity, or point to a local Postgres/MySQL instance.

**Notes for testing:**
- Disable registration or create a dedicated test admin account
- Generate API tokens for authenticated requests
- Consider using a fresh data directory between test runs

### 3. End-to-End (E2E) / UI Testing

E2E tests hit the full stack through the browser/API as a real user would. You will want a stable, reproducible instance here.

**Environment/Data Config:**
- **Base URL:** `http://localhost:3000` (set via your test config/env vars)
- **Test users:** Create at least an admin user and a regular user with known credentials
- **Seed data:** Repos, issues, teams/orgs, webhooks, etc. can be created via API before UI tests run
- **Git auth:** For SSH/HTTPS flows in tests, use local keys or disable SSH if not needed
- **Clean state:** Reset DB + data volume between suites to avoid issues

**Tips:**
- If using Docker, mount a known-good backup or run a seed script on startup
- Keep test data minimal where possible
- For browser automation, make sure the instance is fully up before kicking off tests (healthcheck `/api/v1/version`)

## Data Configuration Tips

- **Database**: SQLite is perfect for local QA. For parallel test runs or heavier loads, Postgres is worth it.
- **Secrets**: Never commit real credentials. Use environment variables or a local `.env` (gitignored).
- **Email**: Gitea can be configured for email, but for most QA flows it's not necessary. You can disable or use a local mailcatcher if needed.
- **External auth**: Keep OAuth/SSO disabled unless you're specifically testing it.
- **Storage**: Attachments, avatars, and similar data live in the `data/` directory. Wipe it between clean runs.

## Quick Health Check

Once your instance is up, verify it's good to go:

```bash
# Check version
curl -s http://localhost:3000/api/v1/version

# Check health/status
curl -s http://localhost:3000/api/healthz  # if enabled
```

## How to Contribute

Contributions are welcome! Here's a way to get involved:

1. **Find something to work on** - Check open issues, TODOs in tests, or propose improvements. Bug reports are always appreciated.
2. **Fork & branch** - Fork this repo (and/or the Gitea repo if contributing upstream fixes), then create a feature branch: `git checkout -b qa/your-change`.
3. **Set up your SUT** - Use the setup above that matches what you're testing.
4. **Write tests** - Follow existing patterns in the repo. Add clear descriptions, keep them deterministic, and always clean up.
5. **Test locally** - Run your tests against a fresh instance where possible. Document any special setup if needed.
6. **Open a PR** - Push your branch and open a pull request with a clear summary, what you tested, and how to reproduce/verify.
7. **Be nice** - Keep feedback constructive, share useful logs, and help others debug flaky tests.

### Guidelines
- **Reproducibility over speed**: Prefer a resettable setup (Docker volumes down/up) over reusing dirty state.
- **Document assumptions**: If your test depends on specific config/data, call it out in comments or README updates.
- **No hardcoded creds**: Use fixtures/env vars.
- **Small PRs**: Easier to review and debug.
---

**Note:** This repo is for QA against a locally installed Gitea instance. If you're looking to contribute to Gitea itself, go to [go-gitea/gitea](https://github.com/go-gitea/gitea).

## How to Contribute

1. **Fork & branch** - Fork this repo and create a branch: `git checkout -b your-branch-name`
2. **Set up your SUT** - Spin up a local Gitea instance using the setup above
3. **Write your tests** - Keep them simple, deterministic, and follow existing patterns
4. **Test locally** - Run against a fresh instance if you need a clean state
5. **Open a PR** - Push your branch and open a PR with a short description of what you added/fixed
