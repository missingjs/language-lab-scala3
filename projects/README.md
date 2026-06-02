# Project-Based Learning Path

Scala 3 is excellent for project-driven learning, but the projects should be carefully sequenced. Each project should focus on one to three core skills.

Recommended progression:

```text
Scala 3 core
→ functional data modeling
→ error modeling
→ type classes
→ async / Future
→ effect system
→ HTTP / database
→ streaming
→ advanced type-level design
```

For the conceptual map behind these projects, see [../roadmap.md](../roadmap.md).

---

## The Sixteen Projects

A note on numbering: project 7 is a branch point — you commit to either Cats Effect or ZIO, and projects 8–11 each have an `a` (Cats Effect) and `b` (ZIO) variant. Projects 12–16 are shared and apply to both routes.

1. [CLI TODO Tool](01-cli-todo/README.md) — sbt, case class, enum, Option/Either, pattern matching.
2. [Order Validator](02-order-validator/README.md) — opaque types, typed errors, pure domain functions.
3. [Text Analyzer](03-text-analyzer/README.md) — Iterator, LazyList, foldLeft, pure transformations.
4. [Mini JSON Encoder Type Class](04-json-encoder/README.md) — given/using, summon, type classes, extension methods.
5. [Mini Parser Combinator](05-parser-combinator/README.md) — map/flatMap/for-comprehension, generic data, error modeling.
6. [Future-based URL Checker](06-future-url-checker/README.md) — Future, ExecutionContext, traverse, controlled parallelism.
7. [Choose an Effect System Route](07-effect-system-choice/README.md) — Cats Effect or ZIO; commit to one main route.
8. Effect-based CLI API Client — [a: Cats Effect](08a-ce-api-client/README.md) · [b: ZIO](08b-zio-api-client/README.md)
9. Bookmark REST API — [a: http4s](09a-ce-bookmark-api/README.md) · [b: ZIO HTTP](09b-zio-bookmark-api/README.md)
10. Database-backed Bookmark API — [a: Doobie](10a-ce-bookmark-db/README.md) · [b: ZIO/Quill](10b-zio-bookmark-db/README.md)
11. Streaming Log Processor — [a: fs2](11a-fs2-log-processor/README.md) · [b: ZStream](11b-zstream-log-processor/README.md)
12. [Background Job Queue](12-job-queue/README.md) — fibers, Queue, Ref, retry, structured concurrency.
13. [Cache or Rate Limiter](13-cache-or-rate-limiter/README.md) — Ref, atomic updates, time-dependent logic.
14. [Real-time Event Stream Service](14-event-stream-service/README.md) — PubSub, backpressure, client lifecycle.
15. [Typed Domain Service](15-typed-domain-service/README.md) — opaque types, state machines, illegal states unrepresentable.
16. [Mini Tagless Final App](16-tagless-final-app/README.md) — higher-kinded types, effect polymorphism, interpreters.

---

## Recommended Project Order

Full recommended sequence:

```text
1. CLI TODO Tool
2. Order Validator
3. Text Analyzer (Markdown / Log)
4. Mini JSON Encoder Type Class
5. Mini Parser Combinator
6. Future URL Checker
7. Choose Cats Effect or ZIO
8. Effect-based API Client
9. Bookmark REST API
10. Database-backed Bookmark API
11. Streaming Log Processor
12. Background Job Queue
13. Cache or Rate Limiter
14. Real-time Event Stream Service
15. Typed Domain Service
16. Mini Tagless Final App
```

Why this order works:

```text
language basics
→ domain modeling
→ collections and data transformation
→ type classes
→ functional composition
→ Future and async
→ effect system
→ HTTP and database
→ streaming
→ concurrency and shared state
→ advanced domain modeling
→ effect-polymorphic design
```

---

## If Time Is Limited

If you only do six projects, choose these:

```text
1. Order Validator
2. Mini JSON Encoder Type Class
3. Mini Parser Combinator
4. Future URL Checker
5. Bookmark REST API with Cats Effect or ZIO
6. Typed Domain Service
```

These cover the most important Scala 3 skills:

```text
type modeling
functional composition
given / using
for-comprehension
async and effect systems
HTTP backend development
typed errors
business domain modeling
```

---

## Three-Version Method for Each Project

For each project, build it in three passes.

### Version 1: Make it work

Implement the core feature first. Do not optimize for perfect abstraction.

### Version 2: Make it idiomatic Scala 3

Improve:

```text
case class and enum modeling
Option and Either usage
pattern matching
immutable data
pure core logic
separation of IO and business logic
```

### Version 3: Add advanced Scala features carefully

Depending on the project, add:

```text
opaque types
given / using
type classes
property-based testing
effect system
Resource or Scope
streaming
typed errors
```

The principle:

> Abstraction should grow from real needs, not from the desire to use advanced syntax.

---

## Skill Levels by Project Cluster

The Stage One through Stage Seven structure in [../roadmap.md](../roadmap.md) describes the **knowledge map**. The clusters below describe what skills you should have practiced after finishing the corresponding **projects**.

### Beginner Level: Projects 1 to 3

You should master:

```text
sbt
Scala 3 syntax
case class
enum
collections
Option / Either
pattern matching
basic testing
pure functions
```

### Intermediate Level: Projects 4 to 11

You should master:

```text
given / using
extension methods
type classes
map / flatMap
for-comprehension
Future
ExecutionContext
effect system basics
HTTP API
JSON
database access
```

### Advanced Level: Projects 12 to 16

You should master:

```text
fibers
Queue / Ref / Deferred / Promise
streaming
backpressure
resource safety
typed domain modeling
property-based testing
higher-kinded types
tagless final
performance and JVM awareness
```

---

## Projects to Avoid at the Beginning

These are valuable, but not ideal for early learning:

```text
complete microservice platform
complex Akka Cluster system
large Spark data platform
custom effect system
complex macro library
compiler implementation
large tagless-final architecture
distributed stream processing system
```

They combine too many difficult topics at once:

```text
JVM
concurrency
type system
build tools
dependency management
effect systems
databases
deployment
streaming
distributed systems
```

Early projects should be small and focused.

---

## Questions to Ask During Scala 3 Projects

For each project, ask:

```text
Can this domain be modeled more clearly with case class or enum?
Should this use Option, Either, or exception?
Can this error be modeled as a concrete type?
Should this String or Int be an opaque type?
Can this logic be a pure function?
Where is the side-effect boundary?
What does this for-comprehension expand into?
Is this given easy to discover, or does it pollute scope?
Is this type class really necessary?
Is Future enough here, or do I need IO / ZIO?
Are resources safely released?
Does concurrency support cancellation and timeout?
Is the abstraction helping, or just showing off?
```

---

## Advanced Scala 3 User Checklist

You are becoming an advanced Scala 3 user when you can:

```text
Model domains clearly with case classes and enums
Use Option and Either to represent absence and failure
Use pattern matching and for-comprehension fluently
Write immutable, composable, testable business logic
Understand given / using scope and resolution rules
Design simple and useful type classes
Use opaque types to avoid primitive obsession
Decide when Future is enough and when IO / ZIO is better
Manage resources, concurrency, cancellation, and errors safely
Organize sbt multi-module projects
Interop with Java libraries and JVM ecosystem safely
Read Cats Effect, ZIO, fs2, http4s, or ZIO HTTP code
Avoid excessive abstraction and type gymnastics
Think about thread pools, blocking, GC, performance, and observability
```
