---
name: commit-work
description: Use only when the user explicitly invokes `$commit-work`.
---

# Commit Work

Create the fewest clean local commits that clearly represent completed work.

## Start

1. Read the repository instructions.
2. Inspect the working tree and recent commit messages.
3. Note changes that existed before the task. Do not commit or overwrite them.

Treat explicit use of this skill as permission to create local commits for the current task. It does not give permission to push, create or switch branches, rebase, amend commits, or change unrelated work.

## Choose Commit Boundaries

Prefer one cohesive commit for the current task. Split only when the task contains multiple changes that are independently complete and useful. Each split should:

- Be understandable and testable on its own.
- Be reasonable to review or revert without the other commits.
- Represent a distinct purpose, not merely the order in which edits were made.

When uncertain, keep related changes together. Do not treat each requirement, file, or chronological milestone as an automatic commit boundary. Keep implementation, tests, and documentation for the same behavior in one commit. Follow-up corrections needed to complete that behavior belong there too.

Wait until a unit is complete and stable enough to review before committing it.

## Commit Completed Work

After choosing the commit boundaries, process each completed unit:

1. Review its diff and confirm it belongs to the current task.
2. Run the narrowest useful checks for that unit.
3. Stage only the files or parts that belong together.
4. Commit the unit with a short, simple message that follows the repository's style.
5. Confirm the commit succeeded, then continue the task.

Do not create a commit for every small edit. Do not commit broken, unfinished, unrelated, generated, or sensitive content. If a file has both task changes and older work and cannot be staged safely, leave it uncommitted and explain why.

## Handle Work Already in Progress

If the skill is invoked after changes already exist, review the full task diff and create the fewest cohesive commits needed for the user's current work. Split only according to the boundary rules above. Preserve existing changes whose ownership or purpose is unclear.

## Finish

Before reporting completion:

1. Inspect the working tree again.
2. Commit any final completed work using the boundary rules above.
3. Report the commits created and any task changes left uncommitted.

Never add co-author trailers. Never push unless the user separately asks.
