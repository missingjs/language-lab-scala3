[← Back to projects](../README.md)

# Project 9a: http4s Bookmark API

> Route A (Cats Effect / Typelevel). For the ZIO equivalent, see [Project 9b](../09b-zio-bookmark-api/README.md).

## Goal

Build a small REST API:

```text
POST   /bookmarks
GET    /bookmarks
GET    /bookmarks/{id}
DELETE /bookmarks/{id}
```

## Focus

```text
Cats Effect IO
http4s routes
circe JSON
service / repository layering
EitherT
error handling
Resource
```

## Completion Criteria

```text
Domain model and HTTP layer are separated
Errors map to consistent HTTP responses
Repository is a trait
Service logic can be tested independently
Startup and shutdown are managed by Resource
```
