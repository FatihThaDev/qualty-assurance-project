# Test Strategy

## Functional Scope

**In Scope:**
- User authentication (login/logout, registration)
- Repository management (create, view, clone)
- Issues (create, view, comment)
- Pull Requests (create, view)
- Basic user profile settings
- Accessing repos via web UI and API

**Out of Scope:**
- Advanced admin settings
- LFS, Webhooks, and integrations
- Email functionality
- External auth (OAuth/SSO)

## Test Levels and Tools

| Test Level | Tool | Purpose |
|---|---|---|
| Manual | Markdown test cases | Core functionality checks |
| API | Postman/REST calls | Test Gitea REST API endpoints |
| E2E/UI | Playwright (TypeScript) | Test user flows through browser |
| Unit | Previous project's repo (linked in README) | Isolated component tests |

## Test Data and Environment

- **Environment:** Locally installed Gitea at [http://localhost:3000](http://localhost:3000)
- **Database:** SQLite (default for local testing)
- **Test Data:** Create dedicated test users and test repos. Use API tokens for API tests.
- **Setup:** Follow instructions in README to spin up Gitea via Docker or binary.

## Entry/Exit Criteria

**Entry Criteria:**
- Gitea instance is up and accessible at `http://localhost:3000`
- Test users/repos can be created
- Test environment matches setup in README

**Exit Criteria:**
- All planned regression tests executed
- Critical bugs reported in `/bugs/` if found
- Test results documented

## Risks

| Risk | Mitigation |
|---|---|
| Dirty state between tests | Reset DB between test runs |
| Instance not ready before tests | Check `/api/v1/version` before running tests |
| Unreliable UI tests | Keep tests simple and use fresh test data |
| Port conflicts | Use default port or configure one that isn't used |
