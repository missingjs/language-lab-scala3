[← Back to projects](../README.md)

# Project 12: Background Job Queue

> Shared advanced project. Useful whether you chose Cats Effect or ZIO in [Project 7](../07-effect-system-choice/README.md).

## Goal

Build a small background job system.

Features:

```text
enqueue job
worker executes job
failure retry
maximum retry count
timeout
graceful shutdown
```

## Focus

```text
fibers
queues
worker pool
retry policy
cancellation
resource safety
structured concurrency
```

Cats Effect concepts:

```text
Queue
Deferred
Ref
Supervisor
Resource
```

ZIO concepts:

```text
Queue
Ref
Promise
Fiber
Schedule
Scope
```

## Completion Criteria

```text
Supports multiple workers
Supports retry and backoff
Supports timeout
Supports graceful shutdown
Job state is queryable
Does not leak fibers
```
