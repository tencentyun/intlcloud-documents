## Namespace

Namespace=QCE/CMONGO



## Monitoring Metrics

### MongoDB

#### 1. Requests

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :-------------- | :------------------------- | :---- | :---------------- |
| Inserts    | Write requests    | Number of writes in unit time         | -    | target (instance ID) |
| Reads      | Read requests    | Number of reads in unit time         | -    | target (instance ID) |
| Updates    | Update requests    | Number of updates in unit time         | -    | target (instance ID) |
| Deletes    | Deletion requests    | Number of deletions in unit time         | -    | target (instance ID) |
| Counts     | Count requests  | Number of counts in unit time      | -    | target (instance ID) |
| Aggregates | Aggregate requests    | Number of aggregates in unit time     | -    | target (instance ID) |
| Success    | Successful requests    | Number of successful requests in unit time     | -    | target (instance ID) |
| Commands   | Command requests | Number of command requests in unit time     | -    | target (instance ID) |
| Timeouts   | Timed-out requests    | Number of timed-out requests in unit time     | -    | target (instance ID) |
| Qps        | Requests per second  | Number of operations per second, including CRUD operations | Requests/sec | target (instance ID) |

#### 2. Delay requests

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :--------------------------- | :--------------------------------------- | :--- | :---------------- |
| Delay10 | Requests with a delay of 10–50 ms | Number of successful requests with a delay of 10–50 ms in unit time | -  | target (instance ID) |
| Delay50 | Requests with a delay of 50–100 ms | Number of successful requests with a delay of 50–100 ms in unit time | -  | target (instance ID) |
| Delay100 | Requests with a delay of over 100 ms | Number of successful requests with a delay of over 100 ms in unit time | -  | target (instance ID) |

#### 3. Connections

| Parameter | Metric | Description | Unit | Dimension |
| :---------- | :--------- | :------------------------------------------ | :--- | :---------------- |
| ClusterConn | Cluster connections | Total number of cluster connections, i.e., the total number of connections received by the current cluster proxy | - | target (instance ID) |
| Connper | Connection utilization | Proportion of current connections to the configured total connections of the cluster | % | target (instance ID) |

#### 4. System

| Parameter | Metric | Description | Unit | Dimension |
| :--------------- | :--------- | :----------------------------------------- | :--- | :---------------- |
| ClusterDiskusage | Disk utilization | Proportion of used storage capacity to the configured total capacity of the cluster | % | target (instance ID) |

### MongoDB replica set

#### 1. System

| Parameter | Metric | Description | Unit | Dimension |
| :--------------- | :--------- | :--------------- | :--- | :------------------ |
| ReplicaDiskusage | Disk utilization | Replica set capacity utilization | % | target (replica set ID) |

#### 2. Primary-secondary

| Parameter | Metric | Description | Unit | Dimension |
| :---------------- | :------------ | :--------------------------------------- | :--- | :------------------ |
| SlaveDelay | Primary-secondary lag | Average primary-secondary lag in unit time | Seconds | target (replica set ID) |
| Oplogreservedtime | Oplog retention time | Time difference between the last operation and the first operation in oplog | hours | target (replica set ID) |

#### 3. Cache

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :----------------- | :---------------------------- | :--- | :----------------- |
| CacheDirty | Dirty data percentage in cache | Percentage of dirty data in the current memory cache | % | target (replica set ID) |
| CacheUsed | Cache utilization | Percentage of currently used cache |% | target (replica set ID) |
| HitRatio | Cache hit rate | Current cache hit rate | % | target (replica set ID) |

### Mongo node

#### 1. System

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :----------- | :----------- | :--- | :--------------- |
| CpuUsage | CPU utilization | CPU utilization | % | target (node ID) |
| MemUsage | Memory utilization | Memory utilization | % | target (node ID) |
| NetIn | Network inbound traffic | Network inbound traffic | MB/s | target (node ID) |
| NetOut | Network outbound traffic | Network outbound traffic | MB/s | target (node ID) |
| Disk | Node disk usage | Node disk usage | MB | target (node ID) |

#### 2. Connections

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :--------- | :--------- | :--- | :--------------- |
| Conn | Connections | Number of node connections | - | target (node ID) |

#### 3. Reads and writes

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :------------------------- | :------------------------- | :--- | :--------------- |
| Qr | Read requests waiting in the queue | Number of read requests waiting in the queue | - | target (node ID) |
| Qw | Write requests waiting in the queue | Number of write requests waiting in the queue | - | target (node ID) |
| Ar | ActiveRead of WT engine | Number of active read requests | - | target (node ID) |
| Aw | ActiveWrite of WT engine | Number of active write requests | - | target (node ID) |

#### 4. TTL index

| Parameter | Metric | Description | Unit | Dimension |
| :--------- | :----------------- | :----------------- | :--- | :--------------- |
| TtlDeleted | Data entries deleted by TTL | Number of data entries deleted by TTL | - | target (node ID) |
| TtlPass | TTL running rounds | Number of TTL running rounds | - | target (node ID) |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` values supported by each metric.

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | -------- | --------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name | target | Target dimension name | Enter a String-type dimension name: target |
| Instances.N.Dimensions.0.Value | target | Subject to the query dimension | Please see the [value reference table](#dimensions.0.value-.E5.8F.96.E5.80.BC.E5.8F.82.E7.85.A7.E8.A1.A8) |

> ?Valid values of `Instances.N.Dimensions.0.Value` for TencentDB:
> TencentDB for MongoDB is a cluster service. You can query monitoring data in three dimensions: "cluster", "replica set", and "node" as detailed below:
>- "Cluster" dimension: it represents a certain TencentDB for MongoDB instance you purchased. In this dimension, you can query the number of read and write requests, capacity utilization, and timed-out requests of the entire instance.
>- "Replica set" dimension: you can query the internal capacity utilization and primary-secondary lag of a certain replica set in the cluster. A replica set instance itself contains only one replica set, while each shard of a shard instance is a replica.
>- "Node" dimension: you can query the CPU, memory, and other information of any node in the cluster.

### dimensions.0.value value reference table

| Value Type | Sample Value | Description |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Instance ID              | cmgo-6ielucen                                                | Unique ID of a TencentDB for MongoDB instance, <br><li>which can be obtained in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb) <br><li>or by calling an applicable TencentDB for MongoDB API |
| Replica set ID            | <li>cmgo-6ielucen_0<br><li>cmgo-6ielucen_2                   | A replica set ID can be obtained by adding "\_index number" after the instance ID. <br>The "index number" starts at 0 and can be up to the number of replica sets - 1. A replica set instance has only one replica set, so it is sufficient to always suffix "\_0". A sharded instance has many shards, each of which is a replica set; for example, for the replica set ID of the third shard, suffix "\_2" |
| Node ID              | <li>cmgo-6ielucen_0-node-primary<br><li>cmgo-6ielucen_1-node-slave0<br><li>cmgo-6ielucen_3-node-slave2 | <li>Add "-node-primary" after the replica set ID to get the primary node ID of the replica set. <br><li>Add "-node-slave node index number" after the replica set ID to get the corresponding secondary node ID. The "secondary node index number" starts at 0 and can be up to the number of secondary nodes - 1 |

## Input Parameter Description

**To query the monitoring data of a TencentDB for MongoDB instance, use the following input parameters:**
&Namespace=QCE/CMONGO
&Instances.N.Dimensions.0.Name=target
&Instances.N.Dimensions.0.Value=subject to query dimension
