# Quality Assurance Project - Gitea (SUT)

## Overview

[Gitea](https://about.gitea.com/) is a lightweight, self-hostable Git forge that will serve as my **System Under Test (SUT)**. It provides repository hosting, issue tracking, pull requests, user management, and everything else you would expect from services like GitHub, but running locally.

**Local URL:** [http://localhost:3000](http://localhost:3000)  
**Default Port:** `3000` (configurable)  
**Type:** Self-hosted Git service (Docker / prebuilt binary)

## Prerequisites

Before getting started, make sure you have the following installed:

| Tool | Minimum Version | Notes |
|---|---|---|
| [Git](https://git-scm.com/) | 2.x+ | For cloning and version control |
| [Docker](https://www.docker.com/) | Latest stable | Used to run Gitea |
| `curl` | Any | For the API test cases and health check |

## Setup & Installation

The SUT runs in Docker with a single command. No Gitea source code, Go toolchain, or external database is needed.

### Option A: Docker (Recommended)

**1. Start Gitea:**

```bash
docker run -d --name gitea-sut -p 3000:3000 -v gitea-data:/data gitea/gitea:latest
```

What each part does:

| Flag | Meaning |
|---|---|
| `-d` | Run the container in the background |
| `--name gitea-sut` | Name the container `gitea-sut` (used by the stop/reset commands below) |
| `-p 3000:3000` | Expose Gitea on `http://localhost:3000` |
| `-v gitea-data:/data` | Keep Gitea's data (database, repos) in a named volume so it survives restarts |

**2. Complete the initial setup (first run only):**

Open [http://localhost:3000](http://localhost:3000) in a browser. The first-run installer is shown:

- **Database Type:** SQLite3 (default) - no external database needed
- **Base URL / Server Settings:** leave the defaults
- **Administrator Account:** create one, e.g. username `gitea-admin` (do **not** use `testuser` - the test cases register that user themselves)
- Click **Install**

**3. Verify the instance is up:**

```bash
curl -s http://localhost:3000/api/v1/version
```

You should get a JSON response with the Gitea version.

**4. Run the tests:**

The test cases in `docs/manual-test-cases/` create their own test data as they run (`testuser`, `test-repo`, an issue, and a pull request), so no manual seeding is needed. For the two API test cases, log in as `testuser` and generate a token in **Settings → Applications**.

### Reset for a clean slate

Between test runs you can wipe everything and start fresh:

```bash
docker stop gitea-sut && docker rm gitea-sut && docker volume rm gitea-data
```

Then repeat the setup above.

### Option B: Prebuilt Binary

If you don't want to use Docker:

1. Download the latest [Gitea binary](https://dl.gitea.com/gitea/) for your OS.
2. Create a working directory (e.g. `~/gitea`).
3. Copy the `gitea` binary there and make it executable: `chmod +x gitea`.
4. Run it: `./gitea web` (on first run it'll guide you through the installer at `http://localhost:3000`).
5. Use SQLite for simplicity.

## Test Documentation

- Test strategy: `docs/test-strategy.md`
- Regression suite: `docs/regression-suite.md`
- Manual test cases: `docs/manual-test-cases/` (results are recorded in each file)
- Bug reports: `bugs/`

## Quick Health Check

Once your instance is up, verify it's good to go:

```bash
# Check version
curl -s http://localhost:3000/api/v1/version

# Check health/status
curl -s http://localhost:3000/api/healthz  # if enabled
```

## How to Contribute

1. **Fork & branch** - Fork this repo and create a branch: `git checkout -b your-branch-name`
2. **Set up your SUT** - Spin up a local Gitea instance using the setup above
3. **Write your tests** - Keep them simple, deterministic, and follow existing patterns
4. **Test locally** - Run against a fresh instance if you need a clean state
5. **Open a PR** - Push your branch and open a PR with a short description of what you added/fixed
