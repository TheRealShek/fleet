# Fleet

This repository is my source of truth for reusable AI-agent configuration. I use it to keep my working agreements, shared skills, and tool-specific adapters consistent across agents.

## How I organize it

- `instructions/global.md` contains my global instructions. Keep guidance specific to Fleet in this root `AGENTS.md`.
- `.agents/skills/` contains the canonical copies of my shared skills. Tool-specific skill directories should symlink to them instead of duplicating them.
- For a shared skill that should work from every repository, symlink its canonical directory into `~/.agents/skills/` for Codex, `~/.claude/skills/` for Claude, and `~/.gemini/config/skills/` for Antigravity. Verify all three links resolve to the canonical copy in this repository.
- Preserve working symlinks and keep their targets portable within this repository whenever possible.

## Global instruction setup

- Keep `~/.codex/AGENTS.md` for Codex and `~/.claude/CLAUDE.md` for Claude symlinked to this repository's `instructions/global.md`.
- For Antigravity and Gemini CLI, global instructions are discovered under `~/.gemini/config/`. Keep `~/.gemini/config/AGENTS.md` (and `~/.gemini/config/GEMINI.md`, `~/.gemini/antigravity-cli/AGENTS.md`) symlinked to `instructions/global.md`. For T3 Code's Antigravity provider, also link under `~/.t3/userdata/providers/antigravity/*/config/AGENTS.md`.
- Create these links on the machine and under the user account running the agent. T3 Code uses its selected environment's provider configuration; opening Fleet in T3 Code does not install global instructions for other projects.
- Verify that each link resolves to the canonical file and its contents are readable. Preserve existing files or different link targets; inspect them before changing them.
- Keep the direct skill-path fallback in `instructions/global.md` available to every provider. Global instruction loading must not depend on skill discovery.
- After changing instruction setup, verify loading in a fresh provider conversation from a project outside Fleet.

## Global skill setup

- Keep the global skill directories as real directories and link each skill folder individually, using its canonical directory name. Preserve unrelated skills and existing working links.
- Install these links under the user account on the machine running the T3 Code provider. Antigravity does not use `~/.agents/skills/` for global skill discovery; its shared global location is `~/.gemini/config/skills/`.
- When renaming a skill, update its global links so none point to the old directory.
- Verify every linked `SKILL.md` is readable and matches its canonical copy. Check discovery in fresh Codex, Claude, and Antigravity conversations outside Fleet; readable links alone do not verify provider discovery or tool support.

## How to write skills

- Make every shared skill work with Claude, Codex, and Antigravity.
- Keep each skill description to one line that only says when to use the skill. The description is always sent to the model, so do not explain the skill there.
- Write skill instructions in simple language.

## What to change

- Change `instructions/global.md` when I ask to update my working preferences across agents.
- Create or update shared skills only in `.agents/skills/`.
- When adding a shared skill intended for global use, create or verify its user-level Codex, Claude, and Antigravity symlinks. A symlink inside this repository does not expose the skill to sibling repositories.
- Change this root `AGENTS.md` only for guidance about maintaining Fleet itself.

## What never to change

- Never replace a shared-skill symlink with a copied directory or maintain separate tool-specific copies.
- Never move canonical files or change external symlink targets unless I explicitly ask to change the repository structure.
