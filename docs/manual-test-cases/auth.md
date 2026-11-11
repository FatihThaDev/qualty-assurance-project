# Manual Test Cases — Authentication

## TC-01: Register a new account

- **Regression ID:** REG-01
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `http://localhost:3000/user/sign_up` | The registration page is displayed |
| 2 | Enter username `testuser`, a valid email address and a password | All fields accept the input |
| 3 | Click **Sign Up** | Registration succeeds, the user is logged in and redirected to the dashboard |

**Result:** Pass,  **Date:** 2026-11-11,  **Bug ID:** —

## TC-02: Log in with valid credentials

- **Regression ID:** REG-02
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `http://localhost:3000/user/login` | The login page is displayed |
| 2 | Enter username `testuser` and the correct password | Both fields accept the input |
| 3 | Click **Sign In** | The user is logged in and redirected to the dashboard |

**Result:** Pass, **Date:** 2026-11-11, **Bug ID:** -

## TC-03: Log out

- **Regression ID:** REG-03
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Log in as `testuser` | The user is logged in |
| 2 | Click the profile avatar (top right) and then **Sign Out** | The user is signed out, redirected to the home page and profile avatar is replaced by "Register" and "Sign In" buttons |

**Result:** Pass, **Date:** 2026-11-11,  **Bug ID:** -

## TC-04: Log in with an invalid password

- **Regression ID:** REG-04
- **Type:** Negative

| # | Action | Expected Result |
|---|---|---|
| 1 | Open `http://localhost:3000/user/login` | The login page is displayed |
| 2 | Enter username `testuser` and a wrong password | Both fields accept the input |
| 3 | Click **Sign In** | An error message is shown and the user is **not** logged in |

**Result:** Pass, **Date:** 2026-11-11, **Bug ID:** -
