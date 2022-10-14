## Namespace

Namespace = QCE/REDIS_MEM

## Monitoring Metrics


### Instance monitoring

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------- | ------------------- | ------------------------------------------------------------ | ----- | ---------- | -------------------------------- |
| CpuUtil          | CPU utilization          | The average CPU utilization                                              | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s |
| CpuMaxUtil       | Max CPU utilization of node | The maximum among all node (shard or replica) CPU utilizations in an instance                    | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| MemUsed          | Used memory          | The actually used memory capacity, including the capacity for data and cache                         | MB    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| MemUtil          | Memory utilization          | The ratio of the actually used memory to the requested total memory                                 | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| MemMaxUtil       | Max memory utilization of node  | The maximum among all node (shard or replica) memory utilizations in an instance                     | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| Keys             | Total keys          | The total number of keys (level-1 keys) stored in the instance                            | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| Expired          | Expired keys          | The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| Evicted          | Evicted keys          | The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| Connections      | Connections            | The number of TCP connections to the instance                                    | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| ConnectionsUtil  | Connection utilization          | The ratio of the number of TCP connections to the maximum number of connections                              | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| InFlow           | Inbound traffic              | The private network inbound traffic                                                   | Mb/s  | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| InBandwidthUtil  | Inbound traffic utilization        | The ratio of the actually used private inbound traffic to the maximum traffic                               | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| InFlowLimit      | Inbound traffic limit count      | The number of times inbound traffic triggers a traffic limit                                         | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| OutFlow          | Outbound traffic              | The private network outbound traffic                                                  | Mb/s  | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| OutBandwidthUtil | Outbound traffic utilization        | The ratio of the actually used private outbound traffic to the maximum traffic                               | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| OutFlowLimit     | Outbound traffic limit count      | The number of times outbound traffic triggers a traffic limit                                         | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyAvg       | Average execution latency        | The average execution latency between the proxy and the Redis server                       | ms    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyMax       | Max execution latency        | The maximum execution latency between the proxy and the Redis server                       | ms    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyRead      | Average read latency          | The average execution latency of read commands between the proxy and the Redis server                   | ms    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyWrite     | Average write latency          | The average execution latency of write commands between the proxy and the Redis server                   | ms    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyOther     | Average latency of other commands    | The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server       | ms    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| Commands         | Total requests              | The QPS, that is, the number of command executions per second                                            | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdRead          | Read requests              | The number of read command executions per second                                           | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdWrite         | Write requests              | The number of write command executions per second                                           | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdOther         | Other requests            | The number of command (excluding write and read commands) executions per second                               | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdBigValue      | Big value requests       | The number of executions of requests larger than 32 KB per second                           | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdKeyCount      | Key requests          | The number of keys accessed by a command per second                                          | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdMget          | MGET requests         | The number of MGET commands executed per second                                           | Count/sec | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdSlow          | Slow queries              | The number of command executions with a latency greater than the configured `slowlog-log-slower-than` value    | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdHits          | Read request hits          | The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdMiss          | Read request misses          | The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdErr           | Execution errors            | The number of command execution errors. For example, the command does not exist, or parameters are incorrect.         | -    | instanceid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdHitsRatio     | Read request hit rate        | Key hits/(key hits + key misses). This metric reflects cache misses. | %     | instanceid | 5s, 60s, 300s, 3600s, 86400s     |


#### Latency metrics (command dimension)
| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ---------------- | ------------------- | ------------------------------------------------------------ | ----- | ---------- | -------------------------------- |
| QpsCommand     | Command executions per second  | The number of commands executed per second                                             | %     | instanceid, command | 5s, 60s, 300s, 3600s, 86400s |
| LatencyAvgCommand   | Average execution latency	  | The average execution latency between the proxy and the Redis server	                                  | %     | instanceid, command | 5s, 60s, 300s, 3600s, 86400s |
| LatencyMaxCommand | Max execution delay    | The maximum execution latency between the proxy and the Redis server                                       | %     | instanceid, command| 5s, 60s, 300s, 3600s, 86400s |
|LatencyP99Command | P99 latency       | The P99 execution latency between the proxy and the Redis server                                    | %     | instanceid, command| 5s, 60s, 300s, 3600s, 86400s |


### Proxy node monitoring

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| --------------------- | ---------------- | ---------------------------------------------------------- | ----- | ------------------- | ---------------------------- |
| CpuUtilProxy          | CPU utilization       | The CPU utilization of the proxy                                           | %     | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s |
| CommandsProxy         | Total requests           | The number of proxy commands executed per second                                         | Count/sec | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s |
| CmdKeyCountProxy      | Key requests          | The number of keys accessed by a command per second                                          | Count/sec | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdMgetProxy          | MGET requests         | The number of MGET commands executed per second                                           | Count/sec | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdErrProxy           | Execution errors            | The number of proxy command execution errors. For example, the command does not exist, or parameters are incorrect.         | -    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdBigValueProxy      | Big value requests       | The number of executions of requests larger than 32 KB per second                           | Count/sec | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| ConnectionsProxy      | Connections            | The number of TCP connections to the instance                                    | -    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| ConnectionsUtilProxy  | Connection utilization          | The ratio of the number of TCP connections to the maximum number of connections                              | %     | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| InFlowProxy           | Inbound traffic              | The private network inbound traffic                                                   | Mb/s  | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| InBandwidthUtilProxy  | Inbound traffic utilization        | The ratio of the actually used private inbound traffic to the maximum traffic                               | %     | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| InFlowLimitProxy      | Inbound traffic limit count      | The number of times inbound traffic triggers a traffic limit                                         | -    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| OutFlowProxy          | Outbound traffic              | The private network outbound traffic                                                  | Mb/s  | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| OutBandwidthUtilProxy | Outbound traffic utilization        | The ratio of the actually used private outbound traffic to the maximum traffic                               | %     | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| OutFlowLimitProxy     | Outbound traffic limit count      | The number of times outbound traffic triggers a traffic limit                                         | -    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyAvgProxy       | Average execution latency        | The average execution latency between the proxy and the Redis server                       | ms    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyMaxProxy       | Max execution latency        | The maximum execution latency between the proxy and the Redis server                       | ms    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyReadProxy      | Average read latency          | The average execution latency of read commands between the proxy and the Redis server                   | ms    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyWriteProxy     | Average write latency          | The average execution latency of write commands between the proxy and the Redis server                   | ms    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| LatencyOtherProxy     | Average latency of other commands    | The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server       | ms    | instanceid, pnodeid | 5s, 60s, 300s, 3600s, 86400s     |


### Redis node monitoring

| Parameter | Metric Name | Description | Unit | Dimension | Statistical Period |
| ------------------- | ------------ | ------------------------------------------------------------ | ----- | ------------------- | ---------------------------- |
| CpuUtilNode          | CPU utilization          | The average CPU utilization                                              | %     | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s |
| ConnectionsNode      | Connections            | The number of connections from the proxy to the node                                    | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| ConnectionsUtilNode | Connection utilization   | The utilization of node connections                                             | %     | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s |
| MemUsedNode          | Used memory          | The actually used memory capacity, including the capacity for data and cache                         | MB    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| MemUtilNode          | Memory utilization          | The ratio of the actually used memory to the requested total memory                                 | %     | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| KeysNode             | Total keys          | The total number of keys (level-1 keys) stored in the instance                            | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| ExpiredNode          | Expired keys          | The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| EvictedNode          | Evicted keys          | The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| ReplDelayNode       | Replication delay     | The command delay between the replica node and the master node                             | Byte  | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s |
| CommandsNode         | Total requests              | The QPS, that is, the number of command executions per second                                            | Count/sec | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdReadNode          | Read requests              | The number of read command executions per second                                           | Count/sec | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdWriteNode         | Write requests              | The number of write command executions per second                                           | Count/sec | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdOtherNode         | Other requests            | The number of command (excluding write and read commands) executions per second                               | Count/sec | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdSlowNode          | Slow queries              | The number of command executions with a latency greater than the configured `slowlog-log-slower-than` value    | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdHitsNode          | Read request hits          | The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdMissNode          | Read request misses          | The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command | -    | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |
| CmdHitsRatioNode     | Read request hit rate        | Key hits/(key hits + key misses). This metric reflects cache misses. | %     | instanceid, rnodeid | 5s, 60s, 300s, 3600s, 86400s     |




## Dimensions and Parameters

| Parameter | Dimension | Description | Format |
| ------------------------------ | ---------- | ------------------- | ------------------------------------------------------------ |
| Instances.N.Dimensions.0.Name  | instanceid | Dimension name of the instance ID    | Enter a string-type dimension name: instanceid                         |
| Instances.N.Dimensions.0.Value | instanceid | Specific instance ID         | Enter a specific Redis instance ID, such as `tdsql-123456`, which can be queried through the [DescribeInstances](https://www.tencentcloud.com/document/product/239/32065) API and can also be an instance string such as `crs-ifmymj41`.  |
| Instances.N.Dimensions.1.Name  | rnodeid    | Dimension name of the Redis node ID | Enter a string-type dimension name: rnodeid        |
| Instances.N.Dimensions.1.Value | rnodeid    | Specific Redis node ID     | Enter a specific Redis node ID, which can be queried through the [DescribeInstanceNodeInfo](https://www.tencentcloud.com/document/product/239/38627) API. |
| Instances.N.Dimensions.1.Name  | pnodeid    | Dimension name of the proxy node ID | Enter a string-type dimension name: pnodeid   |
| Instances.N.Dimensions.1.Value | pnodeid    | Specific proxy node ID     | Enter a specific proxy node ID, which can be queried through the [DescribeInstanceNodeInfo](https://www.tencentcloud.com/document/product/239/38627) API. |
| Instances.N.Dimensions.1.Name  |command   | Dimension name of the command word | Enter a string-type dimension name: command  |
| Instances.N.Dimensions.1.Value | command   |   Specific command word | Enter a specific command word, such as `ping` and `get` |

## Input Parameters

**To query the monitoring data of a TencentDB for Redis instance, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID

**To query the monitoring data of a TencentDB proxy node, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=pnodeid
&Instances.N.Dimensions.1.Value=Proxy node ID

**To query the monitoring data of a TencentDB for Redis node, use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=rnodeid 
&Instances.N.Dimensions.1.Value=Redis node ID

**To query the monitoring data of TencentDB for Redis latency metrics (command dimension), use the following input parameters:**
&Namespace=QCE/REDIS_MEM
&Instances.N.Dimensions.0.Name=instanceid
&Instances.N.Dimensions.0.Value=Instance ID
&Instances.N.Dimensions.1.Name=command
&Instances.N.Dimensions.1.Value=Specific command word
