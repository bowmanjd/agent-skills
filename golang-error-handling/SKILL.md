---
name: golang-error-handling
description: Idiomatic Go (Golang) error handling, wrapping, sentinels, type assertions, and logging. Use when creating, wrapping, or checking errors in Go.
---

# Go Error Handling

Write clean error flows.

## Rules

* Check all returned errors. Never discard with `_`.
* Wrap errors with context:
  * `fmt.Errorf("do action: %w", err)`
* Use `%w` for internal errors. Use `%v` at system boundary to hide internal chains.
* Error strings: start lowercase, no trailing punctuation. They get prefixed by callers.
  * `"load config: %w"` (not `"Failed to load config."`)
* Check sentinels using `errors.Is`:
  * `if errors.Is(err, ErrNotFound) { ... }`
* Check error types using `errors.AsType[T]` (Go 1.26+):
  * `if myErr, ok := errors.AsType[*MyError](err); ok { ... }`
* Log OR return. Never both. Dual handling creates duplicate logs.
* Panic only for unrecoverable bugs (like nil pointer invariant breach). Never for expected runtime errors.

## Related Skills
* Use "golang-safety" skill if comparing interface error variables or preventing runtime panics.
* Use "golang-naming" skill for naming custom error types and sentinel variables.
