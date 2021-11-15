## Monitoring Granularity
TencentDB for MongoDB does not support customizing monitoring granularity. The adaptive monitoring policy is as follows:

| Time Span | Monitoring Granularity | Retention Period |
| -------- | -------- | -------- |
| 0-1 day    | 5 seconds      | 1 day      |
| 0-2 days  | 1 minute    | 2 days      |
| 2-7 days  | 5 minutes    | 7 days      |
| 7-30 days | 1 hour    | 30 days     |

## Types of Instances for Monitoring
TencentDB for MongoDB master, read-only, and disaster recovery instances can be monitored, and each instance is provided with a separate monitoring view for easy query.

## Monitoring Metrics

Cloud Monitor provides the following monitoring metrics for TencentDB for MongoDB instances:

| Metric Name | Metric | Unit | Dimension | Description |
| ---------------- | ----------------- | ----- | ---- | ------------------------------------------ |
| Write requests | inserts | - | Cluster | Number of write requests in the current cluster |
| Read requests | reads | - | Cluster | Number of read requests in the current cluster |
| Update requests | updates | - | Cluster | Number of update requests in the current cluster |
| Deletion requests | deletes | - | Cluster | Number of deletion requests in the current cluster |
| count requests | counts | - | Cluster | Total number of requests in the current cluster |
| Aggregates requests | aggregates | - | Cluster | Number of aggregation requests in the current cluster |
| Cluster connections | conn | - | Cluster | Total number of connections, i.e., the total number of connections received by the current cluster proxy |
| Cluster connection percentage | connper | % | Cluster | Proportion of current connections to the configured total connections of the cluster |
| Capacity utilization | diskusage | % | Cluster | Proportion of used storage capacity to the configured total capacity of the cluster |
| QPS | qps | - | Cluster | Operations per second, including CRUD operations |
| 10–50 ms | 10 ms | - | Cluster | Number of requests with an execution time between 10 and 50 ms |
| 50–100 ms | 50 ms | - | Cluster | Number of requests with an execution time between 50 and 100 ms |
| 100 ms | 100 ms | - | Cluster | Number of requests with an execution time of more than 100 ms |
| Timeouts | timeouts | - | Cluster | Number of timed-out requests |
| Master/slave lag | slavedelay | Seconds | Cluster | Master/slave lag time |
| Oplog time difference | oplogreservedtime | Hours | Cluster | Time difference between the last operation and the first operation in oplog |
| CPU utilization | cpuusage | % | Node | CPU utilization of the current node |
| Memory utilization | memusage | % | Node | Memory utilization of the current node |
| qr | qr | - | Node | Length of client read request queue |
| qw | qw | - | Node | Length of client write request queue |
| Connection count | conn | - | Node | Number of connections of the current mongod node |
| netin | netin | MB/s | Node | Inbound traffic |
| netout | netout | MB/s | Node | Outbound traffic |
