---
name: golang-concurrency
description: Go (Golang) concurrency, goroutine lifecycles, maps, channels, and errgroups. Use when writing concurrent Go code, spawning goroutines, or utilizing synchronization primitives.
---

# Go Concurrency

Write thread-safe, leak-free concurrent code.

## Rules

* Goroutines must have exit path (context or done channel). Never let goroutines block forever.
* Always select on context cancellation in loops/channels:
  ```go
  select {
  case <-ctx.Done():
      return ctx.Err()
  case ch <- data:
  }
  ```
* Maps are not thread-safe. Concurrent read/write crashes program. Use `sync.Mutex`, `sync.RWMutex`, or `sync.Map`.
* Only sender closes channel. Receiver closing causes panic.
* Default to unbuffered channels. Buffered channels hide backpressure.
* Do not call `time.After` in hot loops. It allocates timers. Use `time.NewTimer` and `Reset()`.
* Use `errgroup` for parallel work that returns errors:
  ```go
  g, ctx := errgroup.WithContext(ctx)
  g.SetLimit(10) // bounds worker count
  g.Go(func() error { ... })
  ```
* Send copies, not pointers, over channels. Pointers create concurrent shared memory.

## Related Skills
* Use "golang-context" skill if managing context cancellations, timeouts, or propagating spans.
* Use "golang-safety" skill if debugging concurrent map race crashes or struct copying.
