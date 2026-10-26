---
name: tldraw-diagram-maker
description: Use when creating or improving a diagram in TLDraw.
---

# TL draw diagram maker

Make the requested diagram understandable by looking at it.

## Follow the task

Start with the current request. Keep the diagram type, subject, scenario, and level of detail requested. Don't turn one request into a collection of diagrams.

For a project's request sequence, inspect the code and docs, then trace that request from entry to completion. Identify the real participants, calls, responses, and state changes. Include failures or cancellation where they change that flow. Keep implemented and planned behavior distinct.

Use that understanding to select what belongs in the requested diagram. Reading the whole project doesn't mean drawing the whole project. Choose a representative request when the context makes it clear. Ask only when an unresolved choice would materially change the picture.

Stop when the requested outcome is explained. Don't turn the sequence into an exhaustive call graph. Collapse setup or cleanup that doesn't change the explanation into one short message, or leave it out. Don't bring unrelated features into the picture just because their code runs on the same request.

For an intervention during ongoing work, establish the starting state and associations needed to explain why it affects that work. Preserve those links when compressing setup.

Before detailed drawing, briefly propose the question, main participants or groups, and reading direction. Wait for the user's brief confirmation before building it out. Reuse an already approved plan for small revisions.

## Make the flow understandable

- Give the reader a clear starting point and direction. In a sequence diagram, put participants across the top and let time flow down.
- Use position, grouping, and boundaries to explain relationships and ownership. Show real services or meaningful components. Don't give every helper its own lifeline.
- Keep a consistent level of detail among peers. Nested detail is useful when the enclosing boundary clearly shows ownership. Don't mix deployment boundaries, internal helpers, and individual code statements as peers in the same view.
- Make arrows say who calls whom and what happens next. Distinguish calls, returns, cancellation, and dependencies. Keep the actual caller visible.
- Keep labels short and specific. Name the action or component, then add only what explains its role. Don't paste documentation into boxes.
- Keep implementation mechanics such as mutexes, counters, and metrics out unless they are the subject. Show the state change they achieve. Notes explain a necessary boundary; they aren't a place to collect every other error case.
- For a component, aim for a name and one short purpose line. For a connection, use a verb and its object. Group related detail at the chosen level instead of adding paragraphs, shrinking the text, or adding unrequested diagrams.
- Leave breathing room between shapes, connectors, and labels. Use hierarchy to guide the eye.

Each picture should answer the requested question. A system map explains processes and state ownership. A sequence explains events in order. Layers help when there is a real hierarchy. Choose the structure that serves the task; don't force a template or add another view by default.

## Lay out the picture

- Title the diagram with the question it answers.
- Use one readable body size for labels and a larger size for the title. Add an intermediate size for section headings when grouping needs it. Make room for labels instead of shrinking individual ones.
- Keep sequence messages straight and horizontal, with separate rows in time order. Use elbow connectors for system maps so routes follow the layout.
- Route arrows without crossing other arrows or unrelated boxes and labels. Reorder participants or move routes into clear lanes before adding bends. Sequence messages may cross lifelines on their way to the receiver. Those intersections don't mean a call to each participant they pass.

## Give lines a consistent meaning

Use at most two line styles and no legend. If the reader needs a legend, simplify the notation and make connection labels more specific.

- In a sequence, use solid arrows for calls and signals, and dashed arrows for returns. Label cancellation as an action, such as `cancel upstream request`. Label asynchronous handoffs with their actual action, such as `enqueue job`, and show later work separately without implying the caller waits.
- In a system map, use solid arrows for the relationship the view explains. Label each with its meaning, such as `sends requests`, `reads configuration`, or `publishes events`. Add a second style only when the question requires a distinction, and keep that meaning consistent throughout.
- Lifelines and frames support the layout. Keep them visually secondary so readers can follow the arrows. Never use a line style for several conflicting meanings.

## Follow the visual brief

Use the style, references, and output location supplied for this task. By default, save diagrams in the user's Documents folder. Use black and white with one light grey, or a small muted palette for meaningful groups. Keep connectors thick and arrowheads readable at normal viewing size. Size `l` with triangular heads works well in the offline app.

Use colour consistently, with dark text on light fills and a white background. Colour should reinforce labelled structure without requiring a colour key.

Always export diagram images in light mode with a white background, regardless of the editor theme. Inspect the exported image to verify this.

Use editable shapes with bound connectors and save in the native format. Preserve the parts the user wants to keep. Improving one page doesn't mean redrawing another.

When given a reference, learn from its reading order, grouping, and relationships. Apply those lessons to the task. Copying its appearance won't give the diagram meaning.

## Use the available tools

Use the offline TLDraw app unless the user explicitly requests the online version. Discover its local API from `$XDG_CONFIG_HOME/tldraw/server.json`, or `~/.config/tldraw/server.json` when unset. Read the loopback server's `/readme` for current operations. Use its token as a Bearer credential where required. Never print it.

Read the selected environment's tool or API instructions instead of assuming supported operations. Select the document by its exact path and inspect the canvas before editing. For a locally owned document with a destination in Documents, use `helpers.saveDoc()` as supported by the app's instructions. Refresh affected exports after saving.

This skill needs no companion skill, downloaded library, or mandatory web research. Use existing tools before adding dependencies. If TLDraw access is missing, explain the missing capability. Don't silently substitute another drawing tool.

## Finish the drawing

Render and inspect it at the intended reading size. Check the meaning and flow as well as arrowheads, crossings, collisions, clipping, and connector bindings. Follow each arrow from its source to its target in the rendered image. Fix routes that become ambiguous. A clean linter doesn't prove the drawing makes sense.

If it needs fine-print footers or constant zooming, remove or group detail before shrinking the text. Check that the requested outcome is easy to find and trace without your accompanying explanation.

Trace the requested scenario through the finished picture against the implementation. Check callers, return paths, state changes, and cleanup. Show concurrent work and asynchronous handoffs as they happen. Distinguish work during the response from work after it ends. Fix any relationship the picture gets wrong.

Save through the environment's supported operation at the requested destination. Refresh affected exports. Handle TLDraw work in the background and deliver the finished image directly in chat. The user should be able to request revisions through the agent without opening TLDraw or interacting with the canvas. Keep the native file available for editing, but don't make opening it a prerequisite for viewing the result. Report any save or preview check that couldn't run. Keep the accompanying explanation short.
