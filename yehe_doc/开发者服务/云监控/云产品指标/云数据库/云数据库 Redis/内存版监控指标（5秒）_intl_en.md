## Namespace

Namespace=QCE/REDIS_MEM

## Monitoring Metrics

### Instance summary 

| Metric | Description | Unit | Dimension |
| ---------------- | ------------------------------------------------------------ | ----- | ---------- |
| MemUsed          | Memory capacity actually used, including data and cache                         | MB    | instanceid |
| CpuUtil          | Average CPU utilization                                              | %     | instanceid |
| MemUtil          | Ratio of the memory actually used to the total memory requested                                 | %     | instanceid |
| Keys             | Total number of keys stored in the instance (first-level keys)                            | -    | instanceid |
| Expired          | Number of keys that expired in the time window, which corresponds to the `expired_keys` output by the `info` command | -    | instanceid |
| Evicted          | Number of keys evicted in the time window, which corresponds to the `evicted_keys` output by the `info` command | -    | instanceid |
| Connections      | Number of TCP connections to the instance                                    | -    | instanceid |
| ConnectionsUtil  | Ratio of the number of actual TCP connections to the maximum number of connections                             | %     | instanceid |
| InFlow           | Private network inbound traffic                                                   | MB/s  | instanceid |
| InBandwidthUtil  | Ratio of the actually used private network inbound traffic to the maximum traffic                               | %     | instanceid |
| InFlowLimit      | Number of times that throttling is triggered by the inbound traffic                                         | -    | instanceid |
| OutFlow          | Private network outbound traffic                                                   | MB/s  | instanceid |
| OutBandwidthUtil | Ratio of the actually used private network outbound traffic to the maximum traffic                               | %     | instanceid |
| OutFlowLimit     | Number of times that throttling is triggered by the outbound traffic                                         | -    | instanceid |
| LatencyMax       | Maximum execution latency from proxy to Redis server                      | ms    | instanceid |
| LatencyAvg       | Average execution latency from proxy to Redis server                      | ms    | instanceid |
| LatencyRead      | Average execution latency of read commands from proxy to Redis server | ms    | instanceid |
| LatencyWrite     | Average execution latency of write commands from proxy to Redis server | ms    | instanceid |
| LatencyOther     | Average execution latency of commands other than read and write commands from proxy to Redis server | ms    | instanceid |
| Commands         | QPS (command executions)                                            | Executions/sec | instanceid |
| CmdRead          | Number of read command executions | Executions/sec | instanceid |
| CmdWrite         | Number of write command executions | Executions/sec | instanceid |
| CmdOther         | Number of executions of commands other than read and write commands | Executions/sec | instanceid |
| CmdBigValue      | Number of executions for which the request size exceeds 32 KB                               | Executions/sec | instanceid |
| CmdKeyCount      | Number of keys accessed by commands                                          | Keys/sec | instanceid |
| CmdMget          | Number of Mget command executions                                            | Executions/sec | instanceid |
| CmdSlow | Number of commands whose execution latency is greater than the configured `slowlog-log-slower-than` value | - | instanceid |
| CmdHits          | Number of existent read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command | -    | instanceid |
| CmdMiss          | Number of non-existent read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command | -    | instanceid |
| CmdErr           | Number of command execution errors, such as when a command does not exist or a parameter is incorrect           | -    | instanceid |
| CmdHitsRatio     | Key hits/(key hits + key misses). This metric can reflect the situation of cache miss | %     | instanceid |
| CpuMaxUtil       | Maximum CPU utilization of nodes (shards or replicas) in the instance                    | %     | instanceid |
| MemMaxUtil       | Maximum memory utilization of nodes (shards or replicas) in the instance                     | %     | instanceid |

### Redis node 

| Metric | Description | Unit | Dimension |
| ------------------- | ------------------------------------------------------------ | ----- | ------------------- |
| MemUsedNode         | Memory capacity actually used, including data and cache                         | MB    | instanceid, rnodeid |
| ConnectionsNode     | Number of connections from proxy to node                                     | -    | instanceid, rnodeid |
| ConnectionsUtilNode | Node connection utilization                                             | %     | instanceid, rnodeid |
| CpuUtilNode         | Average CPU utilization                                              | %     | instanceid, rnodeid |
| MemUtilNode         | Ratio of the memory actually used to the total memory requested                                 | %     | instanceid, rnodeid |
| KeysNode            | Total number of keys stored in the instance (first-level keys)                            | -    | instanceid, rnodeid |
| ExpiredNode         | Number of keys that expired in the time window, which corresponds to the `expired_keys` output by the `info` command | -    | instanceid, rnodeid |
| EvictedNode         | Number of keys evicted in the time window, which corresponds to the `evicted_keys` output by the `info` command | -    | instanceid, rnodeid |
| ReplDelayNode       | Command lag from replica node to primary node                             | B     | instanceid, rnodeid |
| CommandsNode        | QPS (command executions)                                            | Executions/sec | instanceid, rnodeid |
| CmdReadNode         | Number of read command executions | Executions/sec | instanceid, rnodeid |
| CmdWriteNode         | Number of write command executions | Executions/sec | instanceid, rnodeid |
| CmdOtherNode        | Number of executions of commands other than read and write commands | Executions/sec | instanceid, rnodeid |
| CmdSlowNode         | Number of commands whose execution latency is greater than the configured `slowlog-log-slower-than` value          | -    | instanceid, rnodeid |
| CmdHitsNode         | Number of existent read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command | -    | instanceid, rnodeid |
| CmdMissNode         | Number of non-existent read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command | -    | instanceid, rnodeid |
| CmdHitsRatioNode    | Key hits/(key hits + key misses). This metric can reflect the situation of cache miss | %     | instanceid, rnodeid |

### Proxy node 

| Metric | Description | Unit | Dimension |
| --------------------- | ------------------------------------------------------------ | ----- | ------------------- |
| CpuUtilProxy          | Proxy CPU utilization                                             | %     | instanceid, pnodeid |
| CommandsProxy         | Number of commands executed by proxy                                           | Commands/sec | instanceid, pnodeid |
| CmdKeyCountProxy      | Number of keys accessed by commands                                          | Keys/sec | instanceid, pnodeid |
| CmdMgetProxy          | Number of Mget command executions                                            | Executions/sec | instanceid, pnodeid |
| CmdErrProxy           | Number of proxy command execution errors, such as when a command does not exist or a parameter is incorrect     | Errors/sec | instanceid, pnodeid |
| CmdBigValueProxy      | Number of executions for which the request size exceeds 32 KB                               | Executions/sec | instanceid, pnodeid |
| ConnectionsProxy      | Number of TCP connections to the instance                                    | -    | instanceid, pnodeid |
| InFlowProxy           | Private network inbound traffic                                                   | MB/s  | instanceid, pnodeid |
| OutFlowProxy          | Private network outbound traffic                                                   | MB/s  | instanceid, pnodeid |
| ConnectionsUtilProxy  | Connection utilization                                                 | %     | instanceid, pnodeid |
| InBandwidthUtilProxy  | Ratio of the actually used private network inbound traffic to the maximum traffic                               | %     | instanceid, pnodeid |
| OutBandwidthUtilProxy | Ratio of the actually used private network outbound traffic to the maximum traffic                               | %     | instanceid, pnodeid |
| InFlowLimitProxy      | Number of times that throttling is triggered by the inbound traffic                                         | -    | instanceid, pnodeid |
| OutFlowLimitProxy     | Number of times that throttling is triggered by the outbound traffic                                         | -    | instanceid, pnodeid |
| LatencyAvgProxy       | Average execution latency from proxy to Redis server                      | ms    | instanceid, pnodeid |
| LatencyMaxProxy       | Maximum execution latency from proxy to Redis server                      | ms    | instanceid, pnodeid |
| LatencyReadProxy      | Average execution latency of read commands from proxy to Redis server | ms    | instanceid, pnodeid |
| LatencyWriteProxy     | Average execution latency of write commands from proxy to Redis server | ms    | instanceid, pnodeid |
| LatencyOtherProxy     | Average execution latency of commands other than read and write commands from proxy to Redis server | ms    | instanceid, pnodeid |

## Overview of Parameters in Each Dimension

| Parameter | Dimension | Dimension Description | Format |
| ------------------------------ | ---------- | ------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | instanceid | Instance ID dimension name    | Enter a String-type dimension name: instanceid                         |
| Instances.N.Dimensions.0.Value | instanceid | Specific instance ID         | Enter a specific Redis instance ID such as `tdsql-123456` or instance SN such as `crs-ifmymj41`, which can be queried by calling the [DescribeInstances](https://intl.cloud.tencent.com/zh/document/product/239/32065) API |
| Instances.N.Dimensions.1.Name  | rnodeid    | Redis node ID dimension name | Enter a String-type dimension name: rnodeid        |
| Instances.N.Dimensions.1.Value | rnodeid    | Specific Redis node ID     | Enter a specific Redis node ID, which can be obtained by calling the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/zh/document/product/239/38627) API |
| Instances.N.Dimensions.1.Name  | pnodeid    | Proxy node ID dimension name | Enter a String-type dimension name: pnodeid   |
| Instances.N.Dimensions.1.Value | pnodeid    | Specific proxy node ID     | Enter a specific proxy node ID, which can be obtained by calling the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/zh/document/product/239/38627) API |

## Input Parameter Description

**To query the monitoring data of a TencentDB for Redis Memory Edition instance, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=instance ID

**To query the monitoring data of a Redis node of a TencentDB for Redis Memory Edition instance, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=rnodeid 
&Instances.N.Dimensions.1.Value=Redis node ID

**To query the monitoring data of a proxy node of a TencentDB for Redis Memory Edition instance, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=pnodeid
&Instances.N.Dimensions.1.Value=Proxy node ID

