[← Back to projects](../README.md)

# Project 5: Mini Parser Combinator

## Goal

Build a tiny parser combinator library.

Support:

```text
char
string
digit
many
orElse
map
flatMap
```

Suggested model:

```scala
case class Parser[+A](run: String => Either[ParseError, (A, String)])
```

Example:

```scala
val number: Parser[Int] =
  digit.many.map(_.mkString.toInt)
```

## Focus

```text
higher-order functions
map
flatMap
for-comprehension
generic data types
error modeling
functional composition
```

## Completion Criteria

```text
Parser has map and flatMap
Can compose parsers with for-comprehension
Errors include position information
Can parse a simple expression or CSV line
Has tests
```

This project teaches why `map`, `flatMap`, and `for-comprehension` are central to Scala.
