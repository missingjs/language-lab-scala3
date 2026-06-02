[← Back to projects](../README.md)

# Project 10a: Database-backed Bookmark API with Doobie

> Route A (Cats Effect / Typelevel). For the ZIO equivalent, see [Project 10b](../10b-zio-bookmark-db/README.md).

## Goal

Add PostgreSQL or SQLite persistence to the Bookmark API.

## Focus

```text
doobie
Transactor
ConnectionIO
transactions
SQL mapping
resource safety
migration
integration testing
```

## Completion Criteria

```text
Database operations live in the repository layer
Transaction boundaries are clear
Has migrations
Has integration tests
Connection pool is managed by Resource
```
