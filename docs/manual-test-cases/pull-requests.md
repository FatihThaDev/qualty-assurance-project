# Manual Test Cases - Pull Requests

## TC-11: Create a pull request

- **Regression ID:** REG-11
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `test-repo`, click the branch selector, click the small branch icon in the main branch row and type `feature` in the dialog, then press `confirm` | The new branch `feature` is created and checked out |
| 2 | Edit a file (e.g. `README.md`) via the web editor and commit the change on `feature` | The commit is saved |
| 3 | Open the **Pull Requests** tab → **New Pull Request** | The PR form is displayed with base branch = default branch and compare branch = `feature` |
| 4 | Enter a title, set `feature` branch to be compared with main and click **New Pull Request**, then click **Create Pull Request** | The new PR page is displayed with the title and the change |

**Result:** Pass, **Date:** 2026-11-12, **Bug ID:** -

## TC-12: View pull request details

- **Regression ID:** REG-12
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `test-repo` → **Pull Requests** | The created PR is listed |
| 2 | Click the PR | Title, description and author are displayed |
| 3 | Open the **Files changed** tab | The diff of the committed change is displayed |

**Result:** Pass, **Date:** 2026-11-12, **Bug ID:** -
