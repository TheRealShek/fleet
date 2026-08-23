---
name: articulate
description: Use only when User explicitly invokes $articulate to turn a rough thought into a simple, human-sounding comment or reply.
---

# Articulate

Turn the user's rough thought into a comment that feels native to X.

Use this skill only when User explicitly names `$articulate`. Never infer its use from an ordinary writing request.

## Approach

- Find the main point and preserve it.
- Keep the user's opinion, uncertainty, humour, and level of confidence.
- Fix only grammar that makes the meaning unclear. Do not polish away the user's voice.
- Respond to the context instead of merely repeating it.
- Do not invent facts, experiences, or stronger claims than the user supplied.
- If the thought has two plausible meanings, mention the assumption briefly and show both interpretations. Ask a question only when guessing could change the point.

## X Voice

- Write the next line of a conversation, not a complete explanation.
- Make it feel like self-talk said while scrolling.
- Prefer one thought and at most one reason. Stop early.
- Use lowercase when the user's draft is casual. Keep the correct casing for names such as Go, Rust, and AI.
- Fragments are fine. A final full stop is usually unnecessary.
- Keep commas and full stops sparse. A line break can carry the pause instead.
- Use contractions and simple words when they fit.
- Avoid semicolons, em dashes, formal transitions, summaries, and conclusion sentences.
- Avoid polished comparison templates such as "X is powerful, but Y offers a better trade-off".
- Avoid essay phrases such as "the real skill is", "this highlights", "it becomes a problem when", "the added complexity is not worth it", and "the key takeaway is".
- Personal phrasing such as "for me", "i'd still", "feels like", or "honestly" can make a thought natural. Use it only when true to the input.
- Do not manufacture slang, emojis, typos, or excitement. Mirror the user's energy.
- Keep every X option under 280 characters. For replies, aim for roughly 60 to 160 characters unless the thought genuinely needs more.

Before returning an option, read it once as speech. If it sounds like a paragraph, compress it again.

## Output

By default, provide:

1. **Best fit**: closest to the user's natural thought.
2. **Another way**: a different rhythm or angle, not synonym replacement.
3. **Shorter**: the point with almost everything else removed.

Return only the options, with no explanation of the edits. If the user requests one final comment, return only that comment.

## Examples

### Add nuance

Rough thought:

> ai makes debugging easy but people might stop thinking

Best fit:

> yeah AI makes debugging way faster but sometimes you stop thinking a little too early

Another way:

> AI is great for narrowing down a bug
>
> easy to forget you still need to understand why the fix worked

Shorter:

> AI makes debugging easier
>
> understanding the fix is still on you

### Give a useful compliment

Rough thought:

> nice project good work

Best fit:

> love how focused this is
>
> one small problem solved properly

Another way:

> this is actually useful
>
> nice work

Shorter:

> small focused and useful

### Disagree without sounding hostile

Rough thought:

> go better than rust for most backend no need complexity

Best fit:

> Rust is great but i'd still pick Go for most backend work
>
> less to think about and it usually gets the job done

Another way:

> for me most backends just don't need the extra control Rust gives you

Shorter:

> i'd still pick Go for most backends

### Express a half-formed observation

Rough thought:

> people say ai killed curiosity but now i can ask dumb questions without bothering anyone

Best fit:

> people say AI killed curiosity but for me it's been the opposite
>
> i can ask the dumb question and keep digging without feeling like i'm bothering someone

Another way:

> honestly AI made me more curious
>
> there's no hesitation around asking the really basic question anymore

Shorter:

> AI didn't kill my curiosity
>
> it made asking easier

### Add something to the conversation

Original post:

> We replaced our queue with Kafka and throughput went up 10x

Rough thought:

> kafka can work but was simpler queue even failing because lot of ops cost

Best fit:

> Kafka makes sense at that scale but i'd still want to know what the simpler queue was failing at
>
> otherwise that's a lot of ops to take on

Another way:

> curious what broke with the old queue
>
> Kafka is a lot to own if throughput was the only problem

Shorter:

> what was the simpler queue failing at though
