[← Back to projects](../README.md)

# Project 4: Mini JSON Encoder Type Class

## Goal

Implement a tiny JSON encoder without using a real JSON library.

Example:

```scala
trait JsonEncoder[A]:
  def encode(value: A): String
```

Support:

```text
String
Int
Boolean
List[A]
Option[A]
case class User
```

Example API:

```scala
def toJson[A](value: A)(using encoder: JsonEncoder[A]): String =
  encoder.encode(value)

extension [A](value: A)
  def toJson(using JsonEncoder[A]): String =
    summon[JsonEncoder[A]].encode(value)
```

## Focus

```text
trait
given
using
summon
extension methods
type classes
generic abstraction
```

## Completion Criteria

```text
Can define encoders for custom types
Can compose encoders for Option[A] and List[A]
Uses given / using
Provides extension method syntax
Does not depend on a real JSON library
```
