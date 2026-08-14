---
name: grill-with-docs
description: Use only when the user explicitly invokes `$grill-with-docs` to sharpen a plan, decision, or idea while maintaining domain docs.
---

# Grill with Docs

Interview the user relentlessly until you reach a shared understanding. Map the discussion as a design tree: every decision branches into the decisions that depend on it.

Do not implement the plan or design. Finish when the user confirms that the shared understanding is complete.

## Run the Interview

Work in rounds. The frontier is every decision whose prerequisites are settled. Ask the whole frontier in one round, then wait for the user's answers before continuing.

Format each question like this:

```md
❓ **Q1** - **<question title>**: <question, context, and choices>

➡️ <recommended answer>
```

Recompute the frontier after every answer. Defer questions that depend on an unsettled decision to a later round.

Find facts by inspecting the environment; do not ask the user for facts you can discover. The decisions remain the user's. If independent exploration can run concurrently, use sub-agents when available without delaying unrelated frontier questions.

The session is complete only when the frontier is empty and the user confirms the shared understanding.

## Maintain the Domain Model

Read existing `CONTEXT.md`, `CONTEXT-MAP.md`, and relevant ADRs before the interview.

During the interview:

- Call out conflicts between the user's language and the existing glossary.
- Sharpen vague or overloaded terms into precise canonical terms.
- Stress-test domain relationships with concrete edge cases.
- Check statements about current behavior against the code and surface contradictions.
- Update the relevant `CONTEXT.md` as soon as a term is resolved. Create it lazily when the first term is ready.

Keep `CONTEXT.md` free of implementation details. It is a domain glossary, not a specification or scratch pad. Define each project-specific term in one or two sentences and list discouraged synonyms under `_Avoid_` when useful:

```md
# <Context Name>

<One or two sentences describing the context.>

## Language

**Order**:
<One or two sentence definition.>
_Avoid_: Purchase, transaction
```

Use one root `CONTEXT.md` unless a root `CONTEXT-MAP.md` identifies multiple contexts. In a multi-context repository, update the mapped context and record relationships in the map when needed.

## Record Durable Decisions

Offer to create an architecture decision record (ADR) only when the decision is all three:

1. Hard to reverse.
2. Surprising without context.
3. The result of a real trade-off.

Place ADRs in `docs/adr/` and increment the highest existing four-digit prefix. Keep the default format short:

```md
# <Short title>

<One to three sentences explaining the context, decision, and reason.>
```

Add status, considered options, or consequences only when they provide lasting value.
