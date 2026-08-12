# Fleet

This repository is my source of truth for reusable AI-agent configuration. I use it to keep my working agreements, shared skills, and tool-specific adapters consistent across agents.

## How I organize it

- `instructions/global.md` contains my global instructions. Keep guidance specific to Fleet in this root `AGENTS.md`.
- `.agents/skills/` contains the canonical copies of my shared skills. Tool-specific skill directories should symlink to them instead of duplicating them.
- Preserve working symlinks and keep their targets portable within this repository whenever possible.

## What to change

- Change `instructions/global.md` when I ask to update my working preferences across agents.
- Create or update shared skills only in `.agents/skills/`.
- Change this root `AGENTS.md` only for guidance about maintaining Fleet itself.

## What never to change

- Never edit skill content through `.claude/`; it is only a compatibility layer of symlinks to `.agents/skills/`.
- Never replace a shared-skill symlink with a copied directory or maintain separate tool-specific copies.
- Never move canonical files or change external symlink targets unless I explicitly ask to change the repository structure.
