---
name: golang-code-style
description: Clean, readable Go (Golang) layout, nesting reduction, early return patterns, and slice instantiation rules. Use when structuring Go functions and control flow.
---

# Go Code Style

Write readable, simple, and flat Go code.

## Rules

* Keep happy path flat. Return errors and edge cases early (early return).
  ```go
  if err != nil {
      return err
  }
  // happy path continues flat here
  ```
* Drop `else` if `if` block ends with `return`, `break`, or `continue`.
* Extract complex `if` conditions (3+ operands) to named boolean variables.
* Keep function parameter count <= 4. Group parameters into structs (e.g. options struct) if more are needed.
* Initialize struct literals using field names. Positional initialization breaks when fields change.
  ```go
  // Good
  srv := &Server{Addr: ":8080"}
  ```
* Initialize empty slices explicitly to prevent `null` in JSON serialization:
  * `s := []T{}` (not `var s []T` if it will be serialized to JSON empty `[]`).
* Preallocate slice capacity when size is known:
  * `s := make([]T, 0, len(items))`

## Related Skills
* Use "golang-naming" skill for formatting package names, variables, and struct fields.
* Use "golang-structs-interfaces" skill for embedding composition layouts and receiver pointer structures.
