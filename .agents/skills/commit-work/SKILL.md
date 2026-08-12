---
name: commit-work
description: Use only when the user explicitly invokes `$commit-work`.
---

# Commit Work

Create clean local commits as meaningful parts of the task are completed.

## Start

1. Read the repository instructions.
2. Inspect the working tree and recent commit messages.
3. Note changes that existed before the task. Do not commit or overwrite them.

Treat explicit use of this skill as permission to create local commits for the current task. It does not give permission to push, create or switch branches, rebase, amend commits, or change unrelated work.

## Commit Throughout the Task

After completing a meaningful functional unit:

1. Review its diff and confirm it belongs to the current task.
2. Run the narrowest useful checks for that unit.
3. Stage only the files or parts that belong together.
4. Commit the unit with a short, simple message that follows the repository's style.
5. Confirm the commit succeeded, then continue the task.

A functional unit should be one clear, useful part of the task. Group changes by purpose, not by file type. Include related tests and documentation in the same commit as the behavior they cover.

Do not create a commit for every small edit. Do not commit broken, unfinished, unrelated, generated, or sensitive content. If a file has both task changes and older work and cannot be staged safely, leave it uncommitted and explain why.

## Handle Work Already in Progress

If the skill is invoked after changes already exist, review the full task diff and divide only the user's current work into logical commits. Preserve existing changes whose ownership or purpose is unclear.

## Finish

Before reporting completion:

1. Inspect the working tree again.
2. Commit any final completed functional unit.
3. Report the commits created and any task changes left uncommitted.

Never add co-author trailers. Never push unless the user separately asks.
