---
name: golang-modernize
description: Modernize Go (Golang) code with latest language features and standard packages (Go 1.21 - 1.26). Use when updating Go syntax or using new library helpers.
---

# Go Modernize

Target modern Go (Go 1.21 - 1.26). Do not write old Go.

## Rules

* Use `any`. Never `interface{}`.
* Use `math/rand/v2`. Never use old `math/rand`. No seed needed.
* Use builtin `min` / `max`. Do not write manual loops or conditions.
* Use standard packages `slices`, `maps`, `cmp`.
  * `slices.Sort(s)`, `slices.Clone(s)`
  * `maps.Keys(m)`, `maps.Values(m)`
  * `cmp.Or(a, b)` (returns first non-zero)
* Loop variables safe in Go 1.22+. Do not write `v := v` shadow inside loop.
* Use `range` over integer for counting:
  ```go
  for i := range 10 { ... }
  ```
* Use `errors.AsType[T](err)` (Go 1.26+) for type assertion check:
  ```go
  if myErr, ok := errors.AsType[*MyError](err); ok { ... }
  ```
* Use `sync.WaitGroup.Go` (Go 1.25+) to launch waitgroup goroutines:
  ```go
  var wg sync.WaitGroup
  wg.Go(func() { ... })
  ```
* Use `os.Root` (Go 1.24+) to jail paths. Prevents directory traversal.
* Use `testing.B.Loop` (Go 1.24+) in benchmarks:
  ```go
  for b.Loop() { ... }
  ```
* Use `t.Context()` (Go 1.24+) for test cancellation context.
* Use range-over-function iterators (Go 1.23+). Return `iter.Seq[V]` or `iter.Seq2[K,V]` instead of allocating slices for iteration:
  ```go
  func (s *Store) All() iter.Seq2[string, Item] { ... }
  ```
  Use `slices.Collect(seq)` to materialize when slice is needed.
* Use `new(expr)` (Go 1.26+) for pointer-to-literal. No helper functions needed:
  ```go
  cfg := &Config{Timeout: new(5 * time.Second)}
  ```
* Run `go fix ./...` to auto-apply modernizers (Go 1.26+). Suggest to user when upgrading Go versions.

## Related Skills
* Use "golang-concurrency" skill if writing concurrent loops or using goroutines.
* Use "golang-testing" skill if writing unit tests, fuzz tests, or benchmarks.
* Use "golang-error-handling" skill if handling, wrapping, or returning errors.
