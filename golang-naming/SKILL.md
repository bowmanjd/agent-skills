---
name: golang-naming
description: Go (Golang) naming conventions for packages, types, methods, receivers, and variables. Use when creating or refactoring identifiers in Go.
---

# Go Naming

Use clean, Go-idiomatic names. Casing controls visibility.

## Rules

* Exported names = `CamelCase`. Unexported = `camelCase`.
* Use `MixedCaps`. Never use underscores in variable or function names.
* Do not stutter package name:
  * `http.Client` (not `http.HTTPClient`)
  * `json.Decoder` (not `json.JSONDecoder`)
  * `user.New()` (not `user.NewUser()`)
* Interface name = method + `-er` suffix (`Reader`, `Closer`, `Stringer`).
* Constants = `MixedCaps` (`MaxRetries`), not `ALL_CAPS`.
* Receivers = 1-2 letters of type name. Never use `this` or `self`.
  * `func (s *Server) Start()`
* Error variables = `Err` prefix (`ErrNotFound`). Error types = `Error` suffix (`PathError`).
* Boolean fields/methods = `is`, `has`, `can` prefix:
  * `isConnected bool`, `IsConnected() bool`
* Acronyms = all uppercase or all lowercase. Never mixed:
  * `URL` (not `Url`), `HTTP` (not `Http`), `xmlParser` (not `xmlparser` or `XmlParser`).

## Related Skills
* Use "golang-code-style" skill for control flow structure and early error return layouts.
* Use "golang-structs-interfaces" skill for pointer receiver semantics and interface segregation.
