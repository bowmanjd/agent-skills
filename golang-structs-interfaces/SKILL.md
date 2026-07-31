---
name: golang-structs-interfaces
description: Go (Golang) struct and interface design rules, pointer vs value receivers, tags, and type assertions. Use when designing types or writing interface APIs in Go.
---

# Go Structs & Interfaces

Design clean, composition-based Go types.

## Rules

* Accept interfaces, return concrete structs:
  * `func NewService(store Store) *Service`
* Keep interfaces small (1-3 methods). Compose large interfaces from small ones:
  * `type ReadWriter interface { Reader; Writer }`
* Define interfaces in consumer package, not implementer package.
* Do not make interfaces prematurely. Start with concrete types. Extract interface only when second implementation or mock is needed.
* Receiver consistency: if any method of a type uses pointer receiver, all methods of that type must use pointer receiver.
* Tag all exported fields in serialized structs:
  * `ID string `json:"id"``
* Verify interface implementation at compile time:
  * `var _ io.Reader = (*MyBuffer)(nil)`
* Always use comma-ok for type assertions to prevent panics:
  * `s, ok := val.(string)` (never `s := val.(string)`)
* Do not over-use generics. Start with concrete types. Use generics only when logic repeats identically across multiple types.
* Use functional options for constructors with many optional params:
  ```go
  func NewServer(addr string, opts ...Option) *Server
  ```

## Related Skills
* Use "golang-naming" skill for struct constructor, interface, and acronym naming conventions.
* Use "golang-code-style" skill for parameter counting rules and struct instantiation formats.
