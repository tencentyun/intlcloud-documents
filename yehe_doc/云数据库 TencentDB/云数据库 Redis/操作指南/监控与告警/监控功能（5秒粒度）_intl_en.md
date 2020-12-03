TencentDB for Redis provides an imperceptible monitoring service. In the latest version, you can view the monitoring data of proxy nodes, Redis nodes, and instances at the granularity of five seconds.
- Proxy node monitoring: proxy nodes are used in TencentDB for Redis instances in the standard or cluster architectures. The proxy node monitoring view shows the monitoring data of all proxy nodes in an instance.
- Redis node monitoring: the Redis node monitoring view shows the monitoring data of Redis master nodes and Redis replica nodes.
- Instance monitoring: the instance monitoring view shows all monitoring data of an instance, including the monitoring data of proxy nodes and Redis nodes, which is aggregated by the SUM, AVG, MAX, and LAST algorithms.
![](https://main.qcloudimg.com/raw/ded170673a382efb790d4ff837fc0e2d.png)

## Description of the Five-Second Monitoring Granularity
- In the future, you can modify the monitoring granularity of existing instances from one minute to five seconds in the TencentDB for Redis console. We will notify you of when the modification becomes supported by notices and pop-up notifications in the [console](https://console.cloud.tencent.com/redis).
- In the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/policylist/create), alarm policies for five-second granularity are of a different policy type from those for one-minute granularity, as shown below. You can replicate the alarm policies for one-minute granularity and change their policy types to **Memory Edition (5-second granularity)**, so that these alarm policies can be associated with new instances supporting five-second granularity.
![](https://main.qcloudimg.com/raw/1f1078e7d1676425b20bc8849d242ac4.png)

## Viewing Instance Monitoring Granularity
- Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance name/ID and enter the instance management page, select **System Monitoring** > **Monitoring Metrics**, and click the **Period** drop-down list at the top. If you can select **5 seconds** from the drop-down list, this instance supports the monitoring granularity of five seconds, or else it supports the monitoring granularity of one minute.
![](https://main.qcloudimg.com/raw/19e0babb73bd59d10993c76ac295b197.png)
- Check the value of the `InstanceSet.MonitorVersion` field returned by the [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API. If the value is `5s`, this instance supports the monitoring granularity of five seconds; if the value is `1m`, it supports the monitoring granularity of one minute.

## Monitoring Granularity and Monitoring Data Retention Period
TencentDB for Redis currently supports monitoring metrics at the five-second, one-minute, five-minutes, one-hour, or one-day granularity. For the retention period of monitoring data at each granularity, please see [Use Limits](https://intl.cloud.tencent.com/document/product/248/32803).

## View Monitoring Data
You can view TencentDB for Redis monitoring data in the instance list and on the instance monitoring page in the TencentDB for Redis console, or in the Cloud Monitor console.
- Instance list: log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click the **View Monitoring** icon in the instance list, and view monitoring metrics in the pop-up window on the right.
![](https://main.qcloudimg.com/raw/654a5c1c2233f9b343522d0dfe66a0f4.png)
- Instance monitoring page: log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance name/ID and enter the instance management page, select **System Monitoring**, and view monitoring data on the **Monitoring Metrics** tab.
![](https://main.qcloudimg.com/raw/fe5085be982282309b0d28f870e63706.png)
- Cloud Monitor console: log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/product/redis_mem_edition) to view the summary of monitoring data.
![](https://main.qcloudimg.com/raw/5aa9c9c0f895454cbe981d8dfa770737.png)
	

## Description of Monitoring Metrics
### Proxy node monitoring
Each Redis instance contains at least 3 proxy nodes. Generally, the number of proxy nodes is 1.5 times that of Redis nodes. The proxy node supports the following monitoring metrics:

| Category     | Metric             | Parameter           | Unit  | Description                                                         |
| -------- | ---------------- | ------------------ | ----- | ------------------------------------------------------------ |
| CPU      | CPU utilization        | cpu_util           | %     | Proxy CPU utilization                                               |
| Request     | Total requests           | proxy_commands     | requests/second | The number of proxy command executions per second                                            |
| Request     | Key requests        | cmd_key_count      | keys/second | The number of keys accessed by a command per second                                            |
| Request     | Mget requests       | cmd_mget           | requests/second | The number of Mget command executions per second                                            |
| Request     | Execution errors         | cmd_err         | errors/second | The number of proxy command execution errors per second. For example, the command does not exist, parameters are incorrect, etc.      |
| Request       | Big value requests      | cmd_big_value      | requests/second | The number of executions of commands larger than 32 KB per second                               |
| Network | Connections         | connections        | -    | The number of TCP connections to an instance                                      |
| Network | Connection utilization       | connections_util   | %     | The ratio of the number of TCP connections to the maximum number of connections                                |
| Network | Inbound traffic           | in_flow            | MB/s  | Private inbound traffic                                                   |
| Network | Inbound traffic utilization     | in_bandwidth_util  | %     | The ratio of the actually used private inbound traffic to the maximum traffic                               |
| Network | Inbound traffic limit count   | in_flow_limit      | -    | The number of times inbound traffic triggers a traffic limit                                         |
| Network | Outbound traffic           | out_flow           | MB/s  | Private outbound traffic                                                   |
| Network | Outbound traffic utilization     | out_bandwidth_util  | %     | The ratio of the actually used private outbound traffic to the maximum traffic                               |
| Network | Outbound traffic limit count   | out_flow_limit      | -    | The number of times outbound traffic triggers a traffic limit                                         |
| Latency | Average execution latency     | latency_avg        | ms    | The average execution latency between the proxy and the Redis server                          |
| Latency | Max execution latency     | latency_max        | ms    | The maximum execution latency between the proxy and the Redis server                          |
| Latency |  Average read latency       | latency_read       | ms   | The average execution latency of read commands between the proxy and the Redis server. For more information about read command types, please see [Command types](#mlfl). |
| Latency |  Average write latency       | latency_write       | ms   | The average execution latency of write commands between the proxy and the Redis server. For more information about write command types, please see [Command types](#mlfl).  |
| Latency | Average latency of other commands | latency_other   | ms    | The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server  |

### Redis node monitoring
The Redis node monitoring includes monitoring information of all master nodes and replica nodes in an instance or a cluster. The following monitoring metrics are supported:

| Category     | Metric             | Parameter           | Unit  | Description                                                         |
| -------- | ------------ | ---------------- | ----- | ------------------------------------------------------------ |
| CPU  | CPU utilization    | cpu_util         | %     | Average CPU utilization                                                |
| Network     | Connections     | connections      | -    | The number of connections between the proxy and a node                                      |
| Network     | Connection utilization   | connections_util | %     | The connection utilization of a node                                             |
| Memory | Used memory   | mem_used         | MB    | Actually used memory capacity, including the capacity for data and cache                         |
| Memory | Memory utilization   | mem_util         | %     | The ratio of the actually used memory to the requested total memory                                 |
| Memory | Total keys    | keys             | -    | The total number of keys (level-1 keys) in instance storage                               |
| Memory | Expired keys    | expired        | -    | The number of keys expired in a time window, which is equal to the value of `expired_keys` outputted by the `info` command      |
| Memory | Evicted keys    | evicted        | -    | The number of keys evicted in a time window, which is equal to the value of `evicted_keys` outputted by the `info` command      |
| Memory | Replication delay     | repl_delay       | Byte  | The command delay between the replica node and the master node                             |
| Request | Total requests       | commands         | requests/second | QPS, that is, the number of command executions per second                                            |
| Request |Write requests       | cmd_read         | requests/second | The number of read command executions per second. For more information about read command types, please see [Command types](#mlfl).                |
| Request |Write requests       | cmd_write        | requests/second | The number of write command executions per second. For more information about write command types, please see [Command types](#mlfl).                |
| Request | Other requests     | cmd_other        | requests/second| The number of command (excluding write and read commands) executions per second |
| Response | Slow queries       | cmd_slow         | -    | The number of command executions with a latency greater than the `slowlog\-log\-slower\-than` configuration         |
| Response | Read request hits  | cmd_hits      | -    | The number of existing read request keys, which is equal to the value of the `keyspace_hits` metric outputted by the `info` command     |
| Response |  Read request misses  | cmd_miss  | -    | The number of nonexistent read request keys, which is equal to the value of the `keyspace_misses` metric outputted by the `info` command |
| Response | Read request hit rate | cmd_hits_ratio   | %     | Key hits/(Key hits + Key misses). This metric reflects the cache miss situation. |

### Redis instance monitoring
The instance monitoring includes all monitoring data of an instance, including the monitoring data of proxy nodes and Redis nodes, which is aggregated by the SUM, AVG, MAX, and LAST algorithms.

| Category     | Metric         | Associated Node View | Parameter        | Unit  | Description                                                     |
| -------- | ------------------ | -------- | ------------------ | ----- | ------------------------------------------------------------ |
| CPU  | CPU utilization          | Redis node     | cpu_util           | %     | Average CPU utilization                               |
| CPU  | Max CPU utilization of a node  | Redis node   | cpu_max_util   | %  | The maximum CPU utilization of a node (shard or replica) in an instance  |
| Memory | Used memory    | Redis node     | mem_used           | MB    | Actually used memory capacity, including the capacity for data and cache         |
| Memory | Memory utilization         | Redis node     | mem_util           | %     | The ratio of the actually used memory to the requested total memory                       |
| Memory | Max memory utilization of node  | Redis node    | mem_max_util    | %     | The maximum memory utilization of a node (shard or replica) in an instance   |
| Memory |  Total keys    | Redis node     | keys      | -    | The total number of keys (level-1 keys) in instance storage                      |
| Memory | Expired keys     | Redis node     | expired  | -    | The number of keys expired in a time window, which is equal to the value of `expired_keys` outputted by the `info` command  |
| Memory |  Evicted keys    | Redis node     | evicted  | -    | The number of keys evicted in a time window, which is equal to the value of `evicted_keys` outputted by the `info` command   |
| Network | Connections           | Proxy node    | connections        | -    | The number of TCP connections to an instance                |
| Network | Connection utilization         | Proxy node    | connections_util   | %     | The ratio of the number of TCP connections to the maximum number of connections    |
| Network | Inbound traffic             | Proxy node    | in_flow            | MB/s  | Private inbound traffic                                          |
| Network | Inbound traffic utilization       | Proxy node    | in_bandwidth_util  | %     | The ratio of the actually used private inbound traffic to the maximum traffic            |
| Network | Inbound traffic limit count     | Proxy node    | in_flow_limit      | -    | The number of times inbound traffic triggers a traffic limit                         |
| Network | Outbound traffic              | Proxy node    | out_flow           | MB/s  | Private outbound traffic                                        |
| Network | Outbound traffic utilization       | Proxy node    | out_bandwidth_util | %     | The ratio of the actually used private outbound traffic to the maximum traffic           |
| Network | Outbound traffic limit count     | Proxy node    | out_flow_limit     | -    | The number of times outbound traffic triggers a traffic limit                               |
| Latency | Average execution latency       | Proxy node    | latency_avg        | ms    | The average execution latency between the proxy and the Redis server        |
| Network | Max execution latency       | Proxy node    | latency_max        | ms   | The maximum execution latency between the proxy and the Redis server        |
| Network | Average read latency         | Proxy node    | latency_read       | ms    | The average execution latency of read commands between the proxy and the Redis server. For more information about read command types, please see [Command types](#mlfl).  |
| Network | Average write latency         | Proxy node    | latency_write      | ms    | The average execution latency of write commands between the proxy and the Redis server. For more information about write command types, please see [Command types](#mlfl).  |
| Network | Average latency of other commands   | Proxy node    | latency_other      | ms    | The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server  |
| Request | Total requests  | Redis node     | commands      | requests/second | QPS, that is, the number of command executions per second                              |
| Request | Write requests    | Redis node     | cmd_read      | requests/second | The number of read command executions per second. For more information about read command types, please see [Command types](#mlfl).          |
| Request | Write requests    | Redis node     | cmd_write    | requests/second | The number of write command executions per second. For more information about write command types, please see [Command types](#mlfl).           |
| Request |  Other requests           | Redis node     | cmd_other          | requests/second| The number of command (excluding write and read commands) executions per second |
| Request | Big value requests        | Proxy node    | cmd_big_value      | requests/second | The number of executions of commands larger than 32 KB per second        |
| Request |  Key requests          | Proxy node    | cmd_key_count      | keys/second | The number of keys accessed by a command per second                     |
| Request | Mget requests         | Proxy node    | cmd_mget           | requests/second | The number of Mget command executions per second                           |
| Response | Slow queries       | Redis node     | cmd_slow     | -    | The number of command executions with a latency greater than the `slowlog\-log\-slower\-than` configuration  |
| Request |  Read request hits         | Redis node     | cmd_hits           | -    | The number of existing read request keys, which is equal to the value of the `keyspace_hits` metric outputted by the `info` command     |
| Request | Read request misses         | Redis node     | cmd_miss           | -    | The number of nonexistent read request keys, which is equal to the value of the `keyspace_misses` metric outputted by the `info` command |
| Request | Execution errors           | Proxy node   | cmd_err            | -    | The number of command execution errors. For example, the command does not exist, parameters are incorrect, etc.           |
| Request | Read request hit rate       | Redis node     | cmd_hits_ratio     | %     | Key hits/(Key hits + Key misses). This metric reflects the cache miss situation. |


<span id = "mlfl"></span>
### Command types

| Type | Commands                                                         |
| -------- | ------------------------------------------------------------ |
| Read   | get,strlen,exists,getbit,getrange,substr,mget,llen,lindex,lrange,sismember,scard,srandmember,<br>sinter,sunion,sdiff,smembers,sscan,zrange,zrangebyscore,zrevrangebyscore,zrangebylex,<br>zrevrangebylex,zcount,zlexcount,zrevrange,zcard,zscore,zrank,zrevrank,zscan,hget,hmget,<br>hlen,hstrlen,hkeys,hvals,hgetall,hexists,hscan,randomkey,keys,scan,dbsize,type,ttl,touch,pttl,<br>dump,object,memory,bitcount,bitpos,georadius_ro,georadiusbymember_ro,geohash,geopos,geodist,pfcount |
| Write   | set,setnx,setex,psetex,append,del,unlink,setbit,bitfield,setrange,incr,decr,rpush,lpush,rpushx,<br>lpushx,linsert,rpop,lpop,brpop,brpoplpush,blpop,lset,ltrim,lrem,rpoplpush,sadd,srem,smove,spop,<br>sinterstore,sunionstore,sdiffstore,zadd,zincrby,zrem,zremrangebyscore,zremrangebyrank,<br>zremrangebylex,zunionstore,zinterstore,hset,hsetnx,hmset,hincrby,hincrbyfloat,hdel,incrby,decrby,<br>incrbyfloat,getset,mset,msetnx,swapdb,move,rename,renamenx,expire,expireat,pexpire,pexpireat,<br>flushdb,flushall,sort,persist,restore,restore-asking,migrate,bitop,geoadd,georadius,georadiusbymember,<br>pfadd,pfmerge,pfdebug |

## Querying Node Information
Use the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) API to get the IDs of proxy and Redis nodes.
>!The IDs of proxy and Redis nodes will change when node failover, instance capacity expansion/reduction, data migration, etc., occur. Therefore, we recommend that you get the latest node information from the API in a timely manner.

