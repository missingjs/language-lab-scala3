[← Back to projects](../README.md)

# Project 15: Typed Domain Service

> Shared advanced project. Useful whether you chose Cats Effect or ZIO in [Project 7](../07-effect-system-choice/README.md).

## Goal

Choose a business domain and model its core logic without focusing on Web or database first.

Possible domains:

```text
payment authorization
subscription billing
inventory reservation
ticket booking
workflow approval
```

## Focus

```text
opaque types
enum
state machines
typed errors
illegal states unrepresentable
domain events
pure core + effectful shell
```

## Example

```scala
enum PaymentState:
  case Created
  case Authorized(authId: AuthId)
  case Captured(captureId: CaptureId)
  case Failed(reason: PaymentFailure)
```

## Completion Criteria

```text
Illegal states are difficult or impossible to represent
State transitions are pure functions
Errors are typed
Has property-based tests
Side effects are at the boundary
```

This is one of the most valuable Scala projects because it trains type-driven domain modeling.
