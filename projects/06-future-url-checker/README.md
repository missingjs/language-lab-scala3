[← Back to projects](../README.md)

# Project 6: Future-based URL Checker

## Goal

Build an asynchronous URL checker:

```text
check urls.txt --parallelism 20 --timeout 2s
```

Output:

```text
OK      https://example.com       200   120ms
FAILED  https://bad.example.com   timeout
```

## Focus

```text
Future
ExecutionContext
traverse
sequence
recover
timeout
Java HTTP Client interop
controlled parallelism
```

## Completion Criteria

```text
Does not launch unlimited parallel requests
Handles timeout
Models errors clearly
Uses ExecutionContext deliberately
Core logic has tests
```

After this project, you should understand:

```text
Future is eager
Future has weak cancellation
blocking IO requires careful thread-pool management
```
