# Regression Suite

15 important regression test cases to cover core functionality of Gitea.

| ID | Test Case | Area | Justification |
|---|---|---|---|
| REG-01 | User can register a new account | Auth | Core entry point. Broken registration blocks all users. |
| REG-02 | User can log in with valid credentials | Auth | Essential for accessing protected features. |
| REG-03 | User can log out | Auth | Must properly end session for security. |
| REG-04 | Create a new repository | Repo | Main functionality of Gitea as a Git forge. |
| REG-05 | View repository page | Repo | Users need to access and read repos. |
| REG-06 | Clone repository URL is visible | Repo | Needed for Git operations. |
| REG-07 | Create a new issue | Issues | Core collaboration feature. |
| REG-08 | View existing issue | Issues | Must be able to read issue details. |
| REG-09 | Comment on an issue | Issues | Key for discussion/workflow. |
| REG-10 | Create a pull request | PRs | Core code review workflow. |
| REG-11 | View pull request details | PRs | Must be able to review changes. |
| REG-12 | View user profile | Profile | Basic user info must be accessible. |
| REG-13 | Edit user profile settings | Profile | Users need to update their info. |
| REG-14 | Access repository via API (authenticated) | API | API is commonly used, so it must still work. |
| REG-15 | List user's repositories via API | API | Core API functionality for integrations. |
