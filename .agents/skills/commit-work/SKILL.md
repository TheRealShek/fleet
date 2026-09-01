---
name: commit-work
description: Create local Git commits when the user asks to commit completed work.
---

# Commit Work

Create local commits by cohesive purpose.

## Rules

- A commit request permits local commits for the current task only. Pushing, branch changes, and history rewriting need a separate request.
- Split distinct, independently useful or revertible changes. Keep code, tests, configuration, and documentation for the same behavior together. Do not split by file or work order.
- Rely on current task context. Check status; inspect only unfamiliar or ambiguous changes, not the full diff by default.
- Commit only complete, scoped work. Exclude unrelated or sensitive content and co-author trailers. Preserve unclear existing changes; partially stage mixed files.

## Commit

For each group:

1. Stage related changes and review the staged diff.
2. Reuse valid verification; run only missing relevant checks.
3. Commit in the known repository style; inspect recent messages only if needed.

Check status, then report created commits and task changes left uncommitted.
