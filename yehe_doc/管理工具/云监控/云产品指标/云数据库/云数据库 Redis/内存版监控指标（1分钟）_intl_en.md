## Namespace

Namespace=QCE/REDIS

## Monitoring Metrics

### Standard edition

| Parameter | Metric Name | Unit | Description | Dimension |
| ---------------- | ---------------- | ----- | ------------------------------------------------------------ | ---------- |
| CpuUsMin | CPU utilization | % | Average CPU utilization | instanceid |
| StorageMin | Memory usage | MB | Actually used memory capacity, including the capacity for data and cache | instanceid |
| StorageUsMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory | instanceid |
| KeysMin | Total number of keys | Count | Total number of keys (level-1 keys) in instance storage | instanceid |
| ExpiredKeysMin | Expired keys | Count | Number of keys expired in a time window, which corresponds to the value of `expired_keys` outputted by the `info` command | instanceid |
| EvictedKeysMin | Evicted keys | Count | Number of keys evicted in a time window, which corresponds to the value of `evicted_keys` outputted by the `info` command | instanceid |
| ConnectionsMin | Connections | Count | Number of TCP connections to an instance | instanceid |
| ConnectionsUsMin | Connection utilization | % | Ratio of the actual number of TCP connections to the maximum number of connections | instanceid |
| InFlowMin | Inbound traffic | Mb/s | Private inbound traffic | instanceid |
| InFlowUsMin | Inbound traffic utilization | % | Ratio of the actually used private inbound traffic to the maximum traffic | instanceid |
| OutFlowMin | Outbound traffic | Mb/s | Private outbound traffic | instanceid |
| OutFlowUsMin | Outbound traffic utilization | % | Ratio of the actually used private outbound traffic to the maximum traffic | instanceid |
| LatencyMin | Average execution latency | ms | Average execution latency between the proxy and the Redis server | instanceid |
| LatencyGetMin | Average execution latency of the `read` command | ms | Average execution latency of the `read` command between the proxy and the Redis server | instanceid |
| LatencySetMin | Average execution latency of the `write` command | ms | Average execution latency of the `write` command between the proxy and the Redis server | instanceid |
| LatencyOtherMin | Average execution latency of other commands | ms | Average execution latency of commands other than `read` and `write` between the proxy and the Redis server | instanceid |
| QpsMin | Total requests | Times/sec | QPS, that is, the number of command executions | instanceid |
| StatGetMin | Read requests | Times/min | Number of read command executions | instanceid |
| StatSetMin | Write requests | Times/min | Number of write command executions | instanceid |
| StatOtherMin | Other requests | Times/sec | Number of command executions other than reads and writes | instanceid |
| BigValueMin | Big-value requests | Times/sec | Number of command executions for which the request size exceeds 32 KB | instanceid |
| SlowQueryMin | Slow queries | Count | Number of slow queries | instanceid |
| StatSuccessMin | Read request hits | Count | Number of existing read request keys, which corresponds to the value of the `keyspace_hits` metric outputted by the `info` command | instanceid |
| StatMissedMin | Read request misses | Count | Number of nonexistent read request keys, which corresponds to the value of the `keyspace_misses` metric outputted by the `info` command | instanceid |
| CmdErrMin | Execution errors | Count | Number of command execution errors, such as when a command does not exist or a parameter is incorrect | instanceid |
| CacheHitRatioMin | Read request hit rate | % | Key hits/(key hits + key misses). This metric reflects the severity of cache misses | instanceid |

### Overview of cluster edition

| Parameter | Metric Name | Unit | Description | Dimension |
| ---------------- | ------------------- | ----- | ------------------------------------------------------------ | ---------- |
| CpuUsMin | Average CPU utilization | % | Average CPU utilization | instanceid |
| CpuMaxUsMin | Maximum shard CPU utilization | % | Highest CPU utilization value of all shards in a cluster | instanceid |
| StorageMin | Memory usage | MB | Actually used memory capacity, including the capacity for data and cache | instanceid |
| StorageUsMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory | instanceid |
| StorageMaxUsMin | Maximum shard memory utilization | % | Highest memory utilization value of all shards in a cluster | instanceid |
| KeysMin | Total number of keys | Count | Total number of keys (level-1 keys) in instance storage | instanceid |
| ExpiredKeysMin | Expired keys | Count | Number of keys expired in a time window, which corresponds to the value of `expired_keys` outputted by the `info` command | instanceid |
| EvictedKeysMin | Evicted keys | Count | Number of keys evicted in a time window, which corresponds to the value of `evicted_keys` outputted by the `info` command | instanceid |
| ConnectionsMin | Connections | Count | Number of TCP connections to an instance | instanceid |
| ConnectionsUsMin | Connection utilization | % | Ratio of the actual number of TCP connections to the maximum number of connections | instanceid |
| InFlowMin | Inbound traffic | Mb/s | Private inbound traffic | instanceid |
| InFlowUsMin | Inbound traffic utilization | % | Ratio of the actually used private inbound traffic to the maximum traffic | instanceid |
| OutFlowMin | Outbound traffic | Mb/s | Private outbound traffic | instanceid |
| OutFlowUsMin | Outbound traffic utilization | % | Ratio of the actually used private outbound traffic to the maximum traffic | instanceid |
| LatencyMin | Average execution latency | ms | Average execution latency between the proxy and the Redis server | instanceid |
| LatencyGetMin | Average execution latency of the `read` command | ms | Average execution latency of the `read` command between the proxy and the Redis server | instanceid |
| LatencySetMin | Average execution latency of the `write` command | ms | Average execution latency of the `write` command between the proxy and the Redis server | instanceid |
| LatencyOtherMin | Average execution latency of other commands | ms | Average execution latency of commands other than `read` and `write` between the proxy and the Redis server | instanceid |
| QpsMin | Total requests | Times/sec | QPS, that is, the number of command executions | instanceid |
| StatGetMin | Read requests | Times/sec | Number of read command executions | instanceid |
| StatSetMin | Write requests | Times/sec | Number of write command executions | instanceid |
| StatOtherMin | Other requests | Times/sec | Number of command executions other than reads and writes | instanceid |
| BigValueMin | Big-value requests | Times/sec | Number of command executions for which the request size exceeds 32 KB | instanceid |
| SlowQueryMin | Slow queries | Count | Number of command executions with a latency greater than the slowlog_log_slower_than configuration | instanceid |
| StatSuccessMin | Read request hits | Count | Number of existing read request keys, which corresponds to the value of the `keyspace_hits` metric outputted by the `info` command | instanceid |
| StatMissedMin | Read request misses | Count | Number of nonexistent read request keys, which corresponds to the value of the `keyspace_misses` metric outputted by the `info` command | instanceid |
| CmdErrMin | Execution errors | Count | Number of command execution errors, such as when a command does not exist or a parameter is incorrect | instanceid |
| CacheHitRatioMin | Read request hit rate | % | Key hits/(key hits + key misses). This metric reflects the severity of cache misses | instanceid |

### Cluster sharding

| Parameter | Metric Name | Unit | Description | Dimension |
| -------------------- | ------------ | ----- | ------------------------------------------------------------ | --------------------- |
| CpuUsNodeMin | CPU utilization | % | Average CPU utilization | instanceid and clusterid |
| StorageNodeMin | Memory usage | MB | Actually used memory capacity, including the capacity for data and cache | instanceid and clusterid |
| StorageUsNodeMin | Memory utilization | % | Ratio of the actually used memory to the requested total memory | instanceid and clusterid |
| KeysNodeMin | Total number of keys | Count | Total number of keys (level-1 keys) in instance storage | instanceid and clusterid |
| ExpiredKeysNodeMin | Expired keys | Count | Number of keys expired in a time window, which corresponds to the value of `expired_keys` outputted by the `info` command | instanceid and clusterid |
| EvictedKeysNodeMin | Evicted keys | Count | Number of keys evicted in a time window, which corresponds to the value of `evicted_keys` outputted by the `info` command | instanceid and clusterid |
| QpsNodeMin | Total requests | Times/sec | QPS, that is, the number of command executions | instanceid and clusterid |
| StatGetNodeMin | Read requests | Times/sec | Number of read command executions | instanceid and clusterid |
| StatSetNodeMin | Write requests | Times/sec | Number of write command executions | instanceid and clusterid |
| StatOtherNodeMin | Other requests | Times/sec | Number of command executions other than reads and writes | instanceid and clusterid |
| SlowQueryNodeMin | Slow queries | Count | Number of command executions with a latency greater than the slowlog_log_slower_than configuration | instanceid and clusterid |
| StatSuccessNodeMin | Read request hits | Count | Number of existing read request keys, which corresponds to the value of the `keyspace_hits` metric outputted by the `info` command | instanceid and clusterid |
| StatMissedNodeMin | Read request misses | Count | Number of nonexistent read request keys, which corresponds to the value of the `keyspace_misses` metric outputted by the `info` command | instanceid and clusterid |
| CmdErrNodeMin | Execution errors | Count | Number of command execution errors, such as when a command does not exist or a parameter is incorrect | instanceid and clusterid |
| CacheHitRatioNodeMin | Read request hit rate | % | Key hits/(key hits + key misses). This metric reflects the severity of cache misses. If the number of access requests is 0, the value of this metric will be null | instanceid and clusterid |

> ?The statistical granularity (`period`) may vary by metric. The [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) API can be used to get the `period` supported by each API.

## Overview of Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ---------- | ---------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name | instanceid | Dimension name of the instance ID | Enter a string-type dimension name, such as instanceid |
| Instances.N.Dimensions.0.Value | instanceid | A specific instance ID | Enter a specific Redis instance ID, such as tdsql-123456. The specific Redis instance ID can also be an instance string, such as crs-ifmymj41. It can be queried through the DescribeRedis API |
| Instances.N.Dimensions.1.Name | clusterid | Dimension name of the shard ID | Enter a string-type dimension name, such as clusterid. <br><li> To pull overall information, do not pass in this parameter. <br><li> To pull shard information, the input parameter must be `clusterid` |
| Instances.N.Dimensions.1.Value | clusterid | A specific shard ID | Enter a specific shard ID such as tdsql-123456, which can be obtained by running commands such as `cluster nodes` |

## Input Parameters

To query the monitoring data of TencentDB for Redis, use the following input parameters:
&Namespace=QCE/REDIS
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=instance ID
