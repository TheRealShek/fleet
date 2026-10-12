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
- Use explicit version prefixes such as `/v1` and `/v2` for all HTTP endpoints, including health, metrics, and admin routes.
- Add a dependency only when its value justifies the cost.

## Readability and comments

- Prefer direct code over clever shortcuts.
- Choose concise names that describe actual roles and behavior at the call site; use consistent names for related operations and distinguish meaningful differences.
- Prefer readable structure over fewer lines; do not compress code at the cost of clarity.
- Keep each function's flow easy to follow. Extract cohesive details into named helpers when they obscure that flow. Keep error handling and resource ownership visible in the caller.
- Define HTTP handlers as separate named functions or methods; keep route registration focused on mapping paths to handlers.
- Give every exported identifier a concise doc comment starting with its name.
- Comment unexported functions only when their purpose or reasoning is not obvious.
- Inline comments explain why code chose an approach, what invariant must hold, what happens on failure, and how requests move between components.
- When code wraps or forwards requests with `http.HandlerFunc`, `ReverseProxy`, request clones, or response flushers, write comments that state where the request enters, what changes it, and which target receives it next.
- Explain naming objections in one line and let the user decide.

## Tests and checks

- Add or update relevant tests when behavior changes. Test observable behavior and important failures.
- Put one brief comment above each test function describing what it tests. Do not add comments inside test bodies or individual table-driven cases. Use clear names for cases and subtests.
- For concurrency, verify cancellation, shutdown, and bounded resource use.
- Run `gofmt -w` on every Go file you write or change.
- Then run `wsl` on the affected packages to check whitespace grouping.
- Use the repository's tool versions, settings, and `golangci-lint` integration when available.
- Fix `wsl` findings in the changed code. Review automatic fixes and keep edits within scope.
- After whitespace fixes, rerun `gofmt -w`, then `wsl`. Skip this repeat if nothing changed.
- Before handing off, confirm `gofmt -l` lists no changed files and the whitespace check passes.
- For read-only reviews, check without applying fixes.
- Run narrow checks first, then broaden when needed.
- If the repo has CI, confirm it runs gofmt, go vet ./..., staticcheck ./..., and go test -race ./.... Don't add or change CI unless asked.
- Report checks that failed or could not run. Do not claim verification from inspecting code alone.

## Configuration

- Do not hardcode deployment-specific values such as addresses, ports, timeouts, limits, upstream URLs, or feature flags.
- Load configuration once at startup, preferably from environment variables, validate it, and pass typed values to the code that needs them.
- Keep configuration access out of application logic. Do not scatter `os.Getenv` calls across packages.
- Hardcode only true program constants whose value is part of the program's behavior.

## Final check

- After writing or changing Go code, review the final diff against every applicable rule in this skill before handing it off. Fix violations and explain any rule that could not be followed.
