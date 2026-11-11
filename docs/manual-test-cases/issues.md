# Manual Test Cases - Issues

## TC-08: Create a new issue

- **Regression ID:** REG-08
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `test-repo` → **Issues** tab → **New Issue** | The new issue form is displayed |
| 2 | Enter the title `Test issue` and a short description, then click **Create Issue** | The new issue page is displayed with the title and an issue number (e.g. `#1`) |

**Result:** Not executed, **Date:** -, **Bug ID:** -

## TC-09: View an issue and add a comment

- **Regression ID:** REG-09
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `test-repo` → **Issues** | The list shows the existing issue `Test issue` |
| 2 | Click the issue | Title, description and details are displayed |
| 3 | Write a comment in the comment box and click **Comment** | The comment appears in the issue timeline |

**Result:** Not executed, **Date:** -, **Bug ID:** -

## TC-10: Create an issue with an empty title

- **Regression ID:** REG-10
- **Type:** Negative

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `test-repo` → **Issues** → **New Issue** | The new issue form is displayed |
| 2 | Leave the title empty, write a description and click **Create Issue** | An error message is shown and no issue is created |

**Result:** Not executed, **Date:** -, **Bug ID:** -
