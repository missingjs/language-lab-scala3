[← Back to projects](../README.md)

# Project 1: CLI TODO Tool

## Goal

Build a small command-line TODO app:

```text
todo add "learn Scala 3"
todo list
todo done 1
todo remove 1
```

## Focus

```text
sbt
Scala 3 syntax
case class
enum
List / Vector / Map
Option
Either
pattern matching
basic file IO
unit testing
```

## Suggested Model

```scala
case class Todo(
  id: TodoId,
  title: String,
  status: TodoStatus
)

enum TodoStatus:
  case Open
  case Done
```

## Completion Criteria

```text
Can add, list, complete, and delete tasks
Data persists to a local file
No null usage
Core logic has tests
Errors are not handled by raw unchecked exceptions
```
