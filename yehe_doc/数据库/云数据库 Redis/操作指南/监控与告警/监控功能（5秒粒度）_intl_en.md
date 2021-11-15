TencentDB for Redis provides a complete and easy-to-use monitoring service where you don’t have to worry about, for example, collecting monitoring data or OPS of the monitoring system. The monitoring service includes Proxy monitoring, Redis monitoring, and instance monitoring which summarizes the monitoring data of an entire instance.
- Proxy monitoring: provides monitoring information of all Proxy nodes in an instance. TencentDB for Redis instances in standard or cluster architecture have Proxy nodes.
- Redis monitoring: provides monitoring information of master and replica Redis nodes.
- Instance monitoring: summarizes the monitoring data of an entire instance (including Proxy nodes and Proxy nodes) and aggregates data according to the SUM, AVG, MAX, and LAST aggregation algorithms.
![](https://main.qcloudimg.com/raw/2ff4346f6da8cfec08adb7bbdd331455.png)
## Description of the Five-second Monitoring Granularity
- By default, new instances (excluding CKV instances) support five-second granularity.
- In the future, you can modify the monitoring granularity of existing instances from one minute to five seconds in the [TencentDB for Redis console](https://console.cloud.tencent.com/redis). Please pay attention to the notices and pop-up notifications in the console.
- In the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist/create), alarm policies for five-second granularity are of a different policy type from those for one-minute granularity. You can replicate the alarm policies for one-minute granularity and change their policy types to **Memory Edition (5-second granularity)**, so that these alarm policies can be associated with new instances supporting five-second granularity.
![](https://main.qcloudimg.com/raw/9bfa0b792d4c0ddc4b262ea5357575e3.png)
## Viewing Instance Monitoring Granularity
- Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID and enter the instance management page, select **System Monitoring** > **Monitoring Metrics**, and click the **Period** drop-down list at the top. If you can select **5 seconds** from the drop-down list, this instance supports the monitoring granularity of five seconds, or else it supports only the monitoring granularity of one minute.
![](https://main.qcloudimg.com/raw/e7833ebba07a4dd949c911c58940a4d0.png)
- Check the value of the `InstanceSet.MonitorVersion` field returned by the [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. If the value is `5s`, this instance supports the monitoring granularity of five seconds; if the value is `1m`, it supports only the monitoring granularity of one minute.

## Monitoring Granularity and Monitoring Data Retention Period
TencentDB for Redis currently supports monitoring metrics at the five-second, one-minute, five-minutes, one-hour, or one-day granularity. For the retention period of monitoring data at each granularity, please see [Use Limits](https://intl.cloud.tencent.com/document/product/248/32803).

## Viewing Monitoring Information
You can view TencentDB for Redis monitoring information in the instance list and on the instance monitoring page in the TencentDB for Redis console, or in the Cloud Monitor console.
- Instance list: log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click the **View Monitoring** icon in the instance list as shown below, and view monitoring metrics in the pop-up window on the right.
![](https://main.qcloudimg.com/raw/e4e9781c7dc38505a1e08624f72f9dff.png)
- Instance monitoring page: log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list and enter the instance management page, select **System Monitoring**, and view monitoring data on the **Monitoring Metrics** tab.
![](https://main.qcloudimg.com/raw/aba46b1c932f11f173634f596b1dd69f.png)
- Cloud Monitor console: log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/product/redis_mem_edition) to view the summary of monitoring data.
![](https://main.qcloudimg.com/raw/7289958cd8a4f4c8b4374d50031eb438.png)


## Monitoring Metric Description
### Proxy node monitoring
Each TencentDB for Redis instance contains at least 3 Proxy nodes. Generally, the number of Proxy nodes is 1.5 times that of Redis nodes. The Proxy node supports the following monitoring metrics:

<table>
<thead><tr><th>Category</th><th>Metric</th><th>Parameter</th><th>Unit</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>CPU</td><td>CPU utilization</td><td>cpu_util</td><td>%</td><td>Proxy CPU utilization</td></tr>
<tr>
<td rowspan=5>Request</td><td>Total requests</td><td>proxy_commands</td><td>requests/second</td><td>The number of proxy command executions per second</td></tr>
<tr>
<td>Key requests</td><td>cmd_key_count</td><td>keys/second</td><td>The number of keys accessed by a command per second</td></tr>
<tr>
<td>Mget requests</td><td>cmd_mget</td><td>requests/second</td><td>The number of Mget command executions per second</td></tr>
<tr>
<td>Execution errors</td><td>cmd_err</td><td>errors/second</td><td>The number of Proxy command execution errors per second. For example, the command does not exist, parameters are incorrect, etc.</td></tr>
<tr>
<td>Big value requests</td><td>cmd_big_value</td><td>requests/second</td><td>The number of executions of requests larger than 32 KB per second</td></tr>
<tr>
<td rowspan=8>Network</td><td>Connections</td><td>connections</td><td>-</td><td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connection utilization</td><td>connections_util</td><td>%</td><td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
<tr>
<td>Inbound traffic</td><td>in_flow</td><td>MB/s</td><td>Private inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td><td>in_bandwidth_util</td><td>%</td><td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>
<tr>
<td>Inbound traffic limit count</td><td>in_flow_limit</td><td>-</td><td>The number of times inbound traffic triggers a traffic limit</td></tr>
<tr>
<td>Outbound traffic</td><td>out_flow</td><td>MB/s</td><td>Private outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td><td>out_bandwidth_util</td><td>%</td><td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td>Outbound traffic limit count</td><td>out_flow_limit</td><td>-</td><td>The number of times outbound traffic triggers a traffic limit</td></tr>
<tr>
<td rowspan=5>Latency</td><td>Average execution latency</td><td>latency_avg</td><td>ms</td><td>The average execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Maximum execution latency</td><td>latency_max</td><td>ms</td><td>The maximum execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Average read latency</td><td>latency_read</td><td>ms</td><td>The average execution latency of read commands between the proxy and the Redis server. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Average write latency</td><td>latency_write</td><td>ms</td><td>The average execution latency of write commands between the proxy and the Redis server. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Average latency of other commands</td><td>latency_other</td><td>ms</td><td>The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server</td></tr>
</tbody></table>

### Redis node monitoring
The Redis node monitoring includes monitoring information of all master nodes and replica nodes in an instance or a cluster. The following monitoring metrics are supported:

<table>
<thead><tr><th>Category</th><th>Metric</th><th>Parameter</th><th>Unit</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>CPU</td><td>CPU utilization</td><td>cpu_util</td><td>%</td><td>Average CPU utilization</td></tr>
<tr>
<td  rowspan=2>Network</td><td>Connections</td><td>connections</td><td>-</td><td>The number of connections between the proxy and a node</td></tr>
<tr>
<td>Connection utilization</td><td>connections_util</td><td>%</td><td>The connection utilization of a node</td></tr>
<tr>
<td  rowspan=6>Memory</td><td>Used memory</td><td>mem_used</td><td>MB</td><td>Actually used memory capacity, including the capacity for data and cache</td></tr>
<tr>
<td>Memory utilization</td><td>mem_util</td><td>%</td><td>The ratio of the actually used memory to the requested total memory</td></tr>
<tr>
<td>Total keys</td><td>keys</td><td>-</td><td>The total number of keys (level-1 keys) in instance storage</td></tr>
<tr>
<td>Expired keys</td><td>expired</td><td>-</td><td>The number of keys expired in a time window, which is equal to the value of `expired_keys` outputted by the `info` command</td></tr>
<tr>
<td>Evicted keys</td><td>evicted</td><td>-</td><td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` outputted by the `info` command</td></tr>
<tr>
<td>Replication delay</td><td>repl_delay</td><td>Byte</td><td>The command delay between the replica node and the master node</td></tr>
<tr>
<td  rowspan=4>Request</td><td>Total requests</td><td>commands</td><td>requests/second</td><td>QPS, that is, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td><td>cmd_read</td><td>requests/second</td><td>The number of read command executions per second. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Write requests</td><td>cmd_write</td><td>requests/second</td><td>The number of write command executions per second. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Other requests</td><td>cmd_other</td><td>requests/second</td><td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td  rowspan=4>Response</td><td>Slow queries</td><td>cmd_slow</td><td>-</td><td>The number of command executions with a latency greater than the `slowlog\-log\-slower\-than` configuration</td></tr>
<tr>
<td>Read request hits</td><td>cmd_hits</td><td>-</td><td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td></tr>
<tr>
<td>Read request misses</td><td>cmd_miss</td><td>-</td><td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td></tr>
<tr>
<td>Read request hit rate</td><td>cmd_hits_ratio</td><td>%</td><td>Key hits/(Key hits + Key misses). This metric reflects cache misses.</td></tr>
</tbody></table>

### Instance monitoring
The instance monitoring includes all monitoring data of an instance, including the monitoring data of Proxy nodes and Redis nodes, which is aggregated by the SUM, AVG, MAX, and LAST algorithms.

<table>
<thead><tr><th>Category</th><th>Metric</th><th>Associated Node View</th><th>Parameter</th><th>Unit</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td  rowspan=2>CPU</td><td>CPU utilization</td><td>Redis node</td><td>cpu_util</td><td>%</td><td>Average CPU utilization</td></tr>
<tr>
<td>Maximum node CPU utilization</td><td>Redis node</td><td>cpu_max_util</td><td>%</td><td>The maximum among all node (shard or replica) CPU utilizations in an instance</td></tr>
<tr>
<td  rowspan=6>Memory</td><td>Used memory</td><td>Redis node</td><td>mem_used</td><td>MB</td><td>Actually used memory capacity, including the capacity for data and cache</td></tr>
<tr>
<td>Memory utilization</td><td>Redis node</td><td>mem_util</td><td>%</td><td>The ratio of the actually used memory to the requested total memory</td></tr>
<tr>
<td>Maximum node memory utilization</td><td>Redis node</td><td>mem_max_util</td><td>%</td><td>The maximum among all node (shard or replica) memory utilizations in an instance</td></tr>
<tr>
<td>Total keys</td><td>Redis node</td><td>keys</td><td>-</td><td>The total number of keys (level-1 keys) in instance storage</td></tr>
<tr>
<td>Expired keys</td><td>Redis node</td><td>expired</td><td>-</td><td>The number of keys expired in a time window, which is equal to the value of `expired_keys` outputted by the `info` command</td></tr>
<tr>
<td>Evicted keys</td><td>Redis node</td><td>evicted</td><td>-</td><td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` outputted by the `info` command</td></tr>
<tr>
<td  rowspan=13>Network</td><td>Connections</td><td>Proxy node</td><td>connections</td><td>-</td><td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connection utilization</td><td>Proxy node</td><td>connections_util</td><td>%</td><td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
<tr>
<td>Inbound traffic</td><td>Proxy node</td><td>in_flow</td><td>MB/s</td><td>Private inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td><td>Proxy node</td><td>in_bandwidth_util</td><td>%</td><td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>
<tr>
<td>Inbound traffic limit count</td><td>Proxy node</td><td>in_flow_limit</td><td>-</td><td>The number of times inbound traffic triggers a traffic limit</td></tr>
<tr>
<td>Outbound traffic</td><td>Proxy node</td><td>out_flow</td><td>MB/s</td><td>Private outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td><td>Proxy node</td><td>out_bandwidth_util</td><td>%</td><td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td>Outbound traffic limit count</td><td>Proxy node</td><td>out_flow_limit</td><td>-</td><td>The number of times outbound traffic triggers a traffic limit</td></tr>
<tr>
<td>Average execution latency</td><td>Proxy node</td><td>latency_avg</td><td>ms</td><td>The average execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Maximum execution latency</td><td>Proxy node</td><td>latency_max</td><td>ms</td><td>The maximum execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Average read latency</td><td>Proxy node</td><td>latency_read</td><td>ms</td><td>The average execution latency of read commands between the proxy and the Redis server. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Average write latency</td><td>Proxy node</td><td>latency_write</td><td>ms</td><td>The average execution latency of write commands between the proxy and the Redis server. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Average latency of other commands</td><td>Proxy node</td><td>latency_other</td><td>ms</td><td>The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server</td></tr>
<tr>
<td  rowspan=12>Request</td><td>Total requests</td><td>Redis node</td><td>commands</td><td>requests/second</td><td>QPS, that is, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td><td>Redis node</td><td>cmd_read</td><td>requests/second</td>
<td>The number of read command executions per second. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Write requests</td><td>Redis node</td><td>cmd_write</td><td>requests/second</td><td>The number of write command executions per second. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td></tr>
<tr>
<td>Other requests</td><td>Redis node</td><td>cmd_other</td><td>requests/second</td><td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td>Big value requests</td><td>Proxy node</td><td>cmd_big_value</td><td>requests/second</td><td>The number of executions of commands larger than 32 KB per second</td></tr>
<tr>
<td>Key requests</td><td>Proxy node</td><td>cmd_key_count</td><td>keys/second</td><td>The number of keys accessed by a command per second</td></tr>
<tr>
<td>Mget requests</td><td>Proxy node</td><td>cmd_mget</td><td>requests/second</td><td>The number of Mget command executions per second</td></tr>
<tr>
<td>Slow queries</td>
<td>Redis node</td><td>cmd_slow</td><td>-</td><td>The number of command executions with a latency greater than the `slowlog\-log\-slower\-than` configuration</td></tr>
<tr>
<td>Read request hits</td><td>Redis node</td><td>cmd_hits</td><td>-</td><td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td></tr>
<tr>
<td>Read request misses</td><td>Redis node</td><td>cmd_miss</td><td>-</td><td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td></tr>
<tr>
<td>Execution errors</td><td>Proxy node</td><td>cmd_err</td><td>-</td><td>The number of command execution errors. For example, the command does not exist, parameters are incorrect, etc.</td></tr>
<tr>
<td>Read request hit rate</td><td>Redis node</td><td>cmd_hits_ratio</td><td>%</td><td>Key hits/(Key hits + Key misses). This metric reflects cache misses.</td></tr>
</tbody></table>

### [Command types](id:mlfl)

| Type | Commands                                                         |
| -------- | ------------------------------------------------------------ |
| Read command   | get, strlen, exists, getbit, getrange, substr, mget, llen, lindex, lrange, sismember, scard, srandmember,<br>sinter, sunion, sdiff, smembers, sscan, zrange, zrangebyscore, zrevrangebyscore, zrangebylex,<br>zrevrangebylex, zcount, zlexcount, zrevrange, zcard, zscore, zrank, zrevrank, zscan, hget, hmget,<br>hlen, hstrlen, hkeys, hvals, hgetall, hexists, hscan, randomkey, keys, scan, dbsize, type, ttl, touch, pttl,<br>dump, object, memory, bitcount, bitpos, georadius_ro, georadiusbymember_ro, geohash, geopos, geodist, pfcount |
| Write command   | set, setnx, setex, psetex, append, del, unlink, setbit, bitfield, setrange, incr, decr, rpush, lpush, rpushx,<br>lpushx, linsert, rpop, lpop, brpop, brpoplpush, blpop, lset, ltrim, lrem, rpoplpush, sadd, srem, smove, spop,<br>sinterstore, sunionstore, sdiffstore, zadd, zincrby, zrem, zremrangebyscore, zremrangebyrank,<br>zremrangebylex, zunionstore, zinterstore, hset, hsetnx, hmset, hincrby, hincrbyfloat, hdel, incrby, decrby,<br>incrbyfloat, getset, mset, msetnx, swapdb, move, rename, renamenx, expire, expireat, pexpire, pexpireat,<br>flushdb, flushall, sort, persist, restore, restore-asking, migrate, bitop, geoadd, georadius, georadiusbymember,<br>pfadd, pfmerge, pfdebug |

## Querying Node Information
Use the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) API to get the IDs of Proxy nodes and Redis nodes.
>!The IDs of Proxy and Redis nodes will change when node failover, instance capacity expansion/reduction, data migration, etc., occur. Therefore, we recommend that you get the latest node information from the API in a timely manner.

