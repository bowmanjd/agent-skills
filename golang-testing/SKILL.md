---
name: golang-testing
description: Go (Golang) table-driven tests, parallel execution, fuzzing, examples, and goroutine leak detection. Use when writing Go unit or integration tests.
---

# Go Testing

Write fast, parallel, and reliable tests.

## Rules

* Use table-driven tests for multiple scenarios. Always name cases and run with `t.Run`.
* Call `t.Parallel()` in both top-level tests and subtests.
* Separate integration tests using build tags:
  * `//go:build integration` at top of file.
* Mock interfaces, not concrete structs.
* Use `go.uber.org/goleak` in `TestMain` to check for goroutine leaks:
  ```go
  func TestMain(m *testing.M) {
      goleak.VerifyTestMain(m)
  }
  ```
* Write executable Examples as verified docs:
  ```go
  func ExampleAdd() {
      fmt.Println(Add(1, 2))
      // Output: 3
  }
  ```
* For concurrent time-based tests in Go 1.25+, use `synctest.Test` to synthetic-advance time instantly:
  ```go
  synctest.Test(t, func(t *testing.T) {
      time.Sleep(5 * time.Second) // synthetic time advances instantly
  })
  ```
* Write fuzz tests for parsing and validation functions:
  ```go
  func FuzzParseInput(f *testing.F) {
      f.Add("seed input")
      f.Fuzz(func(t *testing.T, data string) { ... })
  }
  ```
* Use `t.Context()` (Go 1.24+) instead of manually creating test contexts.

## Related Skills
* Use "golang-concurrency" skill if checking for active goroutine leaks or channel deadlocks during tests.
