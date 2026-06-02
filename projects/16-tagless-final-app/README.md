[← Back to projects](../README.md)

# Project 16: Mini Tagless Final App

> Shared advanced project. Useful whether you chose Cats Effect or ZIO in [Project 7](../07-effect-system-choice/README.md).

## Goal

Build a small application using effect-polymorphic design.

## Example

```scala
trait UserRepository[F[_]]:
  def find(id: UserId): F[Option[User]]

trait EmailService[F[_]]:
  def send(email: Email): F[Unit]

final class UserProgram[F[_]: Monad](
  users: UserRepository[F],
  emails: EmailService[F]
):
  def run(id: UserId): F[Unit] =
    ...
```

## Focus

```text
higher-kinded types
type classes
Monad
effect polymorphism
testability
algebra / interpreter pattern
```

## Completion Criteria

```text
Business logic is not tied to a concrete IO or ZIO type
Has a test interpreter
Has a production interpreter
Abstraction is justified and not excessive
You can explain why F[_] is useful here
```

Do this project late, after you are comfortable with an effect system.
