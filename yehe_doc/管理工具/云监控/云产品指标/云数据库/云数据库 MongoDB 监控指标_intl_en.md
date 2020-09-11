## Namespace

Namespace=QCE/CMONGO

## Monitoring Metrics

>?The metrics `Aggregates`, `Timeouts` and `Conn` are deprecated.

| Parameter | Metric Name | Description | Unit | Dimension |
| ----------------- | -------------------------- | ------------------------------------------- | ----- | ------------------- |
| Inserts | Write requests | Writes per unit time | Times | target (instance ID) |
| Reads | Read requests | Reads per unit time | Times | target (instance ID) |
| Updates | Update requests | Updates per unit time | Times | target (instance ID) |
| Deletes | Delete requests | Deletions per unit time | Times | target (instance ID) |
| Counts | Count requests | Counts per unit time | Times | target (instance ID) |
| ClusterConn | Cluster connections | Total number of cluster connections, which indicates the connections received by the current cluster proxy | Times | target (instance ID) |
| Commands | Command requests | Number of command requests | Times | target (instance ID) |
| Connper | Percentage of cluster connections | Ratio of the current cluster connections to the configured total cluster connections | % | target (instance ID) |
| ClusterDiskUsage | Cluster capacity utilization | Ratio of the actually used storage space to the configured total capacity | % | target (instance ID) |
| QPS | Operations | Operations per second, including CRUD operations | Times/sec | target (instance ID) |
| Success | Number of successful requests | Number of successful requests per unit time | Times | target (instance ID) |
| Delay10 | Number of requests with a latency between 10 ms and 50 ms | Number of successful requests with a latency between 10 ms and 50 ms per unit time | Times | target (instance ID) |
| Delay50 | Number of requests with a latency between 50 ms and 100 ms | Number of successful requests with a latency between 50 ms and 100 ms per unit time | Times | target (instance ID) |
| Delay100 | Number of requests with a latency over 100 ms | Number of successful requests with a latency over 100 ms | Times | target (instance ID) |
| ReplicaDiskUsage | Disk utilization | Replica set capacity utilization | % | target (replica set ID) |
| Slavedelay | Master-Slave latency | Average latency per unit time between the Master and Slave | Second | target (replica set ID) |
| Oplogreservedtime | Oplog save time | Time difference between the last operation and the first operation for Oplog records | Hour | target (replica set ID) |
| Cpuusage | CPU utilization | CPU utilization | % | target (node ID) |
| Memusage | Memory utilization | Memory utilization | % | target (node ID) |
| Qr | Read request queue length | Number of read requests in the waiting queue | Count | target (node ID) |
| Qw | Write request queue length | Number of write requests in the waiting queue | Count | target (node ID) |
| Netin | Network inbound traffic | Network inbound traffic | MB/s | target (node ID) |
| Netout | Network outbound traffic | Network outbound traffic | MB/s | target (node ID) |

> The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to obtain the `period` supported by each metric.

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | -------- | -------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name | target | Dimension name of target | Enter a string-type dimension name, such as target |
| Instances.N.Dimensions.0.Value | target | Subject to the actual query dimension | See the [value reference table](#dimensions.0.value-.E5.8F.96.E5.80.BC.E5.8F.82.E7.85.A7.E8.A1.A8) |

> **TencentDB for Redis Instances.N.Dimensions.0.Value:**
> Tencent Cloud’s MongoDB is a cluster service. You can use the API to query the monitoring data of MongoDB from three dimensions: "cluster", "replica set", and "node".
> - "Cluster" represents a MongoDB instance that you purchased. You can query the number of read/write requests, the capacity utilization, and the timeout requests of the entire instance through this dimension.
> - The "replica set" dimension can be used to query the internal capacity utilization and the master-slave latency of a replica set in the cluster. A replica set instance contains only one replica set, and each shard of a sharding instance is a replica.
> - The "node" dimension can be used to query information such as the CPU and the memory utilization of a node in a cluster.

### Reference table of dimensions.0.value

| Value Type | Sample Value | Parameter Description |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Instance ID | cmgo-6ielucen | Instance ID, the unique identifier of a MongoDB instance. <br><li>It can be obtained on the [MongoDB Console](https://console.cloud.tencent.com/mongodb)<br><li> or by calling the MongoDB API |
| Replica set ID | <li>cmgo-6ielucen_0<br><li>cmgo-6ielucen_2 | A replica set ID can be obtained by appending "\_index number" to the instance ID. <br>The "index number" starts from 0 and has a maximum value that equals to 1 less than the number of replica sets. A replica set instance has only one replica set so "\_0" should be suffixed. A sharded instance has many shards, each of which is a replica set. For example, for the replica set ID of the third shard, suffix "\_2" |
| Node ID | <li>cmgo-6ielucen_0-node-primary<br><li>cmgo-6ielucen_1-node-slave0<br><li>cmgo-6ielucen_3-node-slave2 | <li>Append "-node-primary" to the replica set ID to obtain the master node ID of the replica set. <br><li>Append "-node-slave node index number" to the replica set ID to obtain the corresponding slave node ID. The "slave node index number" starts from 0 and has a maximum value that equals to 1 less than the number of slave nodes |

## Input Parameters

To query the monitoring data of TencentDB for MongoDB, use the following input parameters:
&Namespace=QCE/CMONGO
&Instances.N.Dimensions.0.Name=target
&Instances.N.Dimensions.0.Value=<Subject to the actual query dimension> 
