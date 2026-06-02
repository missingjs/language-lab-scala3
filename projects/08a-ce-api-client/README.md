[← Back to projects](../README.md)

# Project 8a: Cats Effect CLI API Client

> Route A (Cats Effect / Typelevel). For the ZIO equivalent, see [Project 8b](../08b-zio-api-client/README.md).

## Goal

Build a CLI client that:

```text
reads configuration
calls an external HTTP API
parses JSON
prints results
handles errors
```

## Focus

```text
IO
Resource
retry
timeout
cancellation
http4s client
circe
pure description of effects
```

## Completion Criteria

```text
main returns IO[Unit]
HTTP client is managed with Resource
All side effects are represented by IO
Has timeout
Has tests or a mock client
```
