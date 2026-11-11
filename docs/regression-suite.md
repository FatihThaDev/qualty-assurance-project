# Regression Suite

15 important regression test cases to cover core functionality of Gitea. Four of them are negative test cases. The full step-by-step versions live in `docs/manual-test-cases/`.

| ID | Test Case | Area | Type | Justification |
|---|---|---|---|---|
| REG-01 | User can register a new account | Auth | Positive | Core entry point. Broken registration blocks all users. |
| REG-02 | User can log in with valid credentials | Auth | Positive | Essential for accessing protected features. |
| REG-03 | User cannot log in with an invalid password | Auth | Negative | Invalid credentials must be rejected for security. |
| REG-04 | User can log out | Auth | Positive | Must properly end session for security. |
| REG-05 | Create a new repository | Repo | Positive | Main functionality of Gitea as a Git forge. |
| REG-06 | View repository page and clone URL | Repo | Positive | Users need to access repos and clone them. |
| REG-07 | Cannot create a repository with a duplicate name | Repo | Negative | Duplicate names must be rejected, not silently overwrite. |
| REG-08 | Create a new issue | Issues | Positive | Core collaboration feature. |
| REG-09 | View an issue and add a comment | Issues | Positive | Must be able to read issues and discuss them. |
| REG-10 | Cannot create an issue with an empty title | Issues | Negative | Invalid input must be rejected with a clear error. |
| REG-11 | Create a pull request | PRs | Positive | Core code review workflow. |
| REG-12 | View pull request details | PRs | Positive | Must be able to review changes. |
| REG-13 | View and edit user profile | Profile | Positive | Users need to access and update their info. |
| REG-14 | API rejects an invalid token | API | Negative | The API must not leak data with bad credentials. |
| REG-15 | List user's repositories via API | API | Positive | Core API functionality for integrations. |
