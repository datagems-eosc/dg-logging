# Maintenance

The service is part of the DataGEMS platform offered through an existing deployment, following the DataGEMS release and deployment procedures over a managed infrasrtucture along with the maintenance activities that are scheduled within the platform. The purpose of this section is not to detail the maintenance activities put in place by the DataGEMS team.

## Healthchecks

The service [observability documentation](https://www.elastic.co/docs/api/doc/elasticsearch/operation/operation-cluster-health) describes healthcheck endpoints that can be used to track the status of the service. 

An example of a healthcheck response that returns 200 OK for healthy state is:
```json
{
  "cluster_name": "e...h",
  "status": "green",
  "timed_out": false,
  "number_of_nodes": "...",
  "number_of_data_nodes": "...",
  "active_primary_shards": "...",
  "active_shards": "...",
  "relocating_shards": "...",
  "initializing_shards": "...",
  "unassigned_shards": "...",
  "delayed_unassigned_shards": "...",
  "number_of_pending_tasks": "...",
  "number_of_in_flight_fetch": "...",
  "task_max_waiting_in_queue_millis": "...",
  "active_shards_percent_as_number": "..."
}
```

## Verions & Updates

The service follows the versioning and update scheme that ELK supports.

## Backups

All state persisted by the service is maintained in the elastic indices as described in the respective [datastores](datastore.md) section.

To keep backups of the state, the respective utilities must be scheduled to run in a consistent manner. 

## Troubleshooting

Troubleshooting is primarily done through the logging mechanisms that are from the ELK stack components.
