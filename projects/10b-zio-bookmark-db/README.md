[← Back to projects](../README.md)

# Project 10b: ZIO Database-backed API

> Route B (ZIO). For the Cats Effect equivalent, see [Project 10a](../10a-ce-bookmark-db/README.md).

## Goal

Add database persistence to the Bookmark API.

Possible tools:

```text
Quill
JDBC wrapper
zio-jdbc
```

## Focus

```text
transactions
connection pool
ZLayer resource
typed DB errors
integration testing
```

## Completion Criteria

```text
Database resources are managed through Layer
DB errors are converted into domain errors
Transaction boundaries are clear
Has integration tests
```
