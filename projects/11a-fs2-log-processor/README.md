[← Back to projects](../README.md)

# Project 11a: fs2 Streaming Log Processor

> Route A (Cats Effect / Typelevel). For the ZIO equivalent, see [Project 11b](../11b-zstream-log-processor/README.md).

## Goal

Build a streaming log processor:

```text
read large log file
parse records as a stream
aggregate status codes and paths
output JSON report
```

## Focus

```text
fs2 Stream
Pipe
Chunk
backpressure
resource safety
concurrent stream processing
```

## Completion Criteria

```text
Does not load the full file into memory
Parsing logic is a Pipe
Transformations are composable
Errors are clear
Has benchmark or basic performance observation
```
