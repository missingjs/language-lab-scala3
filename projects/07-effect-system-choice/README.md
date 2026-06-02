[← Back to projects](../README.md)

# Project 7: Choose an Effect System Route

This is a decision point, not a coding project. After Project 6, choose one main effect system route and stick with it for projects 8 through 11.

```text
Route A: Cats Effect / Typelevel
Route B: ZIO
```

Do not try to master both at the same time in the beginning. Each ecosystem has its own idioms, libraries, and mental model — splitting attention early slows both down.

## Route A: Cats Effect / Typelevel

Common stack:

```text
Cats Effect
http4s
fs2
doobie
circe
skunk
tapir
```

Characteristics:

```text
highly functional
type-safe
very composable
steeper learning curve
```

Core idea:

```text
Describe effects as values, then let a runtime execute them.
```

If you choose Route A, the next four projects are:

- [Project 8a: Cats Effect CLI API Client](../08a-ce-api-client/README.md)
- [Project 9a: http4s Bookmark API](../09a-ce-bookmark-api/README.md)
- [Project 10a: Doobie Bookmark DB API](../10a-ce-bookmark-db/README.md)
- [Project 11a: fs2 Streaming Log Processor](../11a-fs2-log-processor/README.md)

---

## Route B: ZIO

Common stack:

```text
ZIO
ZIO HTTP
ZIO JSON
ZIO Config
ZIO Test
Quill
```

Characteristics:

```text
integrated ecosystem
typed errors
environment-based dependency management
strong consistency within the ecosystem
```

Type signature:

```scala
ZIO[R, E, A]   // requires R, may fail with E, succeeds with A
```

If you choose Route B, the next four projects are:

- [Project 8b: ZIO CLI API Client](../08b-zio-api-client/README.md)
- [Project 9b: ZIO HTTP Bookmark API](../09b-zio-bookmark-api/README.md)
- [Project 10b: ZIO Database-backed API](../10b-zio-bookmark-db/README.md)
- [Project 11b: ZStream Log Processor](../11b-zstream-log-processor/README.md)

---

## How to Choose

Both routes can build the same kinds of systems. Useful tiebreakers:

```text
Pick Cats Effect if you value composable type classes, tagless final, and the broader Typelevel ecosystem.
Pick ZIO if you value typed errors in the result type, ZLayer-based dependency injection, and a tightly integrated ecosystem.
```

Whichever you pick, projects 12 through 16 are shared and can be built on top of the route you chose.
