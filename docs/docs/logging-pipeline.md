# Logging Overview

## Ingestion Pipeline

The logging service offers various entrypoints through which log ingestion can take place, as it is backed by the mechanisms available by the ELK stack. For the purpose of the DataGEMS integration we have choosen a less intrucive approach for the integrating components.

We make use of the Beats agents offered by the ELK stack. Through the deployment model utilized, an agent will read the logs produced by each pod and will scan for entries marked as Log Entries. A transformation step will apply any needed mutations to the log entry retrieved to match the logging model expected by the logging service. The trasformation can be customized based on specific deployment labels. A set of supported schemas is provided and each deployed service can declare the logging event schema it conforms to. Based on this schema the transformation is applied. After the log entry model is transformed, enriched with environment metadata and generated, it is pused to the logging service datastore where it becomes available for browsing.
