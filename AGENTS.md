# Fleet

This repository is my source of truth for reusable AI-agent configuration. I use it to keep my working agreements, shared skills, and tool-specific adapters consistent across agents.

## How I organize it

- `instructions/global.md` contains my global instructions. Keep guidance specific to Fleet in this root `AGENTS.md`.
- `.agents/skills/` contains the canonical copies of my shared skills. Tool-specific skill directories should symlink to them instead of duplicating them.
- `.claude/skills/` is the repository-local Claude compatibility layer. Its symlinks only make skills available when Claude discovers this repository; they do not install skills globally.
- For a shared skill that should work from every repository, symlink its canonical directory into both `~/.agents/skills/` for Codex and `~/.claude/skills/` for Claude. Verify both links resolve to the canonical copy in this repository.
- Preserve working symlinks and keep their targets portable within this repository whenever possible.

## How to write skills

- Make every shared skill work with both Claude and Codex.
- Keep each skill description to one line that only says when to use the skill. The description is always sent to the model, so do not explain the skill there.
- Write skill instructions in simple language.

## What to change

- Change `instructions/global.md` when I ask to update my working preferences across agents.
- Create or update shared skills only in `.agents/skills/`.
- When adding a shared skill intended for global use, create or verify its user-level Codex and Claude symlinks. A symlink inside this repository does not expose the skill to sibling repositories.
- Change this root `AGENTS.md` only for guidance about maintaining Fleet itself.

## What never to change

- Never edit skill content through `.claude/`; it is only a compatibility layer of symlinks to `.agents/skills/`.
- Never replace a shared-skill symlink with a copied directory or maintain separate tool-specific copies.
- Never move canonical files or change external symlink targets unless I explicitly ask to change the repository structure.
