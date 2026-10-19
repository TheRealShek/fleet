---
name: pr-file
description: Use when opening a requested pull request without a repository template, or when the requested pull request includes UI changes.
---

# PR Filing

## Prepare

1. Read the repository instructions and contribution guide.
2. Identify the actual base branch and inspect the complete diff for unintended changes or sensitive data.
3. Check for an existing PR for the branch. Update or report it instead of creating a duplicate.
4. Read each issue before linking it and confirm how the change relates to it.
5. Run the relevant tests and record the results.
6. Use `code-review` against the actual base branch if the complete current diff has not already been reviewed. Reuse a review that still covers the final diff.
7. Address valid findings and rerun relevant tests before opening the PR. If a fix is not authorized, stop and report the finding instead.

Follow `commit-work` for local commits and the global Git rules for publishing. Keep code changes within the authorized scope.

## UI screenshots

When the user requests a PR with UI changes, include labeled before and after screenshots in its description, even when using a PR template. Capture the actual base and changed UI with the same viewport and state, without changing the user's focus or overwriting their work. Use image URLs reviewers can access and verify they render. If capture or upload fails, report the blocker.

For Hyprland windows, use `grim -T <identifier> <output.png>`. Get the identifier from the Wayland foreign-toplevel list, not the `hyprctl` window address. This also works on inactive workspaces.

## Write

Use the repository's PR template when present. Otherwise, use the title and description format below.

Write the title as `<type>(<scope>): <action> - #<issue>`, for example `feat(analytics): report connected client platforms - #8481`. The type says what kind of change it is, the scope names the main area touched, and the action says what the PR does. Include only a verified issue number; omit the suffix when there is no issue.

Cover these points in order. Headings and bold labels are optional:

- Explain the problem and why it matters in one short paragraph.
- Describe the resulting behavior in a short paragraph or at most five bullets.
- Summarize validation and results in at most three bullets. If nothing ran, say `Not run` and why.
- Add a verified issue reference when applicable.
- Include material limitations or tradeoffs only when they affect review or use.

Use `Fixes #123` only when the PR fully resolves the issue and targets the default branch. Use `Related to #123` for similar, overlapping, partial, or non-default-branch work. Never guess an issue number.

## Description limits

- Keep the description under 200 words, excluding screenshot markup and required template boilerplate. Treat this as a ceiling, not a target.
- Summarize related changes together. Omit file-by-file inventories, repeated checks, and debugging history.
- State what validation passed, failed, or was skipped. Keep details that affect confidence in the change.
- Put breaking changes first. Exceed the word limit only for necessary breaking-change or migration instructions, or when the user requests more detail.

## Open and Verify

1. Open a ready PR when the work is complete. Open a draft only when the user requests one.
2. Verify the title, base, head, description, URL, and issue references. When using `Fixes`, confirm GitHub lists the closing issue.
3. Report the PR link and any failed checks or blockers.
