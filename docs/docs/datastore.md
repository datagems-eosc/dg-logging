# Data Stores

The Logging service provides an aggregation functionality through which DataGEMS service distributed logs are accumulated in a single centralized repository. These logs are persisted with various retention policies as needed.

## Event Datastore

The log entry data is stored in a NoSQL Elastic Search datastore. The indices define rollover policies that ensure that after a period of time the logs are discarded.

## Updates

When updating the Elastic Stack service to newer versions, any needed indice updates are handled by the migration process of the ELK stack.
