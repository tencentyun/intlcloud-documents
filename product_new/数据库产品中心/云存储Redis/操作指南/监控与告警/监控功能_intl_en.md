TencentDB for Redis provides a full range of monitoring and custom alarming capabilities, including metrics such as load monitoring, access statistics, and network traffic.
The monitoring data is collected by the agents deployed on each host and then reported to the data relay node where it is checked, summarized, and reported to the Cloud Monitor system in batches. Cloud Monitor provides data views, data query APIs, and custom alarms.

You can log in to the [Redis Console](https://console.cloud.tencent.com/redis) or [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) to view monitoring data.

## Monitoring Data Retention Period
Redis currently supports monitoring metrics at the 1-minute, 5-minutes, 1-hour, or 1-day granularity. For the retention period of monitoring data at each granularity, please see [Use Limits](https://intl.cloud.tencent.com/document/product/248/32803).

## Descriptions of Monitoring Metrics
Cloud Monitor provides the following monitoring metrics for TencentDB for Redis instances:

<table>
<thead>
<tr>
<th>Category</th>
<th>Name</th>
<th>Parameter</th>
<th>Unit</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>CPU</td>
<td>CPU utilization</td>
<td>cpu_us_min</td>
<td>%</td>
<td>Average CPU utilization</td>
</tr>
<tr>
<td  rowspan=5>Memory</td>
<td>Memory usage</td>
<td>storage_min</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td>
</tr>
<tr>
<td>Content utilization</td>
<td>storage_us_min</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td>
</tr>
<tr>
<td>Keys</td>
<td>keys_min</td>
<td> - </td>
<td>Total number of keys stored in an instance (first-level keys)</td>
</tr>
<tr>
<td>Expired keys</td>
<td>expired_keys_min</td>
<td> - </td>
<td>Number of keys eliminated in a time window, which corresponds to the `expired_keys` output by the `info` command</td>
</tr>
<tr>
<td>Evicted keys</td>
<td>evicted_keys_min</td>
<td> - </td>
<td>Number of keys evicted in a time window, which corresponds to the `evicted_keys` output by the `info` command</td>
</tr>
<tr>
<td  rowspan=6>Network</td>
<td>Connections</td>
<td>connections_min</td>
<td> - </td>
<td>Number of TCP connections to an instance</td>
</tr>
<tr>
<td>Connection utilization</td>
<td>connections_us_min</td>
<td>%</td>
<td>Proportion of used connections</td>
</tr>
<tr>
<td>Inbound traffic</td>
<td>in_flow_min</td>
<td>Mb/s</td>
<td>Private network inbound traffic</td>
</tr>
<tr>
<td>Inbound traffic utilization</td>
<td>in_flow_us_min</td>
<td>%</td>
<td>Proportion of used private network inbound traffic</td>
</tr>
<tr>
<td>Outbound traffic</td>
<td>out_flow_min</td>
<td>Mb/s</td>
<td>Private network outbound traffic</td>
</tr>
<tr>
<td>Outbound traffic utilization</td>
<td>out_flow_us_min</td>
<td>%</td>
<td>Proportion of used private network outbound traffic</td>
</tr>
<tr>
<td  rowspan=4>Latency</td>
<td>Average execution latency</td>
<td>latency_min</td>
<td>ms</td>
<td>Average execution latency from proxy to Redis server</td>
</tr>
<tr>
<td>Average read latency</td>
<td>latency_get_min</td>
<td>ms</td>
<td>Average execution latency of read commands from proxy to Redis server</td>
</tr>
<tr>
<td>Average write latency</td>
<td>latency_set_min</td>
<td>ms</td>
<td>Average execution latency of write command from proxy to Redis server</td>
</tr>
<tr>
<td>Average latency of other commands</td>
<td>latency_other_min</td>
<td>ms</td>
<td>Average execution latency of commands other than read and write commands from proxy to Redis server</td>
</tr>
<tr>
<td  rowspan=5>Request</td>
<td>Requests</td>
<td>qps_min</td>
<td>requests/second</td>
<td>QPS, i.e., command executions</td>
</tr>
<tr>
<td>Read requests</td>
<td>stat_get_min</td>
<td>requests/second</td>
<td>Read command executions</td>
</tr>
<tr>
<td>Write requests</td>
<td>stat_set_min</td>
<td>requests/second</td>
<td>Write command executions</td>
</tr>
<tr>
<td>Other requests</td>
<td>stat_other_min</td>
<td>requests/second</td>
<td>Executions of commands other than read and write commands</td>
</tr>
<tr>
<td>Big value requests</td>
<td>big_value_min</td>
<td>requests/second</td>
<td>Number of executions for which the request size exceeds 32 KB</td>
</tr>
<tr>
<td  rowspan=5>Response</td>
<td>Slow queries</td>
<td>slow_query_min</td>
<td> - </td>
<td>Number of slow query commands</td>
</tr>
<tr>
<td>Read request hits</td>
<td>stat_success_min</td>
<td> - </td>
<td>Number of existing read request keys, which corresponds to the `keyspace_hits` metric output by the `info` command</td>
</tr>
<tr>
<td>Read request misses</td>
<td>stat_missed_min</td>
<td> - </td>
<td>Number of non-existing read request keys, which corresponds to the `keyspace_misses` metric output by the `info` command</td>
</tr>
<tr>
<td>Execution errors</td>
<td>cmd_err_min</td>
<td> - </td>
<td>Number of command execution errors, such as when a command does not exist or a parameter is incorrect</td>
</tr>
<tr>
<td>Read request hit rate</td>
<td>cache_hit_ratio_min</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null</td>
</tr>
</tbody></table>


The monitoring information of the Redis Cluster Edition can be divided into summary and shard information. The shard information does not include the network and latency metrics, while the summary information includes two additional metrics:

| Category | Name | Parameter | Unit | Description |
|---------|---------|---------|---------|---------|
| CPU | Maximum shard CPU utilization |cpu_max_us_min|%| The highest CPU utilization value of all shards in a cluster |
| Memory | Maximum shard memory utilization  |storage_max_us_min|%| The highest memory utilization value of all shards in a cluster |


### Command category

| Command Category | List |
|---------|---------|
| Read command | get,strlen,exists,getbit,getrange,substr,mget,llen,lindex,lrange,sismember,scard,srandmember,<br>sinter,sunion,sdiff,smembers,sscan,zrange,zrangebyscore,zrevrangebyscore,zrangebylex,<br>zrevrangebylex,zcount,zlexcount,zrevrange,zcard,zscore,zrank,zrevrank,zscan,hget,hmget,<br>hlen,hstrlen,hkeys,hvals,hgetall,hexists,hscan,randomkey,keys,scan,dbsize,type,ttl,touch,pttl,<br>dump,object,memory,bitcount,bitpos,georadius_ro,georadiusbymember_ro,geohash,geopos,geodist,pfcount |
| Write command | set,setnx,setex,psetex,append,del,unlink,setbit,bitfield,setrange,incr,decr,rpush,lpush,rpushx,<br>lpushx,linsert,rpop,lpop,brpop,brpoplpush,blpop,lset,ltrim,lrem,rpoplpush,sadd,srem,smove,spop,<br>sinterstore,sunionstore,sdiffstore,zadd,zincrby,zrem,zremrangebyscore,zremrangebyrank,<br>zremrangebylex,zunionstore,zinterstore,hset,hsetnx,hmset,hincrby,hincrbyfloat,hdel,incrby,decrby,<br>incrbyfloat,getset,mset,msetnx,swapdb,move,rename,renamenx,expire,expireat,pexpire,pexpireat,<br>flushdb,flushall,sort,persist,restore,restore-asking,migrate,bitop,geoadd,georadius,georadiusbymember,<br>pfadd,pfmerge,pfdebug |

