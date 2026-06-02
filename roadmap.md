# Scala 3 Learning Roadmap

A roadmap for learners who want to grow from Scala 3 beginners into advanced, production-capable Scala developers.

Scala 3 is different from Go and Elixir. Go emphasizes simplicity, engineering discipline, concurrency, and production services. Elixir emphasizes OTP, lightweight processes, fault tolerance, and distributed systems. Scala 3 emphasizes:

> Type systems, functional programming, JVM engineering, and abstraction design.

The key to learning Scala 3 well is not to rush into advanced abstractions too early. Learn to write clear Scala first, then functional Scala, and only then highly abstract Scala.

This roadmap is the knowledge map: what to learn and in what order. For the project sequence that turns these concepts into practical engineering skill, see [projects/README.md](projects/README.md).

---

## 1. Understand Scala 3's Positioning

Scala 3 can be understood as three layers:

```text
Layer 1: Better Java
Layer 2: Functional Programming Language
Layer 3: Type-level Abstraction Language
```

A healthy learning path is:

```text
Write clear Scala
→ Write functional Scala
→ Write abstract and type-safe Scala
```

Avoid starting with Cats, ZIO, tagless final, higher-kinded types, or advanced type-level programming before you are comfortable with the language fundamentals.

---

## 2. Stage One: Master Scala 3 Syntax and Data Modeling

The first stage is becoming fluent in Scala 3 as an expression-oriented language with strong data modeling primitives. Before reaching for functional or type-level abstractions, you should be comfortable describing your domain with case classes, enums, and pattern matching, and processing data with the standard collection library.

### 2.1 Scala 3 Syntax and Expression-oriented Programming

Start with the core language:

```text
val
var
def
if expressions
for expressions
match expressions
indentation syntax
```

Scala is expression-oriented. Many constructs return values:

```scala
val result =
  if score >= 60 then "pass" else "fail"
```

This is different from Java or Go, where many constructs are primarily statements.

#### What to learn

- `val` versus `var`
- Method definitions with `def`
- Indentation-based syntax
- Expressions versus statements
- Type inference
- When to write explicit type annotations

Use explicit types especially for:

```text
public APIs
complex return types
effect types
recursive functions
module boundaries
```

---

### 2.2 Data Modeling with Case Classes and Enums

#### Case Classes

`case class` is the core tool for immutable data modeling:

```scala
case class User(id: UserId, email: Email, age: Int)
```

You should understand:

```text
immutability
copy
automatic equals / hashCode / toString
pattern matching
companion objects
```

Example:

```scala
val updated = user.copy(email = newEmail)
```

#### Enums

Scala 3 enums are very useful for modeling finite states and algebraic data types:

```scala
enum PaymentStatus:
  case Pending
  case Paid
  case Failed(reason: String)
```

Use enums for:

```text
states
commands
events
errors
finite choices
```

Avoid using raw strings or integers for domain states when an enum would be clearer and safer.

---

### 2.3 Pattern Matching

Pattern matching is central to Scala:

```scala
status match
  case PaymentStatus.Pending =>
    "waiting"
  case PaymentStatus.Paid =>
    "done"
  case PaymentStatus.Failed(reason) =>
    s"failed: $reason"
```

Learn:

```text
case class matching
enum matching
tuple matching
guards
sealed hierarchy matching
exhaustiveness checking
```

Good Scala code often combines type modeling with pattern matching to reduce illegal states and unclear branching logic.

---

### 2.4 Collections and Data Transformation

Scala's collection library is powerful. Learn these types early:

```text
List
Vector
Seq
Map
Set
Option
Either
Try
Iterator
LazyList
```

Core operations:

```text
map
flatMap
filter
foldLeft
collect
partition
groupBy
```

Example:

```scala
val emails =
  users
    .filter(_.active)
    .map(_.email)
```

Learn the difference between:

```text
map      transforms values inside a structure
flatMap  transforms and flattens nested structure
fold     aggregates many values into one result
```

---

## 3. Stage Two: Functional Programming Foundations

Once you can model data, the next stage is composing it. This is where Scala starts to feel different from "Java with better syntax": errors are values, transformations are pipelines, and `for` is a sequencing operator over many shapes.

### 3.1 Option, Either, and Typed Errors

#### Option

Use `Option[A]` to represent a value that may be absent:

```scala
def findUser(id: UserId): Option[User]
```

Avoid `null` in Scala code.

#### Either

Use `Either[E, A]` to represent a computation that may fail:

```scala
def parseEmail(raw: String): Either[ValidationError, Email]
```

Prefer domain-specific errors:

```scala
enum ValidationError:
  case EmptyEmail
  case InvalidEmailFormat
```

Then:

```scala
def parseEmail(raw: String): Either[ValidationError, Email]
```

This makes error handling explicit, composable, and testable.

#### Try

Use `Try[A]` mainly when working with exception-throwing APIs, especially Java APIs.

Suggested usage:

```text
Missing value: Option[A]
Business validation failure: Either[DomainError, A]
Exception-based computation: Try[A] or convert to Either
```

---

### 3.2 Functional Programming Foundations

You do not need to become a category theory expert to write good Scala, but you do need functional fundamentals.

#### Pure Functions

A pure function:

```text
returns the same output for the same input
has no side effects
```

Example:

```scala
def totalPrice(items: List[Item]): BigDecimal =
  items.map(_.price).sum
```

Try to keep core business logic pure, and push side effects to the boundary.

#### Immutability

Prefer:

```text
val
case class
List
Vector
Map
copy
```

Avoid overusing:

```text
var
mutable.Map
ArrayBuffer
null
```

Immutability makes code easier to reason about, test, and run safely in concurrent contexts.

#### Higher-order Functions

Functions can be passed as values:

```scala
def transform[A, B](values: List[A])(f: A => B): List[B] =
  values.map(f)
```

This is the foundation of many Scala abstractions.

---

### 3.3 For-comprehension

Scala's `for` is not just a loop. It is syntax over `map`, `flatMap`, and `withFilter`.

Example:

```scala
val result =
  for
    user <- findUser(userId)
    account <- findAccount(user.accountId)
  yield account.balance
```

You must understand how this expands. It will help you later with:

```text
Option
Either
Future
IO
ZIO
Parser
Stream
```

---

## 4. Stage Three: Object Composition and Extensions

Scala is also an object-oriented language. This stage covers the parts of the language that organize code rather than transform values: traits, classes, composition, and extension methods. Treat these as tools for shaping module boundaries, not as a separate paradigm to fight against the functional core.

### 4.1 Object-oriented Scala and Composition

Scala supports object-oriented programming, but idiomatic Scala often favors composition over inheritance.

Learn:

```text
class
trait
object
companion object
abstract class
constructor
```

Example:

```scala
trait UserRepository:
  def find(id: UserId): Option[User]

final class UserService(repo: UserRepository)
```

Recommended modeling style:

```text
Use case class for data
Use enum for finite states
Use trait for capability boundaries
Use class to compose dependencies
Avoid deep inheritance trees
```

---

### 4.2 Extension Methods

Scala 3 extension methods let you add methods to existing types:

```scala
extension (s: String)
  def isEmail: Boolean =
    s.contains("@")
```

They are useful for:

```text
domain-specific convenience methods
syntax improvements
type class syntax
small DSLs
```

Use them carefully. Too many extension methods can make code harder to understand because method origins become less obvious.

---

## 5. Stage Four: Contextual Abstractions, Type Classes, and Domain Modeling

This stage is the transition from intermediate to advanced Scala 3. `given`/`using`, type classes, and opaque types are the tools you reach for when you want to express invariants in the type system rather than enforce them with runtime checks.

### 5.1 Contextual Abstractions: given and using

Scala 3 replaces many Scala 2 implicit patterns with clearer `given` and `using` syntax.

Example:

```scala
def greet(name: String)(using prefix: String): String =
  s"$prefix $name"

given String = "Hello"

greet("Alice")
```

Learn:

```text
context parameters
given instances
summon
scope resolution
implicit search rules
how to avoid given pollution
```

This is one of the key transitions from intermediate to advanced Scala 3.

---

### 5.2 Type Classes

A type class defines behavior for a type without requiring that type to inherit from an interface.

Example:

```scala
trait JsonEncoder[A]:
  def encode(value: A): String

given JsonEncoder[User] with
  def encode(user: User): String =
    s"""{"email":"${user.email}"}"""

def toJson[A](value: A)(using encoder: JsonEncoder[A]): String =
  encoder.encode(value)
```

Type classes are foundational in Scala libraries such as Cats, Circe, and many functional ecosystems.

You should understand type classes before deeply studying Cats or effect-polymorphic programming.

---

### 5.3 Opaque Types and Domain Modeling

Opaque types allow you to create domain-specific types with little or no runtime overhead.

Example:

```scala
opaque type UserId = String

object UserId:
  def from(value: String): Option[UserId] =
    if value.nonEmpty then Some(value) else None

extension (id: UserId)
  def value: String = id
```

Use opaque types for:

```text
UserId
Email
OrderId
Money
Percentage
NonEmptyString
Quantity
```

This helps prevent primitive obsession, where everything is represented by raw `String`, `Int`, or `BigDecimal`.

---

## 6. Stage Five: Concurrency and Effect Systems

This stage moves from single-threaded transformations to programs that interact with the outside world. Start with `Future` to understand the JVM's standard concurrency story and its limits, then commit to one effect system to learn structured concurrency, typed errors, and resource safety in depth.

### 6.1 Future and Basic Concurrency

Scala's standard library provides `Future` for asynchronous computation:

```scala
val result: Future[User] =
  userRepository.findAsync(id)
```

Learn:

```text
ExecutionContext
map
flatMap
recover
recoverWith
sequence
traverse
timeout patterns
```

Also learn the limitations of `Future`:

```text
Future is eager
cancellation is weak
error channel is not typed
resource management is not very structured
blocking operations require care
```

This prepares you for Cats Effect or ZIO.

---

### 6.2 Effect Systems: Cats Effect or ZIO

Do not start here too early. First become comfortable with:

```text
Option
Either
Future
for-comprehension
map / flatMap
basic type classes
```

Then choose one main effect system.

#### Cats Effect / Typelevel Route

Learn:

```text
IO
Resource
Ref
Deferred
Queue
Fiber
cancellation
structured concurrency
fs2
http4s
doobie
circe
```

Core idea:

```text
Describe effects as values, then let a runtime execute them.
```

Example:

```scala
val program: IO[Unit] =
  for
    user <- readUser
    _    <- sendEmail(user)
  yield ()
```

#### ZIO Route

Learn:

```text
ZIO[R, E, A]
ZLayer
Scope
typed errors
Fiber
Schedule
Queue
Ref
ZStream
ZIO HTTP
zio-json
zio-test
```

ZIO makes dependencies, errors, and results visible in the type:

```scala
ZIO[UserRepo, CreateUserError, User]
```

Choose one route deeply first. Do not try to master Cats Effect and ZIO at the same time in the beginning.

---

## 7. Stage Six: Advanced Types and JVM Engineering

Scala runs on the JVM, and its type system can express much more than most application code requires. This stage is where you go deep on both: enough type-level fluency to read and design libraries, and enough JVM awareness to debug production systems.

### 7.1 Advanced Type System Topics

Learn these gradually after you are comfortable writing real Scala applications.

#### Generics

```scala
def first[A](values: List[A]): Option[A] =
  values.headOption
```

Learn:

```text
type parameters
upper bounds
lower bounds
context bounds
```

#### Variance

```scala
trait Producer[+A]
trait Consumer[-A]
trait Box[A]
```

Understand:

```text
covariance
contravariance
invariance
```

#### Higher-kinded Types

Example:

```scala
trait Repository[F[_]]:
  def findUser(id: UserId): F[Option[User]]
```

This appears in tagless final, Cats, and effect-polymorphic programs.

#### Match Types

Scala 3 supports type-level pattern matching:

```scala
type Elem[X] = X match
  case String => Char
  case Array[t] => t
  case Iterable[t] => t
```

This is mostly useful for library authors.

#### Inline and Macros

Learn later:

```text
inline
transparent inline
compiletime operations
quotes
Expr
```

Application developers usually need to read common macro usage before they need to write macros themselves.

---

### 7.2 JVM and Java Interoperability

Scala 3 runs on the JVM. Advanced Scala developers must understand JVM realities.

Learn:

```text
class loading
heap
stack
GC
JIT
threads
blocking IO
synchronized
volatile
exceptions
classpath
```

Java interop topics:

```text
Java collection conversion
Optional versus Option
CompletableFuture versus Future / IO / ZIO
checked exceptions
null boundaries
annotations
```

No matter how functional your Scala code is, production systems still face JVM issues such as thread pools, blocking calls, GC, dependency conflicts, and classpath problems.

---

## 8. Stage Seven: Engineering Practices and Ecosystem

The final stage covers the tooling, testing, and ecosystem decisions that turn Scala code into shippable systems. None of this is exotic, but Scala's expressiveness makes consistent style, good tests, and well-chosen libraries especially valuable.

### 8.1 Build Tools and Engineering

#### sbt

Learn sbt first:

```text
build.sbt
libraryDependencies
multi-project builds
test
run
assembly
dependency eviction
compiler options
```

Common commands:

```bash
sbt compile
sbt test
sbt run
```

#### Scala CLI and Mill

Scala CLI is convenient for learning and scripts. Mill is used by some teams for larger builds. Learn them after sbt basics.

Suggested order:

```text
sbt first
Scala CLI second
Mill as needed
```

#### Formatting and Linting

Learn:

```text
scalafmt
scalafix
compiler warnings
wartremover or scalafix rules
```

Scala is expressive, so consistent formatting and team conventions matter a lot.

---

### 8.2 Testing

Common testing tools:

```text
ScalaTest
MUnit
weaver-test
zio-test
ScalaCheck
Hedgehog
Discipline
```

Learn:

```text
unit testing
table-driven testing
property-based testing
effectful testing
test fixtures
fakes over excessive mocking
```

Property-based testing is especially valuable in Scala.

Example properties:

```text
reverse(reverse(xs)) == xs
decode(encode(value)) == value
normalizing twice gives the same result as normalizing once
```

---

### 8.3 Web, Database, and Streaming Ecosystem

#### Typelevel Route

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

#### ZIO Route

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

#### Actor and Stream Route

For actor systems and distributed applications, learn:

```text
Akka Typed
Apache Pekko
Akka Streams / Pekko Streams
Cluster
Persistence
```

Do not mix too many ecosystems early. Pick one main route and go deep.

---

## 9. Recommended Learning Order

A practical learning sequence:

```text
1. Scala 3 syntax and expression-oriented programming
2. Case class, enum, and pattern matching
3. Collections: List, Vector, Map, Option, Either
4. Functional basics: pure functions, immutability, higher-order functions
5. for-comprehension and map / flatMap
6. Class, trait, object, and composition
7. Error modeling with Option and Either
8. Extension methods
9. given / using and contextual abstractions
10. Type class basics
11. Opaque types and domain modeling
12. Future and ExecutionContext
13. sbt, testing, formatting, and engineering workflow
14. JVM and Java interoperability
15. Choose Cats Effect or ZIO as the main effect-system route
16. HTTP, JSON, database, and configuration ecosystem
17. Streaming: fs2, ZStream, or Akka Streams
18. Advanced type system: variance, higher-kinded types, match types
19. Inline, macros, and metaprogramming
20. Performance, GC, thread pools, observability, and production operations
```

---

## Final Advice

Scala 3 is not about writing the most abstract code possible. Mature Scala code should be:

```text
clear in its domain model
precise in its types
moderate in its abstractions
explicit about errors
careful with side effects
safe in resource management
readable by a team
stable on the JVM
```

The ultimate goal is to combine Scala 3's type system, functional programming model, and JVM engineering capabilities to build systems that are safer, clearer, and easier to maintain.
