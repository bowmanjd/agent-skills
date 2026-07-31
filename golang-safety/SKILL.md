---
name: golang-safety
description: Prevent Go (Golang) runtime crashes, nil pointer panics, slice backing array sharing bugs, and resource accumulation. Use when reviewing Go code paths, initializing maps/slices, or casting types.
---

# Go Safety

Write correct, crash-free code.

## Rules

* Typed nil inside interface is NOT nil. Do not return typed nil pointers.
  * Bad: `var h *MyHandler; return h` (evaluates as non-nil interface)
  * Good: `if h == nil { return nil }`
* Nil maps panic on write. Always initialize before write:
  * `m := make(map[string]int)`
* Slices sharing backing array leak mutations on `append`. Use full slice expression or clone:
  * `b := a[:len(a):len(a)]` or `b := slices.Clone(a)`
* `defer` runs at function exit, not loop end. Do not use `defer` in loops. Extract loop body to function.
* Integer casts truncate silently (e.g. `int64` to `int32`). Check bounds:
  ```go
  if val > math.MaxInt32 || val < math.MinInt32 { return err }
  ```
* Do not compare floats with `==`. Use epsilon check:
  * `math.Abs(a - b) < 1e-9`
* Structs holding mutexes, waitgroups, or channels must not be copied. Pass by pointer.
* Return defensive copies of internal slices/maps:
  * `return slices.Clone(s.hosts)`

## Related Skills
* Use "golang-concurrency" skill for protecting shared struct state and maps.
* Use "golang-error-handling" skill if returning errors or handling nil interface errors.
