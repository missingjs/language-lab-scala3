[← Back to projects](../README.md)

# Project 11b: ZStream Log Processor

> Route B (ZIO). For the Cats Effect equivalent, see [Project 11a](../11a-fs2-log-processor/README.md).

## Goal

Build a streaming log processor using ZStream.

## Focus

```text
ZStream
ZPipeline
backpressure
chunks
resource safety
parallel processing
```

## Completion Criteria

```text
Does not load large files into memory
Uses ZStream to compose the processing flow
Supports clear error handling
Supports concurrent processing where useful
Has zio-test tests
```
