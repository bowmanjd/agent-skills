---
name: golang-context
description: Propagate Go (Golang) context, timeouts, and metadata. Use when coordinating network APIs, database queries, and async lifecycles in Go.
---

# Go Context

Propagate cancellation, timeouts, and request metadata correctly.

## Rules

* Pass `ctx context.Context` as first parameter of functions.
* Never store context inside a struct field. Pass it explicitly.
* Never pass `nil` context. Use `context.TODO()` or `context.Background()`.
* Propagate same context through call chain: HTTP handler context -> service -> DB / external API calls.
* Always call `cancel()` (or `defer cancel()`) for `WithCancel`, `WithTimeout`, `WithDeadline`. Prevents context leaks.
* Use context values only for request-scoped metadata (request ID, trace context). Never for function arguments.
* Use unexported type for context value keys to prevent package collisions:
  ```go
  type ctxKey struct{}
  var key = ctxKey{}
  ```
* Use `context.WithoutCancel(ctx)` for background work that must outlive parent request lifecycle.

## Related Skills
* Use "golang-concurrency" skill if using context to cancel concurrent goroutine pipeline loops.
