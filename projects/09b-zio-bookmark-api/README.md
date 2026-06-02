[← Back to projects](../README.md)

# Project 9b: ZIO HTTP Bookmark API

> Route B (ZIO). For the Cats Effect equivalent, see [Project 9a](../09a-ce-bookmark-api/README.md).

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
ZIO HTTP
ZLayer
service pattern
typed errors
JSON codec
middleware
```

## Completion Criteria

```text
Repository, service, and HTTP layers are separated
Error channel is explicit
Dependencies are composed with ZLayer
Has zio-test tests
```
