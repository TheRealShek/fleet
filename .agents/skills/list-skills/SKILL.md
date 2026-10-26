---
name: list-skills
description: Use when Fleet skill discovery is missing or explicitly requested.
---

# List skills

Use this registry when the harness omits Fleet skills or the user asks what is available. If the catalog already includes the needed skill, read that skill directly. Do not load this registry routinely or read every skill body.

For a task, select the relevant skill below and read its linked `SKILL.md` before using it. When asked for a list, show the relevant names, briefs, and invocation rules without running their workflows.

Links are relative to this file. The canonical root is `/Drive2/Coding_Skills/Personal/fleet/.agents/skills/`; each skill lives at `<name>/SKILL.md`. Missing filesystem access cannot be repaired by this registry. Report an unreadable skill rather than inventing its instructions. A listed skill does not supply tools absent from the harness.

## Automatic skills

Use these when their task conditions apply. Global and task instructions take precedence.

| Skill | When to use |
| --- | --- |
| [rust-conventions](../rust-conventions/SKILL.md) | Writing or changing Rust code, not merely reading it. |
| [go-conventions](../go-conventions/SKILL.md) | Writing or changing Go code, not merely reading it. |
| [code-review](../code-review/SKILL.md) | Unreviewed medium/complex changes or unreviewed changes before pull requests. |
| [commit-work](../commit-work/SKILL.md) | When a scoped local commit helps complete authorized work. |
| [diagnosing-bugs](../diagnosing-bugs/SKILL.md) | Hard bugs, performance issues, or unsuccessful simpler debugging. |
| [pr-file](../pr-file/SKILL.md) | Requested pull requests lacking templates or including UI changes. |
| [write-like-me](../write-like-me/SKILL.md) | Writing beyond direct replies, including documents, posts, comments, and PR text. |
| [tldraw-diagram-maker](../tldraw-diagram-maker/SKILL.md) | Creating or changing TLDraw diagrams. |
| [list-skills](SKILL.md) | Missing Fleet skill discovery or an explicit request. |

## Skills requiring a request

These require the user to name the skill, except `html-communication`, which requires an explicit request to create an HTML PPT.

| Skill | When requested |
| --- | --- |
| [teach](../teach/SKILL.md) | Explain technical topics from first principles with examples and tradeoffs. |
| [html-communication](../html-communication/SKILL.md) | Create an HTML PPT. |
| [frontend-design](../frontend-design/SKILL.md) | Create or reshape frontend visual design. |
| [grill-with-docs](../grill-with-docs/SKILL.md) | Challenge a design and maintain its domain documentation. |
| [unslop](../unslop/SKILL.md) | Edit text beyond direct replies to remove AI writing patterns. |
| [video-script](../video-script/SKILL.md) | Plan technical teaching videos and their speaking cues. |

## Permissions and boundaries

- Only `code-review` and `grill-with-docs` may use subagents without a separate user request. Other skills do not gain delegation permission by appearing here.
- Skip small or redundant code reviews. Reuse a review covering the final diff and recheck affected code after fixes.
- Skill discovery does not authorize edits, commits, publishing, messaging, or desktop interaction beyond the user's task. Preserve read-only requests and explicit restrictions.
- Keep the `write-like-me` and `unslop` workflows separate. Follow the selected skill's instructions and the user's requested experiment.
