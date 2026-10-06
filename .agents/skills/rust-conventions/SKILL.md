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
- Write brief doc comments for most functions and structs, and for methods that need explanation. State their purpose or important behavior without restating the code or writing an essay.

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

- Use [kache](https://github.com/kunobi-ninja/kache) for Rust builds to reuse compiler outputs across projects and worktrees and reduce disk space used by duplicate build artifacts.
- Follow kache's current setup documentation and preserve existing Cargo compiler-wrapper configuration. Verify the setup with `kache doctor` before relying on the cache.

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
