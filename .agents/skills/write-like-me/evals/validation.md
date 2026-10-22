# Validation record

Date: 17 October 2026.

One GPT-6.1 Sol subagent with medium reasoning effort generated the drafts. The same subagent handled retries and holdouts; no additional subagent was used. The parent independently inspected outputs and compared the profile with the saved source articles. Generated prose remains outside the repository.

## Findings and corrections

- A short personal draft repeated its facts to meet a minimum length. The profile now forbids padding and requires an honest length note when the source cannot support the requested length. The original sparse request still did not meet its minimum; an additional case with fuller notes passed.
- The initial research drafts were clearer than they were distinctive. A source audit found that their repeated call for further investigation displaced the engineering judgment. An original research calibration example now shows the benefit, mechanism, supported local result, and relevant limit together.
- The initial team rewrite lost the supplied first-person stance. The profile now explicitly preserves supplied I and we. Follow-up personal and team rewrites retained their narrators without inventing experience.
- A procedure referred to the prompt's supplied signs of success. The profile now tells the writer to address the intended reader and omit drafting instructions. The procedural retry used the actual steps and observable outcomes.

## Final behavioural checks

Two successive final batches produced seven inspected drafts with no new actionable findings:

- Procedure retry: 110 whitespace-separated words, within the requested 100 to 150.
- Relative-symlink holdout: 171 words, within 150 to 210, with the target resolved from the link's directory.
- Condition-variable holdout: 155 words, within 140 to 190, with five lines of labelled pseudocode and the predicate rechecked under the mutex.
- Team rewrite: 117 words, within 110 to 160, preserving we, the measurements, memory cost, and different-day limitation.
- British personal note: 76 words, within 75 to 105, preserving the literal `color_mode` identifier.
- Research holdout: 166 words, within 140 to 190, preserving the fictional-study label, measurements, proposed mechanism, and untested limits.
- Configuration explanation: 180 words, within 150 to 200, distinguishing a changed file from settings already held in memory and limiting the explanation to the stated application.

Earlier regression checks also preserved an exact quotation containing an em dash and a legitimate technical use of robust, kept a requested three-bullet format, and followed British spelling without changing identifiers. The sparse-note case returned its supported short draft and reported the length limitation separately.

## Installation and structural checks

A fresh Codex app-server `skills/list` request with `forceReload` discovered an enabled user-scoped `write-like-me` skill from a directory outside Fleet. Its path resolved to the canonical `SKILL.md`, and its display name was Write like me. No model conversation was started for that catalog check. The earlier subagent's injected catalog had been stale; it used the installed path explicitly.

The skill validator, metadata, Markdown references, whitespace, and all three global symlinks were checked. Codex, Claude, and Antigravity links resolve to the same canonical skill and readable profile. Fresh Claude and Antigravity conversation discovery was not tested.

These are small behavioural tests and a qualitative comparison with calibration material. They do not guarantee results across every topic. The evidence is strongest for technical explanation and research discussion. Personal writing remains a conservative adaptation of those habits.
