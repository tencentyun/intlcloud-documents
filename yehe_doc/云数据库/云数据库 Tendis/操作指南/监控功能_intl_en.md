TencentDB for Tendis provides a complete and easy-to-use monitoring service where you don’t have to worry about, for example, collecting monitoring data or OPS of the monitoring system. The monitoring service includes Proxy monitoring, Redis monitoring, and Tendis monitoring which summarizes the monitoring data of an entire instance. Details are as follows:
- Proxy monitoring: provides monitoring information of all Proxy nodes in an instance. TencentDB for Tendis instances in standard or cluster architecture have Proxy nodes.
- Redis monitoring: provides monitoring information of TencentDB for Tendis primary and secondary nodes.
- Tendis monitoring: summarizes the monitoring data of an entire instance (including Proxy nodes and Tendis nodes) and aggregates data according to the SUM, AVG, MAX, and LAST aggregation algorithms.
![](https://main.qcloudimg.com/raw/8a4553ef858c749d70549f9e16c7eb4f.png)

## Monitoring Granularity and Monitoring Data Retention Period
Tendis currently supports monitoring metrics at the 1-minute, 5-minutes, 1-hour, or 1-day granularity. For the retention period of monitoring data at each granularity, please see [Use Limits](https://intl.cloud.tencent.com/document/product/248/32803).

## Viewing Monitoring Information
You can view TencentDB for Tendis monitoring information in the instance list and on the instance monitoring page in the TencentDB for Tendis console, or in the Cloud Monitor console.
- Instance list: log in to the [TencentDB for Tendis console](https://console.cloud.tencent.com/tendis), click the **View Monitoring** icon in the instance list as shown below, and view monitoring metrics in the pop-up window on the right.
![](https://main.qcloudimg.com/raw/1bf892252c14a40f0162228ac28cc801.png)
- Instance monitoring page: log in to the [TencentDB for Tendis console](https://console.cloud.tencent.com/tendis), click an instance ID in the instance list and enter the instance management page, select **System Monitoring**, and view monitoring data on the **Monitoring Metrics** tab.
![](https://main.qcloudimg.com/raw/6d293d768113036c6cacd4a46172a2c6.png)

## Monitoring Metric Description
### Proxy monitoring
Each Tendis instance contains at least 3 Proxy nodes. Generally, the number of Proxy nodes is 1.5 times that of Tendis nodes. The Proxy node supports the following monitoring metrics:

<table>
<thead>
<tr><th>Category</th><th>Metric</th><th>Parameter</th><th>Unit</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>CPU</td>
<td>CPU utilization</td>
<td>cpu_util</td>
<td>%</td>
<td>Proxy CPU utilization</td>
</tr>
<tr>
<td rowspan=5>Request</td>
<td>Total requests</td>
<td>proxy_commands</td>
<td>requests/second</td>
<td>The number of Proxy command executions per second</td>
</tr>
<tr>
<td>Key requests</td>
<td>cmd_key_count</td>
<td>keys/second</td>
<td>The number of keys accessed by a command per second</td>
</tr>
<tr>
<td>Mget requests</td>
<td>cmd_mget</td>
<td>requests/second</td>
<td>The number of Mget command executions per second</td>
</tr>
<tr>
<td>Execution errors</td>
<td>cmd_err</td>
<td>errors/second</td>
<td>The number of Proxy command execution errors per second, for example, when a command does not exist, parameters are incorrect, etc.</td>
</tr>
<tr>
<td>Big value requests</td>
<td>cmd_big_value</td>
<td>requests/second</td>
<td>The number of executions of commands larger than 32 KB per second</td>
</tr>
<tr>
<td rowspan=8>Network</td>
<td>Connections</td>
<td>connections</td>
<td> - </td>
<td>The number of TCP connections to an instance</td>
</tr>
<tr>
<td>Connection usage</td>
<td>connections_util</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td>
</tr>
<tr>
<td>Inbound traffic</td>
<td>in_flow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td>
</tr>
<tr>
<td>Inbound traffic utilization</td>
<td>in_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td>
</tr>
<tr>
<td>Inbound traffic limit count</td>
<td>in_flow_limit</td>
<td> - </td>
<td>The number of times inbound traffic triggers a traffic limit</td>
</tr>
<tr>
<td>Outbound traffic</td>
<td>out_flow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td>
</tr>
<tr>
<td>Outbound traffic utilization</td>
<td>out_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td>
</tr>
<tr>
<td>Outbound traffic limit count</td>
<td>out_flow_limit</td>
<td> - </td>
<td>The number of times outbound traffic triggers a traffic limit</td>
</tr>
<tr>
<td rowspan=5>Latency</td>
<td>Average execution latency</td>
<td>latency_avg</td>
<td>ms</td>
<td>The average execution latency from Proxy to Redis server</td>
</tr>
<tr>
<td>Max execution latency</td>
<td>latency_max</td>
<td>ms</td>
<td>The maximum execution latency from Proxy to Redis server</td>
</tr>
<tr>
<td>Average read latency</td>
<td>latency_read</td>
<td>ms</td>
<td>The average execution latency of read commands from Proxy to Redis server. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Average write latency</td>
<td>latency_write</td>
<td>ms</td>
<td>The average execution latency of write commands from Proxy to Redis server. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Average latency of other commands</td>
<td>latency_other</td>
<td>ms</td>
<td>The average execution latency of commands other than read and write commands from Proxy to Redis server</td>
</tr>
</tbody></table>

### Redis monitoring
The Redis node monitoring includes monitoring information of all primary nodes and secondary nodes in an instance or a cluster. The following monitoring metrics are supported.

<table>
<thead>
<tr><th>Category</th><th>Metric</th><th>Parameter</th><th>Unit</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td>CPU</td>
<td>CPU utilization</td>
<td>cpu_util</td>
<td>%</td>
<td>Average CPU utilization</td>
</tr>
<tr>
<td  rowspan=2>Network</td>
<td>Connections</td>
<td>connections</td>
<td> - </td>
<td>The number of connections from Proxy to a node</td>
</tr>
<tr>
<td>Connection usage</td>
<td>connections_util</td>
<td>%</td>
<td>The connection usage of a node</td>
</tr>
<tr>
<td  rowspan=6>Memory</td>
<td>Used memory</td>
<td>mem_used</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td>
</tr>
<tr>
<td>Memory utilization</td>
<td>mem_util</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td>
</tr>
<tr>
<td>Keys</td>
<td>keys</td>
<td> - </td>
<td>Total number of keys stored in an instance (first-level keys)</td>
</tr>
<tr>
<td>Expired keys</td>
<td>expired</td>
<td> - </td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command</td>
</tr>
<tr>
<td>Evicted keys</td>
<td>evicted</td>
<td> - </td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command</td>
</tr>
<tr>
<td>Replication delay</td>
<td>repl_delay</td>
<td>Byte</td>
<td>The command delay between the secondary node and the primary node</td>
</tr>
<tr>
<td  rowspan=4>Request</td>
<td>Total requests</td>
<td>commands</td>
<td>queries/second</td>
<td>QPS, that is, the number of command executions per second</td>
</tr>
<tr>
<td>Read requests</td>
<td>cmd_read</td>
<td>requests/second</td>
<td>The number of read command executions per second. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Write requests</td>
<td>cmd_write</td>
<td>requests/second</td>
<td>The number of write command executions per second. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Other requests</td>
<td>cmd_other</td>
<td>requests/second</td>
<td>The number of command (excluding write and read commands) executions per second</td>
</tr>
<tr>
<td  rowspan=4>Response</td>
<td>Slow queries</td>
<td>cmd_slow</td>
<td> - </td>
<td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td>
</tr>
<tr>
<td>Read request hits</td>
<td>cmd_hits</td>
<td> - </td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td>
</tr>
<tr>
<td>Read request misses</td>
<td>cmd_miss</td>
<td> - </td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td>
</tr>
<tr>
<td>Read request hit rate</td>
<td>cmd_hits_ratio</td>
<td>%</td>
<td>Key hits/(Key hits + Key misses). This metric reflects the cache miss situation.</td>
</tr>
</tbody></table>

### Tendis monitoring
The Tendis monitoring includes all monitoring data of an instance, including the monitoring data of Proxy nodes and Redis nodes, which is aggregated by the SUM, AVG, MAX, and LAST algorithms.

<table>
<thead>
<tr><th>Category</th><th>Metric</th><th>Associated Node View</th><th>Parameter</th><th>Unit</th><th>Description</th></tr>
</thead>
<tbody><tr>
<td  rowspan=2>CPU</td>
<td>CPU utilization</td>
<td>Tendis node</td>
<td>cpu_util</td>
<td>%</td>
<td>Average CPU utilization</td>
</tr>
<tr>
<td>Max CPU utilization of a node</td>
<td>Tendis node</td>
<td>cpu_max_util</td>
<td>%</td>
<td>The maximum CPU utilization of a node (shard or replica) in an instance</td>
</tr>
<tr>
<td  rowspan=6>Memory</td>
<td>Used memory</td>
<td>Tendis node</td>
<td>mem_used</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td>
</tr>
<tr>
<td>Memory utilization</td>
<td>Tendis node</td>
<td>mem_util</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td>
</tr>
<tr>
<td>Max memory utilization of a node</td>
<td>Tendis node</td>
<td>mem_max_util</td>
<td>%</td>
<td>The maximum memory utilization of a node (shard or replica) in an instance</td>
</tr>
<tr>
<td>Keys</td>
<td>Tendis node</td>
<td>keys</td>
<td> - </td>
<td>Total number of keys stored in an instance (first-level keys)</td>
</tr>
<tr>
<td>Expired keys</td>
<td>Tendis node</td>
<td>expired</td>
<td> - </td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command</td>
</tr>
<tr>
<td>Evicted keys</td>
<td>Tendis node</td>
<td>evicted</td>
<td> - </td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command</td>
</tr>
<tr>
<td  rowspan=13>Network</td>
<td>Connections</td>
<td>Proxy node</td>
<td>connections</td>
<td> - </td>
<td>The number of TCP connections to an instance</td>
</tr>
<tr>
<td>Connection usage</td>
<td>Proxy node</td>
<td>connections_util</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td>
</tr>
<tr>
<td>Inbound traffic</td>
<td>Proxy node</td>
<td>in_flow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td>
</tr>
<tr>
<td>Inbound traffic utilization</td>
<td>Proxy node</td>
<td>in_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td>
</tr>
<tr>
<td>Inbound traffic limit count</td>
<td>Proxy node</td>
<td>in_flow_limit</td>
<td> - </td>
<td>The number of times inbound traffic triggers a traffic limit</td>
</tr>
<tr>
<td>Outbound traffic</td>
<td>Proxy node</td>
<td>out_flow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td>
</tr>
<tr>
<td>Outbound traffic utilization</td>
<td>Proxy node</td>
<td>out_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td>
</tr>
<tr>
<td>Outbound traffic limit count</td>
<td>Proxy node</td>
<td>out_flow_limit</td>
<td> - </td>
<td>The number of times outbound traffic triggers a traffic limit</td>
</tr>
<tr>
<td>Average execution latency</td>
<td>Proxy node</td>
<td>latency_avg</td>
<td>ms</td>
<td>Average execution latency from Proxy to Redis server</td>
</tr>
<tr>
<td>Max execution latency</td>
<td>Proxy node</td>
<td>latency_max</td>
<td>ms</td>
<td>Maximum execution latency from Proxy to Redis server</td>
</tr>
<tr>
<td>Average read latency</td>
<td>Proxy node</td>
<td>latency_read</td>
<td>ms</td>
<td>The average execution latency of read commands from Proxy to Redis server. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Average write latency</td>
<td>Proxy node</td>
<td>latency_write</td>
<td>ms</td>
<td>The average execution latency of write commands from Proxy to Redis server. For more information about wirte command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Average latency of other commands</td>
<td>Proxy node</td>
<td>latency_other</td>
<td>ms</td>
<td>The average execution latency of commands other than read and write commands from Proxy to Redis server</td>
</tr>
<tr>
<td  rowspan=12>Request</td>
<td>Total requests</td>
<td>Tendis node</td>
<td>commands</td>
<td>requests/second</td>
<td>QPS, that is, the number of command executions per second</td>
</tr>
<tr>
<td>Read requests</td>
<td>Tendis node</td>
<td>cmd_read</td>
<td>requests/second</td>
<td>The number of read command executions per second. For more information about read command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Write requests</td>
<td>Tendis node</td>
<td>cmd_write</td>
<td>requests/second</td>
<td>The number of write command executions per second. For more information about write command types, please see <a href="#mlfl">Command types</a>.</td>
</tr>
<tr>
<td>Other requests</td>
<td>Tendis node</td>
<td>cmd_other</td>
<td>requests/second</td>
<td>The number of command (excluding write and read commands) executions per second</td>
</tr>
<tr>
<td>Big value requests</td>
<td>Proxy node</td>
<td>cmd_big_value</td>
<td>requests/second</td>
<td>The number of executions of commands larger than 32 KB per second</td>
</tr>
<tr>
<td>Key requests</td>
<td>Proxy node</td>
<td>cmd_key_count</td>
<td>keys/second</td>
<td>The number of keys accessed by a command per second</td>
</tr>
<tr>
<td>Mget requests</td>
<td>Proxy node</td>
<td>cmd_mget</td>
<td>requests/second</td>
<td>The number of Mget command executions per second</td>
</tr>
<tr>
<td>Slow queries</td>
<td>Tendis node</td>
<td>cmd_slow</td>
<td> - </td>
<td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td>
</tr>
<tr>
<td>Read request hits</td>
<td>Tendis node</td>
<td>cmd_hits</td>
<td> - </td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td>
</tr>
<tr>
<td>Read request misses</td>
<td>Tendis node</td>
<td>cmd_miss</td>
<td> - </td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td>
</tr>
<tr>
<td>Execution errors</td>
<td>Proxy node</td>
<td>cmd_err</td>
<td> - </td>
<td>The number of command execution errors, for example, when a command does not exist, parameters are incorrect, etc.</td>
</tr>
<tr>
<td>Read request hit rate</td>
<td>Tendis node</td>
<td>cmd_hits_ratio</td>
<td>%</td>
<td>Key hits/(Key hits + Key misses). This metric reflects the cache miss situation.</td>
</tr>
</tbody></table>

<span id = "mlfl"></span>
### Command types

| Type | Commands                                                         |
| -------- | ------------------------------------------------------------ |
| Read command   | get, strlen, exists, getbit, getrange, substr, mget, llen, lindex, lrange, sismember, scard, srandmember,<br>sinter, sunion, sdiff, smembers, sscan, zrange, zrangebyscore, zrevrangebyscore, zrangebylex,<br>zrevrangebylex, zcount, zlexcount, zrevrange, zcard, zscore, zrank, zrevrank, zscan, hget, hmget,<br>hlen, hstrlen, hkeys, hvals, hgetall, hexists, hscan, randomkey, keys, scan, dbsize, type, ttl, touch, pttl,<br>dump, object, memory, bitcount, bitpos, georadius_ro, georadiusbymember_ro, geohash, geopos, geodist, pfcount |
| Write command   | set, setnx, setex, psetex, append, del, unlink, setbit, bitfield, setrange, incr, decr, rpush, lpush, rpushx,<br>lpushx, linsert, rpop, lpop, brpop, brpoplpush, blpop, lset, ltrim, lrem, rpoplpush, sadd, srem, smove, spop,<br>sinterstore, sunionstore, sdiffstore, zadd, zincrby, zrem, zremrangebyscore, zremrangebyrank,<br>zremrangebylex, zunionstore, zinterstore, hset, hsetnx, hmset, hincrby, hincrbyfloat, hdel, incrby, decrby,<br>incrbyfloat, getset, mset, msetnx, swapdb, move, rename, renamenx, expire, expireat, pexpire, pexpireat,<br>flushdb, flushall, sort, persist, restore, restore-asking, migrate, bitop, geoadd, georadius, georadiusbymember,<br>pfadd, pfmerge, pfdebug |



