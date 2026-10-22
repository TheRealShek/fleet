---
name: video-script
description: Use when explicitly asked to use video-script to plan a technical teaching video or write its speaking cues.
disable-model-invocation: true
---

# Video script

Turn a topic, title, and coverage notes into a recording script for Abhishek. Write short speaking cues with room to improvise.

## Plan

- Use the supplied audience, prerequisites, duration, language, and media constraints. With only a topic, title, and coverage notes, choose reasonable defaults and proceed. Ask only when an assumption could change the intended lesson.
- Define what the viewer should be able to explain or do afterward. Include only necessary prerequisites, points that serve this outcome, and likely misunderstandings. List important exclusions briefly.
- Order sections around questions the viewer would naturally ask. In the opening section, preview the central mechanism in one plain sentence, then build the explanation. Reuse one concrete example where practical.
- Choose diagrams for relationships, state, and movement. Choose code for implementation and observable behavior. Switch when the explanation needs it.
- Estimate section durations with time for typing, drawing, runs, pauses, and improvisation. Simplify overloaded sections or show prepared code. If coverage cannot fit, state the scope tradeoff and suggest a split. Put deferred topics in preparation notes instead of rushing through them at the end. Timing stays approximate until rehearsed.
- Verify technical claims against primary sources and inspect supplied code. Check demo behavior when tools permit. Distinguish checked results from expected ones. Speak caveats that prevent a wrong takeaway; keep secondary exceptions and references in presenter notes.

## Speaking style

These preferences come from one diagram-led Rust introduction. Adapt them to feedback and new samples. Do not assume they describe live coding habits.

- Use plain, conversational English unless another language is requested. Match the requested spoken language while keeping technical labels consistent.
- Start with a concrete question. Explain the necessary mechanism before naming the feature that solves the problem.
- Trace an example through a change and its consequence. Explain why the result happened.
- Use natural transitions such as "Now what happens?" and "For that, we need to understand..." only when they fit. Avoid repeated catchphrases, fillers, false starts, and forced questions.
- Prepare names, examples, and drawing steps in advance. Leave freedom in the spoken explanation.
- Write exact sentences for opening cues, precise definitions, and important caveats. Use short thought cues elsewhere. Close by answering the opening question.

## Script format

Start with the audience, learning outcome, rough duration, and any essential assumptions or exclusions. Then write numbered sections using this format:

- **Question:** The one question this section answers.
- **Opening cue:** One speakable sentence.
- **Thought flow and screen actions:** Usually three to five short cues, each pairing the current screen action with the thought to explain. Use one sentence per cue where practical, not a paragraph of dialogue. Name the asset, what changes, and why it matters. Use stable IDs such as D1 and C1. Include a prediction question when useful.
- **Takeaway:** The idea the viewer must understand before moving on.
- **Transition:** A short bridge to the next section. End the last section with a closing line instead.

Use actions such as "Show D1 and trace the request arrow" or "Run C1, inspect the output, then explain why it changed." If revealing output in stages, specify the run, stepping, or concealment method. Avoid "explain the diagram."

## Preparation guide

Append these after the script:

1. A small Mermaid flowchart of the major sections, labeled with diagram, code, or spoken explanation. Use plain text if Mermaid is unavailable.
2. A diagram list keyed by ID. Give its purpose, section, exact labels, layout, and reveal states. State what starts visible and any reset needed when reusing it. Specify readable black-and-white visuals with no dependence on color. Keep each brief usable by a drawing agent; omit spoken explanations already in the script.
3. A code-demo list keyed by ID. Give the language and relevant version, setup, starting code or valid file reference, edits, expected result, and concept demonstrated. Include recovery for likely failures and verification status. Keep code reproducible but minimal. Define each code state once and reference it from the script instead of repeating instructions or full outputs.
4. Brief source links and presenter-only caveats when needed.

Omit unused asset lists. Reuse diagrams where possible. Prepare asset instructions by default; create images or runnable demo files only when requested.

## Final pass

Apply `unslop` if available. Cut essays, repetition, tangents, and production notes from speaking cues. Preserve useful examples and necessary caveats. Recheck the busiest section for action time and room to improvise. Fix unresolved asset IDs, vague screen actions, and missing media labels in the flowchart. Ensure the closing delivers the promised outcome. Return the script and preparation guide without process commentary.
