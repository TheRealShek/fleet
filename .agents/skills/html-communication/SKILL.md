---
name: html-communication
description: Use only when explicitly asked to create an HTML PPT.
---

# HTML communication

Create HTML slides that support spoken technical teaching. Use diagrams, code, examples, and short explanations to help the audience follow the presenter. Keep the implementation simple.

Read and apply [unslop](../unslop/SKILL.md) to all authored text, including proposals, slide copy, diagram labels, code comments, accessibility descriptions, and delivery text. Preserve the meaning and accuracy of source code, identifiers, and quotations.

## Plan with the user

- Arrange slides into a clear story flow, building on earlier concepts so each new topic follows from a question, consequence, or idea introduced before it.
- Start with the video idea and directions. Ask about the audience, takeaway, duration, or project location only when missing information affects the plan.
- Keep the requested technical subject and format central. Include background, comparisons, status, and roadmap material only when requested or needed to understand the topic.
- Inspect the relevant docs and code. Ground claims about current behavior in the implementation. Separate existing behavior, plans, and your suggestions. Raise conflicts between docs and code; suggest a supported alternative when a requested topic is absent.
- Propose each slide's takeaway, named layout, and main visual. Briefly identify supporting sources and gaps. Ask for the user's opinion, revise the flow, and wait for approval before building. Revisit affected slides if the scope changes.
- If a facecam will overlay the slides, confirm its size and placement. Otherwise reserve no facecam space.

## Opening slide

Start every deck with a static `Title and goal` slide. Follow it directly with the technical explanation, without an agenda or overview slide in between.

- Main title: the topic in one line, at most 8 words. Use 64px semibold, left-aligned in the upper part of the main area.
- Goal: one or two sentences, at most 25 words, stating what the viewer will understand by the video's end. Start with a verb, such as "Understand how mini-kafka stores a record and assigns its offset." Put a small secondary-text "Today's goal" label above the goal, with the goal itself below the title at 40px in primary text.
- Use only these two parts, with no diagram, code, or bullet list. Omit the normal title-band heading. Do not repeat the opening title or goal text elsewhere in the deck.
- Derive both from the user's topic and directions. If the goal is unclear, ask before proposing the slide flow. Include the exact title and goal in the proposal for approval before building.

## Conclusion slide

End every deck with one static conclusion slide. Add no separate thank-you, questions, or roadmap slide after it.

- Title: "Summary" or a topic-specific label in one line, at most 6 words. Use 64px semibold, left-aligned at the opening title's position.
- Takeaways: two to four items drawn from what the approved slides already show. Each starts with a verb or concrete noun and has at most 12 words. Keep all takeaway text within 25 words total. Introduce no new facts, code, or diagrams.
- Set takeaways at 40px in primary text, left-aligned, one item per line with a small blue numbered marker. Match the opening slide's background, margins, and type styles. Show every item immediately.
- For a project-progress deck, optionally add one bottom line of at most 15 words naming the single next step. Include the exact conclusion title, takeaways, and any next-step line in the proposal for approval before building.

## Teach through the composition

- Give each slide one clear takeaway. Choose the content and depth for what the audience needs to learn. Introduce unfamiliar terms before relying on them, and keep names consistent.
- Build understanding through a concrete example and its internal mechanism. Show data movement, state changes, and relevant failures or tradeoffs. Use project examples where available and label illustrative inputs.
- Give a requested flow or mechanism most of the slide body. Connect supporting code and annotations through placement, alignment, grouping, labels, or leaders. Keep titles and supporting text subordinate to the main explanation.
- Choose representations for the relationships, changes, comparisons, structures, or outcomes they expose. Vary layouts when useful, without a variety quota. Code, short lists, and comparisons can lead a slide when they serve the topic.
- Aim for at most 25 words of explanatory prose per slide, with 40 as the ceiling for essential context. The opening and conclusion keep their stricter limits above. Exclude the title, short diagram labels, actual code, and source paths. Do not disguise paragraphs as diagram labels.
- Show the whole explanation when a slide opens. Use numbered operations or before/after views to explain progression without hiding content. Use another slide for a distinct concept or a flow that cannot fit readably; avoid near-identical slides for individual operations.
- Remove repetition and decoration before useful detail. Use space for examples and relationships, without inflating headings or cards. Keep enough context for the talk without writing the presenter's narration.

## Frame and layouts

Use a 1920 × 1080 canvas with 80px outer margins and 1760px usable width. Inside the margins, allocate 120px for the title band, a 24px gap, 736px for the main area, and 40px for navigation. Use 32px column gutters.

| Layout | Main area |
| --- | --- |
| Diagram plus code | 1024px diagram and 704px code |
| Full diagram | 1760px diagram with anchored annotations |
| Before/after | 800px state, 160px operation including gaps, 800px state |
| Comparison | Two 864px zones with aligned properties |
| File tree plus callouts | 576px tree and 1152px connected callouts or flow |

For content slides, choose from these layouts by default; adapt when the explanation needs it. Use equal panels for comparisons, and keep component styling consistent across layouts.

- Fit the entire header within its band, including wrapped titles, subtitles, eyebrows, line heights, margins, and gaps. Shorten wording or remove optional elements when needed. Keep the gap before the main area clear.
- Keep panels and content inside their assigned zones. Budget for padding and borders. Constrain grid children so intrinsic text or code sizes cannot enlarge their tracks.
- If a facecam is requested without a specific placement, reserve a 320 × 180px area at the main area's bottom-right. Keep code, labels, and connectors outside it.

## Diagrams and code

Honor explicit diagram requests. Use Mermaid when requested. Otherwise prefer Mermaid for sequences and handwritten HTML/CSS/SVG for byte layouts, offsets, record stacks, and precise state changes.

- Trace actual entry points, calls, data, state changes, and results. Include branches, errors, and concurrency boundaries when they affect the explanation. Distinguish implemented execution from proposed behavior.
- Draw meaningful structure: fields inside records, indexes beside entries, byte boundaries, ownership groups, or sequence lifelines. Anchor connectors to the relevant elements and label their direction and meaning.
- Show transformations. For an append, display the incoming payload and initial log alongside the assigned offset, inserted record, updated counter, and returned value. Use arrows or operation numbers to show order, keeping unchanged data recognizable.
- Connect relevant code operations or fields to their corresponding structures and changes through leaders, matching accents, or step numbers. Show a useful source path. Mark omissions and pseudocode.
- In the operation being explained, color keywords purple, strings green, and types blue. Keep comments secondary. Use the code-line background, an orange stripe, and matching operation numbers to connect code to the diagram. Use secondary text for supporting code without hiding it.
- Use code at least 32px and target about 30 characters per line in the code column. Measure after padding and annotation gutters. Wrap Rust and Go signatures at syntactic boundaries, keeping actual excerpts valid. Mark omissions instead of clipping, scrolling, or shrinking code.
- Use distinct header and value areas, subtle tinted fills, and consistent corner radii. Make group boundaries distinguishable from individual items. Pair meaningful colors with labels, shapes, or line styles.

For Mermaid, disable automatic width on the diagram type and set base and label sizes to at least 28px. Start with a configuration such as:

```js
mermaid.initialize({
  theme: 'base',
  securityLevel: 'strict',
  htmlLabels: false,
  fontFamily: 'IBM Plex Sans',
  fontSize: 32,
  themeVariables: {
    darkMode: true, fontSize: '32px', background: '#242320',
    primaryColor: '#3a3935', primaryTextColor: '#faf9f5', primaryBorderColor: '#918e84',
    secondaryColor: '#3a3935', secondaryTextColor: '#faf9f5', secondaryBorderColor: '#918e84',
    tertiaryColor: '#3a3935', tertiaryTextColor: '#faf9f5', tertiaryBorderColor: '#918e84',
    textColor: '#faf9f5', lineColor: '#a6a399', edgeLabelBackground: '#242320',
    noteBkgColor: '#3a3935', noteTextColor: '#faf9f5', noteBorderColor: '#918e84'
  },
  sequence: {
    useMaxWidth: false,
    actorFontSize: 32,
    messageFontSize: 32,
    noteFontSize: 32
  },
  flowchart: { useMaxWidth: false }
});
```

After fitting the SVG into its zone, require every diagram label to be at least 28px at canvas scale. Increase source sizes, adjust layout, or divide the flow when needed. Configuration alone does not establish readability.

## Typography and color

Use IBM Plex Sans regular 400 and semibold 600 for text, with semibold titles and primary labels. Use IBM Plex Mono or another readable monospace for code and identifiers. Inter is an alternative if the user prefers it. Avoid condensed type and all caps except acronyms.

| Element | Starting size at canvas scale |
| --- | --- |
| Title | 56 to 64px |
| Primary label | 36 to 44px |
| Supporting text | 28 to 32px |
| Code | 32px minimum |

Keep short labels centered, longer text left-aligned, and source paths discreet. Use 24 to 32px panel padding, meaningful borders of at least 3px, and connectors of 3 to 5px. Define structure with borders and header bars as well as fills. Keep routes clear and arrowheads readable.

| Role | Color |
| --- | --- |
| Canvas | `#242320` |
| Node surface | `#3a3935` |
| Highlighted code-line bar | `#45443f` |
| Primary text | `#faf9f5` |
| Secondary text / comments | `#c8c5bc` |
| Connectors | `#a6a399` |
| Meaningful borders | `#918e84` |
| Orange / operation being explained | `#e8b887` |
| Blue / data and code types | `#9dc7e8` |
| Green / new state and strings | `#a3d2b4` |
| Purple / code keywords | `#d0b8ed` |
| Red / failure | `#f0a0a0` |

Keep accent meanings consistent. Use a warm charcoal base, off-white text, and purposeful accents. Avoid pure black and distracting effects.

Keep important labels opaque. Aim for 7:1 primary text contrast, at least 4.5:1 for secondary text and syntax colors, and 3:1 for meaningful boundaries and connectors. Recheck actual pairs on tinted panels and highlighted code lines.

## Navigation and transitions

Use one plain-JavaScript controller with a slide index. All slide content is visible on entry. Do not implement reveal steps, subviews, or step counters.

- Right Arrow or Next opens the next slide. Left Arrow or Previous opens the previous slide. Clamp at both ends of the deck and show a slide counter.
- Use a 200ms ease-out fade with about 32px horizontal movement between slides. Moving forward brings the new slide from the right while the old slide exits left; moving backward reverses the direction. Animate slide layers, not the canvas-fit transform. Prevent overlapping transitions during rapid navigation, and restore final positions and full opacity afterward.
- Respect `prefers-reduced-motion` with immediate switching. Keep content still within a slide, with no autoplay. Only the current slide may receive focus or be exposed to assistive technology.
- Hide buttons, the counter, and their background at rest. Show them only on footer hover or keyboard focus within the footer. Keep a stable hover area, disable pointer events on invisible controls, and keep buttons reachable by Tab.
- Hide the cursor over the deck and its controls after two seconds without pointer activity. Restore it immediately on pointer movement or a click, without disturbing keyboard focus.
- `F` toggles fullscreen through the deck container's `requestFullscreen()` and `document.exitFullscreen()`. Handle rejected promises. On `fullscreenchange`, refit the canvas while preserving the current slide. Support Escape to exit.
- Ignore held-key repeats, modified shortcuts, and typing in editable fields. Preserve normal keyboard behavior within focused controls. Keep navigation behavior consistent in fullscreen.

## Build and save

- Use plain HTML, CSS, and JavaScript with Mermaid as the only optional deck dependency. Authoring may use an available browser or renderer; those tools are not playback dependencies.
- Save each deck at `/Drive2/Coding_Skills/HTML-Communication/<topic>/index.html`. Preserve existing work and choose a new folder for an unrelated deck with the same name.
- Use `IBMPlexSans-Regular.woff2`, `IBMPlexSans-SemiBold.woff2`, and `IBMPlexMono-Regular.woff2` from this skill's `assets/fonts/`. Embed them in `@font-face` or copy them beside the deck. Include `assets/fonts/OFL.txt`. A few hundred KB is acceptable. Load fonts before measuring or rendering.
- Render Mermaid during creation and embed its SVGs, retaining the source inside the HTML. Keep scripts and styles inline where practical. Open directly in Chrome without a server, installed fonts, or network access.
- Show one slide at a time, fitted to the viewport at 16:9. Set the page and fullscreen backdrop to the canvas color so letterboxing matches. Keep navigation and diagram descriptions accessible, escape inserted source content, and retain Mermaid's strict security setting.
- Deliver only the presentation and required assets. Leave out narration scripts, speaker notes, planning documents, and an application around the deck.

## Verify and deliver

Render a representative mechanism slide early. Check its composition before repeating the design across the deck.

- Before delivery, open every slide in the browser after fonts load, at both 1920 × 1080 and 1280 × 720. Check settled layouts after transitions finish.
- Check bounded layout containers and text/code blocks for `scrollWidth > clientWidth` or `scrollHeight > clientHeight`, even when overflow is hidden. These layout measurements are unaffected by the fit-to-window transform; do not scale them.
- For region checks, use `scale = canvas.getBoundingClientRect().width / 1920`. Subtract the canvas rectangle's left/top from each element rectangle's left/top, then divide those offsets and its width/height by `scale`. Compare these canvas coordinates with the assigned header, panel, and main-area bounds, never viewport rectangles directly with canvas dimensions.
- Visually inspect each slide for clipping, overlap, readability, and hierarchy. Check the approved opening and conclusion, technical accuracy, text limits, diagram sizes, controls, and offline playback. Test transitions in both directions, rapid navigation, and reduced motion.
- Fix failures and repeat affected checks. Do not conceal overflow or shrink text below its minimum size. Deliver the `index.html` path and list the slides and both viewport sizes checked, plus any failures or unverified checks. Keep research links in the conversation unless visible attribution is requested.

## Sources

These defaults draw on [IBM technical diagrams](https://www.ibm.com/design/language/infographics/technical-diagrams/design/), [Anthropic's brand reference](https://github.com/anthropics/skills/blob/dbd4588f9e1033efb41dad4bef2f7947c8993d44/skills/brand-guidelines/SKILL.md), [WCAG contrast guidance](https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced.html), and Mermaid's [themes](https://mermaid.js.org/config/theming.html), [sizing](https://mermaid.js.org/config/schema-docs/config-defs-base-diagram-config.html), and [sequence configuration](https://mermaid.js.org/config/schema-docs/config-defs-sequence-diagram-config.html). Bundled fonts and their license come from [IBM Plex](https://github.com/IBM/plex/tree/39276912b05f700ee1dd491950c35d8697214208).
