# Manual Test Cases — Repositories

## TC-05: Create a new repository

- **Regression ID:** REG-05
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Log in as `testuser` | The user is logged in |
| 2 | Click the **+** (top right) and select **New Repository** | The create repository form is displayed |
| 3 | Enter the name `test-repo`, check **Initialize Repository** (adds a README and a default branch), and click **Create Repository** | The new repository page is displayed and shows `testuser/test-repo` |

**Result:** Pass, **Date:** 2026-11-11, **Bug ID:** -

## TC-06: View repository page and clone URL

- **Regression ID:** REG-06
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `http://localhost:3000/testuser/test-repo` | The repository page is displayed with its tabs (Code, Issues, Pull Requests, ...) |
| 2 | Click the green **Code** button and copy the HTTP URL | The clone URL `http://localhost:3000/testuser/test-repo.git` is visible and copyable |

**Result:** Pass, **Date:** 2026-11-11, **Bug ID:** -

## TC-07: Create a repository with a duplicate name

- **Regression ID:** REG-07
- **Type:** Negative

| # | Action | Expected Result |
|---|---|---|
| 1 | Click the **+** (top right) and select **New Repository** | The create repository form is displayed |
| 2 | Enter the name `test-repo` (already exists) and click **Create Repository** | An error message is shown and no second repository is created |

**Result:** Pass, **Date:** 2026-11-11, **Bug ID:** -
