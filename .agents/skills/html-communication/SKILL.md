---
name: html-communication
description: Use when explicitly asked to create HTML slides for a narrated video or presentation.
---

# HTML communication

Create a clear, visually rich HTML presentation that supports spoken teaching. Combine diagrams, concise explanations, code, and examples to help the audience follow the talk. Include enough context to follow the explanation while leaving the full narration to the presenter. Keep the implementation simple.

Read and apply [unslop](../unslop/SKILL.md) to all text you author for the task, including proposals, slide copy, diagram labels, code comments, accessibility descriptions, and delivery text. Preserve source code, identifiers, and quoted text when editing them would change their meaning or accuracy.

## Understand and propose

- Start with the user's video idea and directions. Ask about the audience, intended takeaway, or duration only when the missing answer would change the flow.
- Let the requested technical subject and format set the scope. For a code flow or mechanism walkthrough, keep that explanation central. Add background, comparisons, status, or roadmap material only when it supports the requested understanding or the user asks for it.
- For a project walkthrough, inspect the relevant docs and code before proposing slides. Follow the parts needed to understand the topic rather than reading the whole repository. Ask for the project location if it is unavailable.
- Ground claims about existing behavior in the implementation. Keep what is built, what is planned, and your suggestions distinct. Raise important conflicts between docs and code before presenting them as facts. If the code does not support a requested topic, suggest a nearby topic it does support.
- Propose a concise slide-by-slide flow. For each slide, describe its takeaway, named layout, main visual, and reveal steps when needed. Briefly identify the sources behind project claims and any important gaps. Cover the user's goal, including what matters and what can be left out.
- Ask for the user's opinion on the flow. Revise it together and wait for approval before creating the deck. If the user changes the scope later, revisit the affected slides.

## Compose the presentation

- Give each slide a clear takeaway, supported by enough detail for the presenter to explain it. A useful opening, scope list, limitations, or next-steps slide can belong in the flow. Choose the slide count from the story and depth the topic needs.
- For each technical concept, establish what the audience needs to understand, then choose the content, representation, and depth that make it clear. Select useful details from the available information. A useful progression is to introduce the idea, demonstrate it with a concrete example, and explain the relevant internals. Adapt that progression to the topic and audience rather than making it a fixed slide formula. Include failure cases and tradeoffs when they help understanding.
- Introduce unfamiliar concepts and project-specific terms before relying on them. Use the same names throughout and connect implementation names to the concepts they represent.
- Choose a layout from the frame below according to the explanation. Use it consistently within the deck, adapting only when the content needs a different arrangement.
- Compose each slide around a focal explanation. Give a requested technical diagram or mechanism most of the body; a smaller code or annotation column can support it. Use size, position, spacing, contrast, and grouping to make the main explanation recognizable immediately. Keep supporting material subordinate, titles compact, and related elements aligned. Use equal panels for genuine comparisons.
- Choose representations for the relationships, changes, comparisons, structures, or outcomes they reveal. Vary layouts when the explanation benefits, rather than to meet a variety quota. Technical flow slides should retain a prominent diagram; other slides may center on code, a comparison, or a short list when that better serves the user's topic.
- Aim for at most 25 words of explanatory prose per slide, with 40 as the ceiling when essential context needs it. Count across all reveal steps. Exclude the title, short diagram labels, actual code, and source paths; do not move paragraphs into diagrams to evade the budget. Use compact callouts and let the presenter supply the narration.
- Show how data moves or state changes, using concrete details such as record contents, offsets, ownership, request fields, or failure paths. Prefer actual project examples and code when available, and clearly label illustrative inputs. A component list or generic chain of boxes can orient the audience; develop the explanation by tracing what happens to a specific example.
- Develop one mechanism through reveal steps within the same slide. Use another slide for a distinct concept or a flow that cannot fit readably, rather than creating near-identical slides for each operation. Keep names, positions, and visual meaning consistent.
- Balance density with readability. Remove decoration and repeated prose before removing useful facts. Split overloaded slides, while giving related code, visuals, and explanations enough space together. Do not reduce every slide to a single row of boxes.
- Use available space to clarify the example, relationships, or consequences. Avoid oversized headings, inflated cards, or enlarged labels that crowd out useful detail. Leave breathing room deliberately; do not pad a weak composition with trivia or extra boxes.

## Frame and layouts

Use a 1920 × 1080 canvas with 80px outer margins. The usable width is 1760px. Reserve a 120px title band, a 24px gap, a 736px main area, and a 40px footer for navigation. Use 32px gutters between main-area columns.

- Fit the complete header stack inside the title band, including any eyebrow, wrapped title, subtitle, line heights, margins, and gaps. Shorten the wording or remove optional header elements when they do not fit. The main area must begin after the title band and its gap, without covering header text.
- Keep panels and their contents within their assigned main-area zones in every reveal state. Include padding and borders in the size budget, and reserve space for hidden future content. Constrain grid children so intrinsic code or text sizes cannot silently enlarge the tracks; then resolve any remaining content overflow.

Choose from these layouts by default:

| Layout | Main-area structure |
| --- | --- |
| Diagram plus code | 1152px diagram zone and 576px code zone |
| Full diagram | One 1760px diagram zone with anchored annotations |
| Before/after | Two 864px state zones, with the operation connecting them |
| Comparison | Two 864px zones with aligned properties and differences |
| File tree plus callouts | 576px tree zone and 1152px connected responsibility or flow zone |

If the user will overlay a facecam, confirm its placement and size in the brief. Default to a 320 × 180px safe area at the main area's bottom-right when no other placement is given. Keep labels, code, and connectors outside that area. Reserve no facecam space when none is requested. Keep the frame steady during reveals, including space for hidden future steps.

## Draw mechanisms and connect code

- Honor explicit diagram requests. When the user asks for Mermaid, use it for the requested diagrams. Otherwise prefer Mermaid for sequence diagrams and handwritten HTML/CSS/SVG for byte layouts, offsets, record stacks, and precise state changes. Standard notation is welcome; diagrams need faithful technical detail and clear relationships, not decorative complexity.
- For Mermaid, set the diagram type's `useMaxWidth: false`, a base font of at least 28px, and explicit label sizes. A practical starting configuration is `fontFamily: 'IBM Plex Sans', fontSize: 32, themeVariables: {fontSize: '32px'}`, with `sequence: {useMaxWidth: false, actorFontSize: 32, messageFontSize: 32, noteFontSize: 32}` or `flowchart: {useMaxWidth: false}` as appropriate. Measure the final SVG after fitting it into its zone. Every diagram label must remain at least 28px at canvas scale; increase source sizes, relayout, or divide the flow when needed. Disabling automatic width alone does not guarantee readable text.
- For a working codebase flow, trace the actual entry points, calls, data passed, state changes, and results relevant to the topic. Show important branches, errors, or concurrency boundaries when they affect the explanation. Use implementation names where useful and distinguish current execution from proposed behavior. Expand a broad flow across focused diagrams when needed, without adding unrelated presentation sections.
- Show the transformation. For an append operation, reveal the incoming payload and initial log, then the assigned offset and inserted record, then the updated counter and returned value. Keep unchanged data recognizable and emphasize what changed. Use the reveal controller below to advance the explanation.
- Make code part of the visual explanation. Select the relevant operations or fields, highlight them, and connect them to the matching record, pointer, byte range, or state change with anchored leaders, step numbers, or matching accent labels. Syntax coloring alone does not explain the operation. Show a useful source path and clearly mark omissions or simplified pseudocode.
- Use purple `#d0b8ed` for keywords, green `#a3d2b4` for strings, blue `#9dc7e8` for types, and orange `#e8b887` for comments in the active code operation. Give its line or line group a `#45443f` background bar, an accent stripe, and the matching reveal-step number. Render unhighlighted revealed lines in secondary text color. Keep code emphasis synchronized with the diagram.
- Wrap long Rust or Go signatures at syntactic boundaries, placing parameters and generic bounds on separate lines. Show only relevant fields or operations and mark omitted signature details clearly. Preserve valid syntax in excerpts presented as actual code. Avoid horizontal scrolling, clipped generics, or shrinking the entire excerpt to fit one long line.
- Give structures meaningful internal detail instead of generic names alone. Show fields inside a record, indexes beside stored entries, ownership around shared state, or byte boundaries inside a request when those details teach the concept. Route connectors to the elements they describe, keep arrow direction clear, and place labels beside the relevant connection.
- Style components consistently within the deck: distinct header and value areas, subtle tinted fills, measured corner radii, and a clear difference between group boundaries and individual items. Let color identify corresponding operations and structures, with labels preserving the meaning. Vary the composition without changing the visual vocabulary on every slide.

## Reveal and navigation

- Implement one plain-JavaScript controller with a slide index and a step index. Give each staged element a `data-step` number shared by its diagram, code highlight, and annotation. A slide starts at step zero. Static overview or comparison slides may have one step.
- Right Arrow and the next button advance a step. After the final step, they open the next slide at step zero. Left Arrow and the previous button reverse a step; from step zero, they open the previous slide at its final step. Clamp at the deck's beginning and end. Show the slide counter and, on staged slides, a discreet step counter.
- Hide navigation chrome, including buttons, counters, and their background, while idle. Keep a stable hover area in the reserved footer; reveal the controls only while that area is hovered or contains keyboard focus. Use an opacity change without shifting content, and disable pointer events on invisible controls while keeping them reachable by Tab. Hovering elsewhere on the slide must not reveal the bar. Keep this behavior in fullscreen too.
- Pressing `F` toggles browser fullscreen for the deck through the Fullscreen API. Enter with the deck container's `requestFullscreen()` and leave with `document.exitFullscreen()`. Ignore held-key repeats, modified shortcuts, and typing in editable fields. Handle rejected requests without breaking the presentation. On `fullscreenchange`, refit the canvas to the available viewport while preserving the current slide and reveal step; exiting with `F` or Escape restores the normal view.
- The current step is fully opaque with its accent emphasis. Earlier visual elements remain at about 50% opacity; future steps use `visibility: hidden` and are hidden from assistive technology without changing layout. Keep titles and persistent context visible. Keep still-needed labels and code in a separate opaque secondary-text layer so dimming shapes does not make the explanation unreadable. Hidden elements must not retain keyboard focus.
- Advancing or reversing updates visibility and emphasis immediately, with no autoplay or timed animation. Retain the same geometry and scroll position across steps. Give the new record and its code operation matching emphasis. Overviews and comparisons can give several elements equal weight.

## Visual defaults

- Use IBM Plex Sans for titles, labels, and explanations, with regular 400 and semibold 600. Use IBM Plex Mono or another readable monospace for code and identifiers, with restrained syntax highlighting. Avoid condensed type and all caps except acronyms. Inter is an alternative when the user prefers it.
- On the design canvas, start around 56–64px for titles, 36–44px for primary labels, 28–32px for supporting text, and 24–30px for code. Keep diagram labels at least 28px after SVG fitting. Keep the title and subtitle within their band, and keep source paths and metadata discreet. Keep short labels centered and longer text left-aligned.
- Use 24–32px panel padding, at least 3px meaningful borders, and 3–5px connectors at canvas scale. Define structure with clear borders and header bars as well as the brighter panel fill; do not rely on a dark fill difference alone. Keep alignment and spacing consistent, with clear arrowheads and simple routing without crossings.
- Keep a warm charcoal base with off-white text. Use a few purposeful accent colors for components, relationships, code, and emphasis, with lightly tinted panels where helpful. Keep the meaning of each accent consistent across slides. Avoid pure black, distracting effects, and gratuitous color.

| Role | Color |
| --- | --- |
| Canvas | `#242320` |
| Node surface | `#3a3935` |
| Active code-line bar | `#45443f` |
| Primary text | `#faf9f5` |
| Secondary text | `#c8c5bc` |
| Connectors | `#a6a399` |
| Meaningful borders | `#918e84` |
| Warm orange accent | `#e8b887` |
| Blue accent | `#9dc7e8` |
| Green accent | `#a3d2b4` |
| Purple accent | `#d0b8ed` |

- Keep important labels opaque. Aim for 7:1 primary text contrast and at least 4.5:1 for secondary text and syntax colors; meaningful boundaries and connectors need at least 3:1 against adjacent colors. Check actual foreground/background pairs, including active-line bars, tinted panels, and dimmed states. Primary text exceeds 7:1 on both base surfaces; secondary text and accents exceed 4.5:1.
- Pair color with labels, shapes, or line styles when it conveys meaning. For example, explicitly label built and planned components and use solid versus dashed borders, with a small key when needed.
- Default to embedding Plex Sans regular, Plex Sans semibold, and Plex Mono as WOFF2 data URLs in `@font-face`, preserving license notices. A few hundred KB of font data in `index.html` is acceptable for these one-off decks. Local bundled WOFF2 files are also acceptable when the user prefers separate assets. Do not depend on installed fonts or a CDN. Load fonts before rendering or measuring diagrams.

These defaults draw on [IBM's technical diagram guidance](https://www.ibm.com/design/language/infographics/technical-diagrams/design/), [Anthropic's published brand reference](https://github.com/anthropics/skills/blob/dbd4588f9e1033efb41dad4bef2f7947c8993d44/skills/brand-guidelines/SKILL.md), [WCAG contrast guidance](https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced.html), and Mermaid's [diagram sizing](https://mermaid.js.org/config/schema-docs/config-defs-base-diagram-config.html) and [sequence font configuration](https://mermaid.js.org/config/schema-docs/config-defs-sequence-diagram-config.html). The type sizes, geometry, and accent choices are adaptations for these presentations.

## Build the deck

- Save each presentation in its own folder under `/Drive2/Coding_Skills/HTML-Communication/<topic>/`, with `index.html` as the entry point. Choose a new folder when a name already belongs to another presentation. Preserve existing work.
- Use plain HTML, CSS, and JavaScript. Avoid application frameworks, build systems, slide libraries, and extra dependencies beyond Mermaid unless the user requests them.
- Make the finished deck open directly in Chrome through `index.html`. When using Mermaid, render diagrams during creation and embed their SVGs, retaining the source inside the HTML for edits. Keep scripts and styles inline where practical. Playback should not require a server or network requests.
- Default to a 1920 × 1080 presentation canvas with one slide visible at a time. Fit the canvas to the window while preserving its 16:9 proportions.
- Use the reveal controller for previous and next navigation with arrow keys and discreet buttons. Preserve normal keyboard behavior within focused interactive controls.
- Keep navigation keyboard accessible and diagrams meaningfully described for assistive technology without adding visible prose. Escape source content before inserting it into HTML and keep Mermaid's strict security setting.
- Deliver only the presentation and any assets it actually needs. Do not add speaker notes, narration scripts, planning documents, or a separate application around it.

## Check and deliver

- Render a representative mechanism slide early to check composition and component styling before repeating the approach across the deck.
- Open the actual generated page in an available browser. Confirm requested diagrams are present, fully rendered, readable, and prominent enough to explain the flow. Inspect every reveal state for clipping, overlap, unintended visibility, focusable hidden content, and accidental scrollbars at the intended recording size.
- After fonts load, measure rendered header, panel, and content bounds against their assigned regions in every reveal state. Check both content overflowing a panel and whole panels exceeding the main area. Resolve failures by shortening, rearranging, or moving content to another meaningful slide, then remeasure. Clipping, hidden overflow, and smaller unreadable text do not count as fixes.
- Inspect screenshots of individual slides and an overview of the deck. When the user supplies a visual reference, compare actual panel proportions, spacing, density, hierarchy, component styling, color roles, and layout variety against it. Treat it as a design quality target while keeping the presentation's own content and layouts. Do not copy its code or factual claims. Use the written criteria when no reference is available; do not bundle a reference image into the skill.
- Identify specific composition weaknesses and redesign them before delivery: a title that overpowers the mechanism, repeated equal-sized cards, unconnected code and data, weak grouping, text-heavy panels, default diagrams, or unused space where a concrete example needs detail. Verify the revised render. Successful loading and accurate text do not establish visual quality.
- Review the deck as a whole for narrative progression, useful detail, and layout variety. Check that unfamiliar terms are introduced and that mechanism explanations show what happens to data or state. Revise repeated generic diagrams, decorative visuals that explain nothing, and slides too sparse to support the intended explanation. Check the selected code and factual claims against their sources.
- Review from the audience's perspective: what attracts attention first, can they trace the intended mechanism and its related elements, and can they follow the presenter without reading every panel? Revise competing support text and remove material that distracts from the requested technical subject.
- Measure the smallest visible diagram text after SVG fitting and transforms, correcting for the outer slide-to-window scale. Require at least 28px at the 1920px canvas scale, then inspect at 1280 × 720 and a realistic playback width. Verify the intended font loaded; source font sizes alone do not establish readability. Check the prose budget, syntax colors, panel boundaries, and any facecam safe area.
- Check forward and reverse steps, transitions between slides, the first and last deck boundaries, and a smaller window. Confirm future content stays hidden and geometry stays stable. Confirm the finished page works through a local file URL without network access.
- Check `F` to enter and exit fullscreen, Escape to exit, and canvas fitting without losing the current step. Verify the entire navigation bar is invisible at rest, appears on footer hover or keyboard focus, and disappears after both leave, in normal and fullscreen views.
- Fix visual and factual problems before delivery. If browser verification is unavailable, say which checks remain unverified.
- Give the user the path to `index.html` and briefly report what was checked. Keep research references in the conversation, away from the recording canvas, unless the user wants visible attribution.
