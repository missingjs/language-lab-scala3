[← Back to projects](../README.md)

# Project 14: Real-time Event Stream Service

> Shared advanced project. Useful whether you chose Cats Effect or ZIO in [Project 7](../07-effect-system-choice/README.md).

## Goal

Build an SSE or WebSocket event service.

Features:

```text
clients subscribe to events
server broadcasts messages
client disconnects are handled
slow clients are isolated
```

## Focus

```text
streaming
PubSub
backpressure
client lifecycle
resource cleanup
concurrent broadcasting
```

## Completion Criteria

```text
Resources are released when a client disconnects
Slow clients do not block everyone else
Broadcasting logic is testable
Supports graceful shutdown
```
