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

## Dependencies

- Use the standard library or existing dependencies for small, straightforward tasks.
- Do not add a dependency for trivial functionality.
- Use established, maintained crates for substantial or error-prone functionality instead of reimplementing it.

## Performance and allocations

- Watch for unnecessary allocations, clones, copies, intermediate collections, and conversions. Remove them when the simpler alternative remains clear and idiomatic.
- Do not complicate code to optimize performance speculatively.
- Optimize when performance matters or the code is on a clear hot path.

## Unsafe Rust

- Avoid `unsafe` unless the task requires it.
- For non-trivial `unsafe` code, document the safety assumptions and invariants.
- Prefer a safe design when it is practical.

## Tests

- Add or update relevant tests when behavior changes.
- Test observable behavior rather than implementation details.
- Add tests when they cover meaningful behavior, not just to increase coverage or test count.
