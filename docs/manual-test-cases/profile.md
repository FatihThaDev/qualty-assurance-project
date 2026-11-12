# Manual Test Cases — Profile

## TC-13: View and edit the user profile

- **Regression ID:** REG-13
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Click the profile avatar (top right) → **Profile** | The profile page is displayed and shows the username `testuser` |
| 2 | Click **Settings** => **Profile** | The profile settings form is displayed |
| 3 | Change **Full Name** to `Test User` and click **Update Profile** | A success message is shown |
| 4 | Open the profile page again | The full name `Test User` is displayed |

**Result:** Pass, **Date:** 2026-11-12, **Bug ID:** -
