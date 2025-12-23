# Logging Overview

## Log Formats

Two log formats are supported at this point. They are very similar but have been extended to support generic log construction rather than rely on specific implementation details of some logging library. A note to be repeated here, additonal properties are allowed and will be available in the logging service indices, but not as searchable fields.

For the logging service to distinguish between the supported formats, the deployment of each component must be decorated with the log format that it produces.

### json-cf-1 format

**json-cf-1** is a log format that expects the following information to be available in the log message:

```json
{
  "@t": "2025-07-22T12:00:00.000Z",
  "@mt": "Sample log message",
  "@l": "Info",
  "DGCorrelationId": "a...0",
  "UserId": "a...0",
  "ClientId": "a...0"
}
```

### json-cf-2 format

**json-cf-2** is a log format that expects the following information to be available in the log message:

```json
{
  "timestamp": "2025-07-22T12:00:00.000Z",
  "msg": "Sample log message",
  "level": "Info",
  "DGCorrelationId": "a...0",
  "UserId": "a...0",
  "ClientId": "a...0"
}
```
