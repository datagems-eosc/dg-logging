# Logging Overview

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
