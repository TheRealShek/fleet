---
name: pr-file
description: File a pull request when intent is clear and the repository provides no PR template.
---

# PR Filing

## Prepare

1. Read the repository instructions and contribution guide.
2. Identify the actual base branch and inspect the complete diff for unintended changes or sensitive data.
3. Check for an existing PR for the branch. Update or report it instead of creating a duplicate.
4. Read each issue before linking it and confirm how the change relates to it.
5. Run the relevant tests and record the results.
6. Use `code-review` against the actual base branch as the final check immediately before opening the PR.
7. Address valid findings and rerun relevant tests before opening the PR. If a fix is not authorized, stop and report the finding instead.

Do not commit, push, change branches, or alter code unless the user authorized it.

## Write

Write the title as `<type>(<scope>): <action> - #<issue>`, for example `feat(analytics): report connected client platforms - #8481`. The type says what kind of change it is, the scope names the main area touched, and the action says what the PR does. Include only a verified issue number; omit the suffix when there is no issue.

Write the description in this order:

- **Problem:** Explain the issue and why it matters in plain English.
- **Solution:** Explain how the change solves it and what now behaves differently.
- **Tests:** List the tests run and their results. If none ran, say `Not run` and why.
- **Issue:** Add a verified issue reference when applicable.
- **Note:** End with the important implementation details a reviewer needs, such as key design choices or tradeoffs.

Use `Fixes #123` only when the PR fully resolves the issue and targets the default branch. Use `Related to #123` for similar, overlapping, partial, or non-default-branch work. Never guess an issue number.

Keep the description brief. Put breaking changes first. Do not narrate files, functions, commits, or implementation steps unless they help the reviewer understand the solution or its tradeoffs.

## Open and Verify

1. Open a ready PR when the work is complete. Use a draft only when it is incomplete or requested.
2. Verify the title, base, head, description, URL, and issue references. When using `Fixes`, confirm GitHub lists the closing issue.
3. Report the PR link and any failed checks or blockers.
