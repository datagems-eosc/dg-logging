# Logging Overview

## Log Tracking

In order to serve a user request, a number of services invocations may be chained. It will be useful to be able to track the chain of the request across all involved services. To achive this, we utilize a shared Correlation Id that is generated early in the call stack and propagated across all subsequent invocations.

At the begining of the request stack, we check if there is a correlation id provided for the request in the request headers typically under a header named x-tracking-correlation. If not, we generate one for the request and any downstream calls. We also add it in the logging configuration so that all subsequent log messages include this correlation id.

At the time of invoking another service, we include the correlation id header, along with the correlation id value so that the next service in line will use the same identifier.
