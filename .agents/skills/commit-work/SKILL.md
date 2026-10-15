---
name: commit-work
description: Use when committing completed work.
---

# Commit work

Create local commits that are easy to review.

## Rules

- Make local commits only for complete work in the current task. Pushing, branch changes, and history rewriting need a separate request.
- For PR work, group meaningful logic, UI, documentation, and CI/CD changes into separate commits, even when they serve one feature. Keep tests with the code they verify.
- Give each commit one clear purpose. Split further only when it helps review. Do not split by individual file or work order, or force a fixed commit count. A change confined to one area can be one commit.
- Order commits by dependency and keep the project working after each commit. Combine tightly connected changes when separating them would break an intermediate commit.
- Rely on current task context. Check status; inspect only unfamiliar or ambiguous changes, not the full diff by default.
- Commit only complete, scoped work. Exclude unrelated or sensitive content and co-author trailers. Preserve unclear existing changes; partially stage mixed files.

## Commit

For each group:

1. Stage related changes and review the staged diff.
2. Reuse valid verification; run only missing relevant checks.
3. Commit in the known repository style; inspect recent messages only if needed.

Check status, then report created commits and task changes left uncommitted.
