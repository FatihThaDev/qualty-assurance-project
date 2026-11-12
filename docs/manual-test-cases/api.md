# Manual Test Cases — API

> For the API cases you need an access token: log in as `testuser`, go to **Settings → Applications → Generate New Token**, and copy the token.

## TC-14: Access the API with an invalid token

- **Regression ID:** REG-14
- **Type:** Negative

| # | Action | Expected Result |
|---|---|---|
| 1 | Run `curl -s -o /dev/null -w "%{http_code}" -H "Authorization: token invalid-token" http://localhost:3000/api/v1/user` | The API responds with `401` (Unauthorized) |
| 2 | Run `curl -H "Authorization: token <TOKEN>" http://localhost:3000/api/v1/user` with the generated token | The API responds with `200` and the user's data |

**Result:** Pass, **Date:** 2026-11-12, **Bug ID:** -

## TC-15: List the user's repositories via API

- **Regression ID:** REG-15
- **Type:** Positive

| # | Action | Expected Result |
|---|---|---|
| 1 | Run `curl -H "Authorization: token <TOKEN>" http://localhost:3000/api/v1/users/testuser/repos` | The API responds with `200` and a JSON array containing `test-repo` |

**Result:** Pass, **Date:** 2026-11-12, **Bug ID:** -
