---
name: go-conventions
description: Apply these Go conventions when writing, reviewing, or changing Go code.
---

# Go conventions

Write idiomatic Go that fits the codebase and is easy to understand.

Follow repository instructions when they conflict with these conventions.

## Packages and file layout

- Give each package one job. Name it for what it owns, never `util`, `common`, or `helpers`.
- Keep related types and functions together. Split files by concept, not length.
- Keep `main` thin. Put application setup, execution, and cleanup in a `run(ctx context.Context) error` function. Keep process signals and exit status in `main`.

## Abstractions

- Prefer a concrete, simple implementation.
- Define interfaces in the consuming package, with one or two methods. Avoid speculative interfaces.
- Prefer three duplicated lines to a vaguely named helper. Refactor only on the fourth truly identical repeat.

## Context and concurrency

- Put `context.Context` first in function parameters, never in a struct.
- Do not write helpers that hide context creation or cancellation ownership. When deriving a context, make its lifetime and responsibility for calling the cancel function explicit.
- Every goroutine must have an owner that stops it and waits for it to finish.

## Error handling and logging

- Return errors with useful operation and resource context. Preserve the cause with `%w`, for example `fmt.Errorf("fetch key %s from backend %s: %w", keyID, backend, err)`.
- Never include secrets in error messages, log messages, or structured log fields.
- Use `errors.Is` and `errors.As` to inspect errors, never string matching.
- Do not log and return the same error. Log at the boundary that handles it.
- Best-effort cleanup and non-fatal background work may log and continue when ignoring the failure is intentional and safe.
- Use `log/slog` for structured logging.

## Dependencies and HTTP

- Prefer the standard library and existing dependencies for straightforward tasks.
- Prefer `net/http` before adding `chi` or another HTTP router.
- Add a dependency only when its value justifies the cost.

## Readability and comments

- Prefer direct code over clever shortcuts.
- Give every exported identifier a concise doc comment starting with its name.
- Comment unexported functions only when their purpose or reasoning is not obvious.
- Inline comments should explain why an approach was chosen, what invariant must hold, or what happens on failure. Do not restate the code or teach basic Go mechanisms in comments.
- Explain naming objections in one line and let the user decide.

## Tests and checks

- Add or update relevant tests when behavior changes. Test observable behavior and important failures.
- Put one brief comment above each test function describing what it tests. Do not add comments inside test bodies or individual table-driven cases. Use clear names for cases and subtests.
- For concurrency, verify cancellation, shutdown, and bounded resource use.
- Check `gofmt` formatting and run narrow checks first, then broaden when needed.
- If the repo has CI, confirm it runs gofmt, go vet ./..., staticcheck ./..., and go test -race ./.... Don't add or change CI unless asked.
- Report checks that failed or could not run. Do not claim verification from inspecting code alone.

## Final check

- After writing or changing Go code, review the final diff against every applicable rule in this skill before handing it off. Fix violations and explain any rule that could not be followed.
