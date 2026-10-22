---
name: go-conventions
description: Apply these Go conventions when writing, reviewing, or changing Go code.
---

# Go conventions

Write clear, idiomatic Go. Repository instructions take precedence.

## Structure

- Give each package one job and a specific name, never `util`, `common`, or `helpers`. Keep related types and functions together; split files by concept, not length.
- Put setup, execution, and cleanup in `run(ctx context.Context) error`. Keep `main` focused on process signals and exit status.
- Prefer concrete implementations. Define small interfaces in the consuming package, usually with one or two methods, only for current needs. Prefer duplication to a vague helper; extract repeated logic on the fourth truly identical occurrence.

## Ownership and errors

- Put `context.Context` first, never in a struct. Keep context creation, lifetime, and cancellation ownership explicit, including through helpers.
- Every goroutine needs an owner that stops it and waits for it to finish. Keep error handling and resource ownership visible in the caller.
- Give errors operation and resource context, wrap causes with `%w`, and inspect them with `errors.Is` or `errors.As`, never string matching. Keep secrets out of errors and logs.
- Use shared sentinel errors when callers need to recognize a failure, and typed errors when they also need structured details. Repeated wording alone does not justify a type.
- Use `log/slog` for structured logging. Log at the boundary handling the error; do not both log and return it. Best-effort cleanup and non-fatal background work may log and continue when safe and intentional.

## HTTP and configuration

- Prefer the standard library and existing dependencies, including `net/http`. Add dependencies only when their value justifies the cost.
- Use named handler functions or methods; keep route registration focused on mapping paths to handlers. Version all endpoints, including health, metrics, and admin routes, with prefixes such as `/v1`.
- Load and validate configuration once at startup, preferably from environment variables, then pass typed values. Keep `os.Getenv` and other configuration access out of application logic.
- Configure deployment-specific addresses, ports, timeouts, limits, upstream URLs, and feature flags. Hardcode only true program constants.

## Readability and comments

- Use direct code, clear control flow, and concise names that describe roles at the call site. Keep related names consistent and meaningful differences visible. Extract cohesive details when they obscure the flow. Explain naming objections in one line and let the user decide.
- Aim for lines around 100 columns without fighting `gofmt` or sacrificing clarity. Use a named options struct and named fields when related arguments make signatures long or positional calls hard to read. Keep context separate and first; do not add a struct solely for line length.
- Give exported identifiers concise doc comments starting with their names. Comment private functions only when unclear. Inline comments explain reasons, invariants, failure behavior, and request flow.
- For request wrappers and forwarding through `http.HandlerFunc`, `ReverseProxy`, clones, or flushers, comment where the request enters, what changes, and which target receives it next.

## Verification

- Match unit test files to their primary source file. Put all unit tests for `abc.go` in `abc_test.go`, including success, failure, boundary, and concurrency cases. Do not scatter those tests across files named after scenarios or subfeatures, such as `abc_errors_test.go` or `abc_limits_test.go`. Each unit test file should have one primary source file under test; using dependencies or test doubles does not change that ownership.
- Keep integration tests that exercise several components together in `<flow>_integration_test.go`, with one file per complete flow, such as `auth_integration_test.go`. Group them by the behavior they verify rather than forcing them into one source file's unit tests. Using a real database or HTTP server alone does not make a focused source-file test an integration flow.
- Keep test fixtures and helpers with the tests that own them. Shared helpers may be used across test files in the same package; do not create separate helper files for individual scenarios or dependencies. Preserve required splits for build constraints or Go package boundaries, and explain any other exception.
- Before finishing test changes, check the affected package for unit tests scattered outside their matching source-file test. When reorganizing tests, preserve coverage and behavior, avoid unrelated changes, and run the affected tests.
- Test changed behavior and important failures. For concurrency, cover cancellation, shutdown, and bounded resource use. Start with narrow checks.
- Put one brief description above each test function. Use clear case and subtest names; avoid comments inside test bodies or table-driven cases.
- Run `gofmt -w` on changed Go files, then `wsl` on affected packages using repository versions, settings, and `golangci-lint` integration when available. Fix findings within scope and inspect automatic fixes. If fixes change code, repeat both checks. Confirm `gofmt -l` lists no changed files and `wsl` passes. Read-only reviews must not apply fixes.
- If CI exists, inspect whether it runs `gofmt`, `go vet ./...`, `staticcheck ./...`, and `go test -race ./...`. Do not change CI unless asked. Report failed or unavailable checks; inspection alone is not verification.

Review the final diff against these rules. Fix violations and explain any rule you could not follow.
