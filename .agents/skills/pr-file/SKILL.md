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

Local commits follow the global `commit-work` rule. Do not push, change branches, or alter code unless the user authorized it.

## UI screenshots

When the user requests a PR that changes the UI, include before and after screenshots in its description. Follow this workflow even when the repository has a PR template. Keep the template's structure and add the images in its screenshots section or an appropriate new section.

1. Capture the affected UI on the actual PR base and on the proposed changes. Use separate checkouts or worktrees when needed. Never revert or overwrite the user's work to obtain the before image.
2. Use the same viewport, theme, data, and interaction state for both images. Capture each materially different changed view or state. Use safe test data and inspect the images for secrets or private information before publishing.
3. For web UI, use the available browser capture tools. For desktop UI, capture the application window directly when supported. Do not change the user's focus or active workspace. On Hyprland, `grim -T <identifier> <output.png>` can capture a window on an inactive workspace. Obtain the identifier from the Wayland foreign-toplevel list; it is not the address returned by `hyprctl`. A screen-region capture with `grim -g` only captures visible screen content.
4. Inspect both images to confirm they show the intended states and make the change clear. Label them `Before` and `After`, with a short caption when needed.
5. Attach the images through the PR host's supported upload flow, or use a repository-approved image location that reviewers can access. Embed their URLs in the PR description. Local paths and temporary files do not render for reviewers. Do not commit screenshots solely to host them unless the repository calls for it.
6. If capture or upload is unavailable, report the specific blocker and retain any captured files. Do not substitute generated images or claim the comparison is complete. Continue authorized PR work and state the missing screenshots in the description and final report.

## Write

Use the repository's PR template when present. Otherwise, use the title and description format below. Include the UI screenshots required above in either format.

Write the title as `<type>(<scope>): <action> - #<issue>`, for example `feat(analytics): report connected client platforms - #8481`. The type says what kind of change it is, the scope names the main area touched, and the action says what the PR does. Include only a verified issue number; omit the suffix when there is no issue.

Write the description in this order:

- **Problem:** Explain the issue and why it matters in plain English.
- **Solution:** Explain how the change solves it and what now behaves differently.
- **Screenshots:** For UI changes, embed the labeled before and after images.
- **Tests:** List the tests run and their results. If none ran, say `Not run` and why.
- **Issue:** Add a verified issue reference when applicable.
- **Note:** End with the important implementation details a reviewer needs, such as key design choices or tradeoffs.

Use `Fixes #123` only when the PR fully resolves the issue and targets the default branch. Use `Related to #123` for similar, overlapping, partial, or non-default-branch work. Never guess an issue number.

Keep the description brief. Put breaking changes first. Do not narrate files, functions, commits, or implementation steps unless they help the reviewer understand the solution or its tradeoffs.

## Open and Verify

1. Open a ready PR when the work is complete. Open a draft only when the user requests one.
2. Verify the title, base, head, description, URL, and issue references. For UI changes, verify both screenshots render in the PR. When using `Fixes`, confirm GitHub lists the closing issue.
3. Report the PR link and any failed checks or blockers.
