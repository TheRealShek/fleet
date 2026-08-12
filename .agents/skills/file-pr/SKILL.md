---
name: file-pr
description: Use when the user explicitly asks to file, open, or create a PR and nothing else
---

# File PR

## Prepare

1. Read the repository instructions and contribution guide.
2. Inspect the current branch, working tree, upstream state, and remotes. Do not overwrite unrelated work.
3. Check whether a pull request already exists for the branch. Update or report the existing PR instead of creating a duplicate.
4. Determine the actual base branch and review the complete branch diff against it. Do not assume `main` when the repository indicates otherwise.
5. Confirm the branch contains the intended change and no unrelated or sensitive content.
6. Review recent merged PRs and Git history for repository-specific title and description conventions.

Do not create commits, push, change branches, or alter code unless the user has authorized that action. If the branch is not ready or available remotely, explain what is needed.

## Write

- Use a concise, human-readable, imperative title that communicates why the change matters or what improves. Do not merely name the component or implementation.
- Put breaking changes at the top of the description.
- Start from the problem in the user's terms, then describe the outcome. Prefer user-visible behavior over a list of files, functions, or implementation details.
- Keep the description plain, short, and free of AI boilerplate or emoji.
- Use this structure unless the repository requires another format:

  - **Intent:** the problem and why it needed to be solved
  - **Change:** what is now better or behaves differently
  - **Verification:** the checks actually run and their results

## Open and Verify

1. Open a ready PR when the work is complete so normal review checks run. Use a draft only when the work is incomplete or the user asks for one.
2. Verify the resulting PR title, base, head, description, and URL.
3. Report the PR link and any unresolved checks, risks, or blockers.
