---
name: rust-conventions
description: Apply these Rust conventions when writing, reviewing, or changing Rust code.
---

# Rust conventions

Write idiomatic Rust that fits the codebase and is easy to understand.

Follow repository instructions when they conflict with these conventions.

## Error handling

- Use typed errors, often with `thiserror`, in libraries and reusable modules.
- Use `anyhow` at application boundaries when callers do not need to inspect specific error variants.
- Avoid `unwrap()` and `expect()` in production code paths. They are fine in tests or when a failure is impossible because of a clear invariant.

## Ownership and borrowing

- Borrow with `&T` or `&mut T` when the function does not need to take ownership.
- Do not add `.clone()` only to satisfy the borrow checker. Understand the ownership issue and fix the design when possible.
- Prefer code that uses ownership efficiently, as long as it stays clear and idiomatic.

## Abstractions

- Prefer a concrete, simple implementation.
- Add traits, generics, or other abstractions when they solve a current problem, make the code simpler, or support a credible near-term need.
- Do not add abstractions for hypothetical flexibility.

## Readability

- Prefer direct code over clever shortcuts.
- Keep code idiomatic, including when an explicit implementation is easier to follow.
- Use a loop or named intermediate values when they make an iterator or combinator chain easier to understand.
- Avoid needless type complexity and indirection.
- Separate logical steps with blank lines so each block carries one idea. Keep related statements together, and put setup, the main step, and cleanup apart from each other.
- Split a function when it mixes distinct jobs or when a reader needs the signature to recall what the body does. Prefer a few focused functions over one long one.

## Comments

- Write for a reader who is new to the file: someone going top to bottom should finish knowing what each part does and how the parts fit, without opening other docs.
- Give each module a short `//!` doc stating what it owns, what it does not own, and how its main pieces fit together.
- Write `///` doc comments for public items and private items whose behavior is not obvious from the signature. State purpose, important behavior, panics, and how the item connects to the code around it.
- Comment inline to explain what the code cannot say on its own: reasons for non-obvious choices, invariants across functions, failure or fallback behavior, lifetime assumptions, blocking or async flow, and brief signposts above dense sections saying what the section accomplishes before the reader goes line by line.
- Say why it exists and why not the alternative when a tradeoff was made, so the next reader does not re-litigate it.
- Keep comments short by default: one to three lines for a doc comment, one to two inline, up to four for a module doc. Treat these as defaults, not ceilings; go longer when flow, invariants, or domain meaning genuinely need it. Stay dense: more meaning, not more words.
- Do not parrot the code. A brief comment that orients the reader is valuable; one that repeats a line with no added information is noise. Delete it before handing off.

## Modules and crate layout

- Organize modules around a clear responsibility, not one file per function. Keep related types and functions together. Split a file when it contains distinct responsibilities or when moving a cohesive part into its own module makes the code easier to navigate.
- Prefer `foo.rs` with `foo/bar.rs` for child modules instead of `foo/mod.rs` in new code. Follow the repository's existing layout.
- Keep implementation modules private when callers do not need them. Use `pub use` when it gives callers a clearer public path.
- Use `pub(crate)` for items shared within a crate that should not be part of its public API.
- Put reusable code in `src/lib.rs` when a binary or integration tests need it. Keep `src/main.rs` focused on starting the application and donot bloat the file.

## Dependencies

- Use the standard library or existing dependencies for small, straightforward tasks.
- Do not add a dependency for trivial functionality.
- Use established, maintained crates for substantial or error-prone functionality instead of reimplementing it.

## Performance and allocations

- Watch for unnecessary allocations, clones, copies, intermediate collections, and conversions. Remove them when the simpler alternative remains clear and idiomatic.
- Do not complicate code to optimize performance speculatively.
- Optimize when performance matters or the code is on a clear hot path.

## Build cache and disk space

- Preserve and use the existing Cargo compiler-wrapper and build-cache configuration. Ordinary Rust edits do not require cache setup.
- Consider [kache](https://github.com/kunobi-ninja/kache) when the user requests cache setup or the task concerns build performance or duplicate build artifacts. Follow its current setup documentation, preserve existing wrapper configuration, and verify with `kache doctor` before relying on a new setup.

## Unsafe Rust

- Avoid `unsafe` unless the task requires it.
- For non-trivial `unsafe` code, document the safety assumptions and invariants.
- Prefer a safe design when it is practical.

## Tests

- Add or update relevant tests when behavior changes.
- Test observable behavior rather than implementation details.
- Add tests when they cover meaningful behavior, not just to increase coverage or test count.

## Final check

- After writing or changing Rust code, review the final diff against every applicable rule in this skill before handing it off. Fix violations and explain any rule that could not be followed.
