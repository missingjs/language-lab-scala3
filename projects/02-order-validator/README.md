[← Back to projects](../README.md)

# Project 2: Order Validator

## Goal

Build a pure domain validator for orders.

Input:

```text
customer email
shipping address
line items
coupon
payment method
```

Output:

```text
valid order
or validation errors
```

## Focus

```text
case class
enum
opaque type
Either
Validated-style thinking
domain error modeling
pure functions
```

## Suggested Model

```scala
opaque type Email = String
opaque type OrderId = String
opaque type Quantity = Int

enum ValidationError:
  case EmptyEmail
  case InvalidEmailFormat
  case EmptyCart
  case InvalidQuantity
  case UnsupportedPaymentMethod
```

## Completion Criteria

```text
Email, Quantity, and OrderId are not raw String or Int everywhere
Validation errors are modeled as enum values
Business logic is pure
Can accumulate multiple validation errors
Has some property-based tests
```
