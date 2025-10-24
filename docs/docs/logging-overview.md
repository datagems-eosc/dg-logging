# Logging Overview

The DataGEMS services may be operating in cluster where service maintainers do not have direct access. Still, for troubleshooting purposes it will be needed to have access to logs produced by the service to ensure the proper operation of their components. For this reason, a horizontal / common approach to logging must be available across all components. This approach will allow collection of the produced logs, aggregation of these logs in a common repository where they can be browsed, filtered and evaluated.

## Log Tacking

In order to serve a user request, a number of services invocations may be chained. It will be useful to be able to track the chain of the request across all involved services. To achive this, we utilize a shared Correlation Id that is generated early in the call stack and propagated across all subsequent invocations.

At the begining of the request stack, we check if there is a correlation id provided for the request in the request headers typically under a header named x-tracking-correlation. If not, we generate one for the request and any downstream calls. We also add it in the logging configuration so that all subsequent log messages include this correlation id.

At the time of invoking another service, we include the correlation id header, along with the correlation id value so that the next service in line will use the same identifier.

## Log Message Structure

In order for the Logging service to be able to identify key searchable fields by which it can assist the troubleshooting user to group, filter and order the generated logs, some common properties must be directly accessible in logs produced across all services.

The following fields are extracted from the log messages and are available as searcable fields in the logging service:

* timestamp
* message text
* log level
* user identifier
* client identifier (in case the request is not initiated by a user but a service)
* correlation identifier (used to associate cross service request flows)

Additinal properties are available that are directly exracted from the hosting infrastructure. Any additonal properties that are not explicitly extracted from the log message are available within the log message payload available in the logging service.

To facilitate integration with the logging service across components of different technologies, a set of supported log message formats are provided that will allow configuration-less integration. Additionally, the tools to configure custom log message parsing are provided in cases the provided formats cannot be facilatated by some components.

It is recomended that components utilize a logging library that generates structured logs, preferably in JSON format. This will ease the log parsing process as well as enable additional filtering capabilities when browsing the logs.

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
