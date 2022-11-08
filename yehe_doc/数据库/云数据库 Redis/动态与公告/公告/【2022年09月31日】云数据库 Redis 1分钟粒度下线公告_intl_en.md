Cloud Monitor will discontinue the 1-minute granuarity alarm policy for TencentDB for Redis and QCE/REDIS namespace, which will have the following impacts:

- You can’t receive the alarm notification of TencentDB for Redis Memory Edition (1-minute granularity).
- Data can’t be displayed on the dashboard of TencentDB for Redis Memory Edition (1-minute granularity).
- You can’t pull the monitoring data of TencentDB for Redis Memory Edition (1-minute granularity).

** Migration Solutions**

- Alarm policy: You need to migrate the alarm policy of the existing TencentDB for Redis instances with 1-minute monitoring granularity to those with 5-second monitoring granularity. [Click to view the mappings of metrics](#step1)
- Dashboard: You need to migrate the dashboard of the existing TencentDB for Redis instances with 1-minute monitoring granularity to 5-second monitoring granularity. [Click to view the mappings of metrics](#step1)
- Pulling monitoring metric data through APIs: You need to switch QCE/REDIS to QCE/REDIS_MEM, and modify the names of pulled metrics simultaneously.

Because 1-minute monitoring granularity of TencentDB for Redis is not completely the same as the metric names in [Mappings of Metrics](#step1). This document describes the mappings of monitoring metrics of TencentDB for Redis 1-minute monitoring granularity and 5-second monitoring granularity for you to compare and migrate.

<span id="step1"></span>


## Monitoring Metric Mappings Between 1-Minute and 5-Second Alarm Policy 

<table>
<thead>
<tr><th width="24%">1-minute granularity metric</th><th width="5%">Name of 1-minute granularity metric</th><th width="24%"> 5-second granularity metric</th><th width="5%">Name of 5-second metric</th><th width="2%">Unit</th><th width="40%">Description</th></tr>
</thead>
<tbody><tr>
<td>CPU load</td>
<td>cpu_us_min</td>    
<td>CPU utilization</td>
<td>cpu_util</td>
<td>%</td>
<td>Average CPU utilization</td></tr>
<tr>
<td>Maximum CPU load</td>
<td>CpuMaxUsMin</td>    
<td>Max CPU utilization of a node</td>
<td>cpu_max_util</td>
<td>%</td>
<td>The maximum CPU utilization of a node (shard or replica) in an instance</td></tr>    
<tr>
<td>Memory usage</td>
<td>storage_min</td>    
<td>Memory usage</td>
<td>mem_used</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td></tr>
<tr>  
<td>Capacity usage</td>
<td>storage_us_min</td>    
<td>Memory utilization</td>
<td>mem_util</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td></tr>
<tr>  
<td>Maximum capacity utilization</td>
<td>StorageMaxUsMin</td>    
<td>Maximum memory utilization of a node</td>
<td>mem_max_util</td>
<td>%</td>
<td>The maximum memory utilization of a node (shard or replica) in an instance</td></tr>    
<tr>
<td>Private network inbound traffic</td>
<td>in_flow_min</td>     
<td>Inbound traffic</td>
<td>in_flow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td> 
<td>in_flow_us_min</td>    
<td>Inbound traffic utilization</td>
<td>in_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Private network outbound traffic</td>
<td>out_flow_min</td>      
<td>Outbound traffic</td>
<td>out_flow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td>
<td>out_flow_us_min</td>     
<td>Outbound traffic utilization</td>
<td>out_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td>Connections</td>
<td>connections_min</td>     
<td>Connections</td>
<td>connections</td>
<td>-</td>
<td>The number of TCP connections to an instance</td></tr>
    <tr>
<td>Connection utilization</td> 
<td>connections_us_min</td>         
<td>Connection usage</td>
<td>connections_util</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
<tr>
<td>Number of slow queries</td>
<td>slow_query_min</td>    
<td>Slow queries</td>
<td>cmd_slow</td>
<td>Times</td>
<td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td></tr>
<tr>
<td>Keys</td>
<td>keys_min</td>    
<td>Keys</td>
<td>keys</td>
<td>-</td>
<td>Total number of keys stored in an instance (first-level keys)</td></tr>
<tr>
<td>Expired keys</td>
<td>expired_keys_min</td>   
<td>Expired keys</td>
<td>expired</td>
<td>-</td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command.</td></tr>
<tr>
<td>Evicted keys</td>
<td>evicted_keys_min</td>    
<td>Evicted keys</td>
<td>evicted</td>
<td>-</td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command.</td></tr>
<tr>
<td>Average execution latency</td>
<td>latency_min</td>    
<td>Average execution latency</td>
<td>latency_avg</td>
<td>ms</td>
<td>Average execution latency from proxy to Redis server</td></tr>
<tr>
<td>Average read latency</td>
<td>latency_get_min</td>    
<td>Average read latency</td>    
<td>latency_read</td>
<td>ms</td>
<td>Average execution latency of read commands from proxy to Redis server</td></tr>
<tr>
<td>Average write latency</td>
<td>latency_set_min</td>
<td>Average write latency</td>    
<td>latency_write</td>
<td>ms</td>
<td>Average execution latency of write command from proxy to Redis server</td></tr>
<tr>
<td>Average latency of other commands</td>
<td>latency_other_min</td>    
<td>Average latency of other commands</td>
<td>latency_other</td>
<td>ms</td>
<td>Average execution latency of commands other than read and write commands from proxy to Redis server</td></tr>
<tr>
<td>QPS</td>
<td>qps_min</td>    
<td>Total requests</td>
<td>commands</td>
<td>Executions/sec</td>
<td>QPS, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td>
<td>stat_get_min</td>    
<td>Read requests</td>    
<td>cmd_read</td>
<td>Executions/sec</td>
<td>The number of read command executions per second</td></tr>
<tr>
<td>Write requests</td>     
<td>stat_set_min</td>    
<td>Write requests</td>
<td>cmd_write</td>
<td>Executions/sec</td>
<td>The number of write command executions per second</td></tr>
<tr>
<td>Other requests</td>    
<td>stat_other_min</td>
<td>Other requests</td> 
<td>cmd_other</td>
<td>Executions/sec</td>
<td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td>Big value requests</td>
<td>big_value_min</td>    
<td>Big value requests</td>    
<td>cmd_big_value</td>
<td>Executions/sec</td>
<td>The number of executions of commands larger than 32 KB per second</td></tr>
<tr>
<td>Read request hits</td>
<td>stat_success_min</td>    
<td>Read request hits</td>    
<td>cmd_hits</td>
<td>Times</td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command.</td></tr>
<tr>
<td>Read request misses</td>
<td>stat_missed_min</td>    
<td>Read request misses</td>    
<td>cmd_miss</td>
<td>Times</td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command.</td></tr>
<tr>
<td>Execution errors</td>
<td>cmd_err_min</td>     
<td>Execution errors</td>   
<td>cmd_err</td>
<td>Times</td>
<td>Number of command execution errors, such as errors occurred when a command does not exist or a parameter is invalid.</td></tr>
<tr>
<td>Read request hit rate</td> 
<td>cache_hit_ratio_min</td>      
<td>Read request hit rate</td>
<td>cmd_hits_ratio</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null.</td></tr>
</tbody></table>


## Mappings of Monitoring Metrics Between 1-Minute and 5-Second Dashboard

<table>
<thead>
<tr><th width="24%">1-minute granularity metric</th><th width="5%">Name of 1-minute granularity metric</th><th width="24%">5-Second granularity metric</th><th width="5%">Name of 5five-second granularity metric</th><th width="2%">Unit</th><th width="40%">Description</th></tr>
</thead>
<tbody><tr>
<td>CPU utilization</td>
<td>cpu_us_min</td>    
<td>Average CPU utilization</td>
<td>cpu_util</td>
<td>%</td>
<td>Average CPU utilization</td></tr>
<tr>
<td>Maximum CPU utilization of a shard</td>
<td>cpu_max_us_min</td>    
<td>Maximum CPU utilization of a node</td>
<td>cpu_max_util</td>
<td>%</td>
<td>The maximum CPU utilization of a node (shard or replica) in an instance</td></tr>    
<tr>
<td>Memory usage</td>
<td>storage_min</td>    
<td>Memory usage</td>
<td>mem_used</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td></tr>
<tr>  
<td>Memory utilization</td>
<td>storage_us_min</td>    
<td>Memory utilization</td>
<td>mem_util</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td></tr>
<tr>  
<td>Maximum memory utilization of a shard</td>
<td>storage_max_us_min</td>    
<td>Maximum memory utilization of a node</td>
<td>mem_max_util</td>
<td>%</td>
<td>The maximum memory utilization of a node (shard or replica) in an instance</td></tr>    
<tr>
<td>Inbound traffic</td>
<td>in_flow_min</td>     
<td>Inbound traffic</td>
<td>in_flow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td> 
<td>in_flow_us_min</td>    
<td>Inbound traffic utilization</td>
<td>in_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Outbound traffic</td>
<td>out_flow_min</td>      
<td>Outbound traffic</td>
<td>out_flow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td>
<td>out_flow_us_min</td>     
<td>Outbound traffic utilization</td>
<td>out_bandwidth_util</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td>Connections</td>
<td>connections_min</td>     
<td>Connections</td>
<td>connections</td>
<td>-</td>
<td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connection usage</td> 
<td>connections_us_min</td>         
<td>Connection utilization</td>
<td>connections_util</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
<tr>
<td>Slow queries</td>
<td>slow_query_min</td>    
<td>Slow queries</td>
<td>cmd_slow</td>
<td>Times</td>
<td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td></tr>
<tr>
<td>Keys</td>
<td>keys_min</td>    
<td>Keys</td>
<td>keys</td>
<td>-</td>
<td>Total number of keys stored in an instance (first-level keys)</td></tr>
<tr>
<td>Expired keys</td>
<td>expired_keys_min</td>   
<td>Expired keys</td>
<td>expired</td>
<td>-</td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command.</td></tr>
<tr>
<td>Evicted keys</td>
<td>evicted_keys_min</td>    
<td>Evicted keys</td>
<td>evicted</td>
<td>-</td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command.</td></tr>
<tr>
<td>Average execution latency</td>
<td>latency_min</td>    
<td>Average execution latency</td>
<td>latency_avg</td>
<td>ms</td>
<td>Average execution latency from proxy to Redis server</td></tr>
<tr>
<td>Average read latency</td>
<td>latency_get_min</td>    
<td>Average read latency</td>    
<td>latency_read</td>
<td>ms</td>
<td>Average execution latency of read commands from proxy to Redis server</td></tr>
<tr>
<td>Average write latency</td>
<td>latency_set_min</td>
<td>Average write latency</td>    
<td>latency_write</td>
<td>ms</td>
<td>Average execution latency of write command from proxy to Redis server</td></tr>
<tr>
<td>Average latency of other commands</td>
<td>latency_other_min</td>    
<td>Average latency of other commands</td>
<td>latency_other</td>
<td>ms</td>
<td>Average execution latency of commands other than read and write commands from proxy to Redis server</td></tr>
<tr>
<td>QPS</td>
<td>qps_min</td>    
<td>Total requests</td>
<td>commands</td>
<td>Executions/sec</td>
<td>QPS, that is, the number of command executions per second</td></tr>
<tr>
<td>Number of read requests</td>
<td>stat_get_min</td>    
<td>Read requests</td>    
<td>cmd_read</td>
<td>Executions/sec</td>
<td>The number of read command executions per second</td></tr>
<tr>
<td>Number of write requests</td>     
<td>stat_set_min</td>    
<td>Write requests</td>
<td>cmd_write</td>
<td>Executions/sec</td>
<td>The number of write command executions per second</td></tr>
<tr>
<td >Number of Get requests</td>    
<td>cmdstat_get_min</td>
<td rowspan=18">Other requests</td> 
<td rowspan="18">cmd_other</td>
<td rowspan="18">Executions/sec</td>
<td rowspan="18">The number of command (excluding write and read commands) executions per second.</td>    
</tr>
<tr>    
<td>Number of Getbit requests</td>    
<td>cmdstat_getbit_min</td>
</tr>
<tr>       
<td>Number of Getrange requests</td>    
<td>cmdstat_getrange_min</td>
</tr>
<tr>    
<td>Number of Mget requests</td>    
<td>cmdstat_hget_min</td>
</tr>
<tr>    
<td>Number of Hgetall requests</td>    
<td>cmdstat_hmget_min</td>
</tr>
<tr>       
<td>Number of Hmget requests</td>    
<td>cmdstat_hmget_min</td>
 </tr>
<tr>     
<td>Number of Hmset requests</td>    
<td>cmdstat_hmset_min</td>
</tr>
<tr>      
<td>Number of Hset requests</td>    
<td>cmdstat_hset_min</td>
</tr>
<tr>      
<td>Number of Hsetnx requests</td>    
<td>cmdstat_hsetnx_min</td>
</tr>
<tr>      
<td>Number of lset requests</td>    
<td>cmdstat_lset_min</td>
</tr>
<tr>      
<td>Number of Mget requests</td>    
<td>cmdstat_mget_min</td>
</tr>
<tr>      
<td>Number of Mset requests</td>    
<td>cmdstat_mset_min</td>
</tr>
<tr>      
<td>Number of Msetnx requests</td>    
<td>cmdstat_msetnx_min</td>
</tr>
<tr>      
<td>Number of Set requests</td>    
<td>cmdstat_set_min</td>
</tr>
<tr>      
<td>Number of Setbit requests</td>    
<td>cmdstat_setbit_min</td>
</tr>
<tr>      
<td>Number of Setex requests</td>    
<td>cmdstat_setex_min</td>
</tr>
<tr>      
<td>Number of Setnx requests</td>    
<td>cmdstat_setnx_min</td>
</tr>
<tr>      
<td>Number of Setrange requests</td>    
<td>cmdstat_setnx_min</td>
</tr>
<tr>
<td>Big value requests</td>
<td>big_value_min</td>    
<td>Big value requests</td>    
<td>cmd_big_value</td>
<td>Executions/sec</td>
<td>The number of executions of commands larger than 32 KB per second</td></tr>
<tr>
<td>Read request hits</td>
<td>stat_success_min</td>    
<td>Read request hits</td>    
<td>cmd_hits</td>
<td>Times</td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command.</td></tr>
<tr>
<td>Read request misses</td>
<td>stat_missed_min</td>    
<td>Read request misses</td>    
<td>cmd_miss</td>
<td>Times</td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command.</td></tr>
<tr>
<td>Execution errors</td>
<td>cmd_err_min</td>     
<td>Execution errors</td>   
<td>cmd_err</td>
<td>-</td>
<td>Number of command execution errors, such as errors occurred when a command does not exist or a parameter is invalid.</td></tr>
<tr>
<td>Read request hit rate</td> 
<td>cache_hit_ratio_min</td>      
<td>Read request hit rate</td>
<td>cmd_hits_ratio</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null.</td></tr>
</tbody></table>




### Mappings between 1-minute and 5-second API monitoring metrics

### Namespace

- 1-minute: Namespace=QCE/REDIS 
-  5-second: Namespace=QCE/REDIS_MEM 

### Monitoring metrics

#### Instance dimension (standard architecture)

<table>
<thead>
<tr><th width="35%">1-minute granularity metric</th><th width="5%">Name of 1-minute granularity metric</th><th width="35%">5-Second granularity metric</th><th width="5%">Name of 5-second granularity metric</th><th width="2%">Unit</th><th width="18%">Description</th></tr>
</thead>
<tbody><tr>
<td>CPU utilization</td>
<td>CpuUsMin</td>    
<td>CPU utilization</td>
<td>CpuUtil</td>
<td>%</td>
<td>Average CPU utilization</td></tr>
<tr>
<td>Memory usage</td>
<td>StorageMin</td>    
<td>Memory usage</td>
<td>MemUsed</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td></tr>
<tr>  
<td>Memory utilization</td>
<td>StorageUsMin</td>    
<td>Memory utilization</td>
<td>MemUtil</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td></tr> 
<tr>
<td>Keys</td>
<td>keys_min</td>    
<td>Keys</td>
<td>Keys</td>
<td>-</td>
<td>Total number of keys stored in an instance (first-level keys)</td></tr>
<tr>
<td>Expired keys</td>
<td>ExpiredKeysMin</td>    
<td>Expired keys</td>
<td>Expired</td>
<td>-</td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command.</td></tr>
<tr>
<td>Evicted keys</td>
<td>EvictedKeysMin</td>    
<td>Evicted keys</td>
<td>Evicted</td>
<td>-</td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command.</td></tr>
<tr>
<td>Connections</td>
<td>ConnectionsMin</td>     
<td>Connections</td>
<td>Connections</td>
<td>-</td>
<td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connection utilization</td>
<td>ConnectionsUsMin</td>    
<td>Connection usage</td>
<td>ConnectionsUtil</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
    <tr>
<td>Inbound traffic</td>
<td>InFlowMin</td>     
<td>Inbound traffic</td>
<td>InFlow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td>
<td>InFlowUsMin</td>     
<td>Inbound traffic utilization</td>
<td>InBandwidthUtil</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Outbound traffic</td>
<td>OutFlowMin</td>      
<td>Outbound traffic</td>
<td>OutFlow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td>
<td>OutFlowUsMin</td>      
<td>Outbound traffic utilization</td>
<td>OutBandwidthUtil</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Average execution latency</td>
<td>LatencyMin</td>    
<td>Average execution latency</td>
<td>LatencyAvg</td>
<td>ms</td>
<td>Average execution latency from proxy to Redis server</td></tr>
<tr>
<td>Average read latency</td>
<td>LatencyGetMin</td>    
<td>Average read latency</td>    
<td>LatencyRead</td>
<td>ms</td>
<td>Average execution latency of read commands from proxy to Redis server</td></tr>
<tr>
<td>Average write latency</td>
<td>LatencySetMin</td>
<td>Average write latency</td>    
<td>LatencyWrite</td>
<td>ms</td>
<td>Average execution latency of write command from proxy to Redis server</td></tr>
<tr>
<td>Average latency of other commands</td>
<td>LatencyOtherMin</td>    
<td>Average latency of other commands</td>
<td>LatencyOther</td>
<td>ms</td>
<td>Average execution latency of commands other than read and write commands from proxy to Redis server</td></tr>
<tr>
<td>Total requests</td>
<td>QpsMin</td>    
<td>Total requests</td>
<td>Commands</td>
<td>Executions/sec</td>
<td>QPS, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td>
<td>StatGetMin</td>    
<td>Read requests</td>    
<td>CmdRead</td>
<td>Executions/sec</td>
<td>The number of read command executions per second</td></tr>
<tr>
<td>Write requests</td>     
<td>StatSetMin</td>    
<td>Write requests</td>
<td>CmdWrite</td>
<td>Executions/sec</td>
<td>The number of write command executions per second</td></tr>
<tr>
<td>Other requests</td>     
<td>StatOtherMin</td>    
<td>Other requests</td>
<td>CmdOther</td>
<td>Executions/sec</td>
<td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td>Big value requests</td>
<td>BigValueMin</td>    
<td>Big value requests</td>    
<td>CmdBigValue</td>
<td>Executions/sec</td>
<td>The number of executions of commands larger than 32 KB per second</td></tr>
<tr>
    <td>Slow queries</td>
    <td>SlowQueryMin</td>
    <td>Slow queries</td>
    <td>CmdSlow</td>
    <td>Times</td>
    <td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td></tr>    
<tr>
<td>Read request hits</td>
<td>StatSuccessMin</td>    
<td>Read request hits</td>    
<td>CmdHits</td>
<td>Times</td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command.</td></tr>
<tr>
<td>Read request misses</td>
<td>StatMissedMin</td>    
<td>Read request misses</td>    
<td>CmdMiss</td>
<td>Times</td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command.</td></tr>
<tr>
<td>Execution errors</td>
<td>CmdErrMin</td>     
<td>Execution errors</td>   
<td>CmdErr</td>
<td>Times</td>
<td>Number of command execution errors, such as errors occurred when a command does not exist or a parameter is invalid.</td></tr>
<tr>
<td>Read request hit rate</td> 
<td>CacheHitRatioMin</td>      
<td>Read request hit rate</td>
<td>CmdHitsRatio</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null.</td></tr>    
</tbody></table>


#### Instance dimension (cluster architecture)

<table>
<thead>
<tr><th width="35%">1-minute granularity metric</th><th width="5%">Name of 1-minute granularity metric</th><th width="35%">5-second granularity metric</th><th width="5%">Name of 5-second granularity metric</th><th width="2%">Unit</th><th width="18%">Description</th></tr>
</thead>
<tbody><tr>
<td>Average CPU utilization</td>
<td>CpuUsMin</td>    
<td>CPU utilization</td>
<td>CpuUtil</td>
<td>%</td>
<td>Average CPU utilization</td></tr>
<tr>
<td>Max CPU utilization of a shard</td>
<td>CpuMaxUsMin</td>    
<td>Max CPU utilization of a node</td>
<td>CpuMaxUtil</td>
<td>%</td>
<td>Highest CPU utilization value of all shards in a cluster</td></tr>   
<tr>
<td>Memory usage</td>
<td>StorageMin</td>    
<td>Memory usage</td>
<td>MemUsed</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td></tr>
<tr>  
<td>Memory utilization</td>
<td>StorageUsMin</td>    
<td>Memory utilization</td>
<td>MemUtil</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td></tr> 
<tr>
<td>Max Memory Utilization of Shard</td>
<td>StorageMaxUsMin</td>    
<td>Max memory utilization of a node</td>
<td>MemMaxUtil</td>
<td>%</td>
<td>The highest memory utilization value of all shards in a cluster</td></tr>  
<tr>
<td>Keys</td>
<td>KeysMin</td>    
<td>Keys</td>
<td>Keys</td>
<td>-</td>
<td>Total number of keys stored in an instance (first-level keys)</td></tr>
<tr>
<td>Expired keys</td>
<td>ExpiredKeysMin</td>    
<td>Expired keys</td>
<td>Expired</td>
<td>-</td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command.</td></tr>
<tr>
<td>Evicted keys</td>
<td>EvictedKeysMin</td>    
<td>Evicted keys</td>
<td>Evicted</td>
<td>-</td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command.</td></tr>
<tr>
<td>Connections</td>
<td>ConnectionsMin</td>     
<td>Connections</td>
<td>Connections</td>
<td>-</td>
<td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connection utilization</td>
<td>ConnectionsUsMin</td>    
<td>Connection usage</td>
<td>ConnectionsUtil</td>
<td>%</td>
<td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
    <tr>
<td>Inbound traffic</td>
<td>InFlowMin</td>     
<td>Inbound traffic</td>
<td>InFlow</td>
<td>MB/s</td>
<td>Private network inbound traffic</td></tr>
<tr>
<td>Inbound traffic utilization</td>
<td>InFlowUsMin</td>     
<td>Inbound traffic utilization</td>
<td>InBandwidthUtil</td>
<td>%</td>
<td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Outbound traffic</td>
<td>OutFlowMin</td>      
<td>Outbound traffic</td>
<td>OutFlow</td>
<td>MB/s</td>
<td>Private network outbound traffic</td></tr>
<tr>
<td>Outbound traffic utilization</td>
<td>OutFlowUsMin</td>      
<td>Outbound traffic utilization</td>
<td>OutBandwidthUtil</td>
<td>%</td>
<td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>    
<tr>
<td>Average execution latency</td>
<td>LatencyMin</td>    
<td>Average execution latency</td>
<td>LatencyAvg</td>
<td>ms</td>
<td>Average execution latency from proxy to Redis server</td></tr>
<tr>
<td>Average read latency</td>
<td>LatencyGetMin</td>    
<td>Average read latency</td>    
<td>LatencyRead</td>
<td>ms</td>
<td>Average execution latency of read commands from proxy to Redis server</td></tr>
<tr>
<td>Average write latency</td>
<td>LatencySetMin</td>
<td>Average write latency</td>    
<td>LatencyWrite</td>
<td>ms</td>
<td>Average execution latency of write command from proxy to Redis server</td></tr>
<tr>
<td>Average latency of other commands</td>
<td>LatencyOtherMin</td>    
<td>Average latency of other commands</td>
<td>LatencyOther</td>
<td>ms</td>
<td>Average execution latency of commands other than read and write commands from proxy to Redis server</td></tr>
<tr>
<td>Total requests</td>
<td>QpsMin</td>    
<td>Total requests</td>
<td>Commands</td>
<td>Executions/sec</td>
<td>QPS, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td>
<td>StatGetMin</td>    
<td>Read requests</td>    
<td>CmdRead</td>
<td>Executions/sec</td>
<td>The number of read command executions per second</td></tr>
<tr>
<td>Write requests</td>     
<td>StatSetMin</td>    
<td>Write requests</td>
<td>CmdWrite</td>
<td>Executions/sec</td>
<td> The number of write command executions per second</td></tr>
<tr>
<td>Other requests</td>     
<td>StatOtherMin</td>    
<td>Other requests</td>
<td>CmdOther</td>
<td>Executions/sec</td>
<td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td>Big value requests</td>
<td>BigValueMin</td>    
<td>Big value requests</td>    
<td>CmdBigValue</td>
<td>Executions/sec</td>
<td>The number of executions of commands larger than 32 KB per second</td></tr>
<tr>
    <td>Slow queries</td>
    <td>SlowQueryMin</td>
    <td>Slow queries</td>
    <td>CmdSlow</td>
    <td>Times</td>
    <td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td></tr>    
<tr>
<td>Read request hits</td>
<td>StatSuccessMin</td>    
<td>Read request hits</td>    
<td>CmdHits</td>
<td>Times</td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command.</td></tr>
<tr>
<td>Read request misses</td>
<td>StatMissedMin</td>    
<td>Read request misses</td>    
<td>CmdMiss</td>
<td>Times</td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command.</td></tr>
<tr>
<td>Execution errors</td>
<td>CmdErrMin</td>     
<td>Execution errors</td>   
<td>CmdErr</td>
<td>Times</td>
<td>Number of command execution errors, such as errors occurred when a command does not exist or a parameter is invalid.</td></tr>
<tr>
<td>Read request hit rate</td> 
<td>CacheHitRatioMin</td>      
<td>Read request hit rate</td>
<td>CmdHitsRatio</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null.</td></tr>    
</tbody></table>


#### Cluster sharding

<table>
<thead>
<tr><th width="35%">1-minute granularity metric</th><th width="5%">Name of 1-minute granularity metric</th><th width="35%">5-second granularity metric</th><th width="5%">Name of 5-second granularity metric</th><th width="2%">Unit</th><th width="18%">Description</th></tr>
</thead>
<tbody><tr>
<td>CPU utilization</td>
<td>CpuUsNodeMin</td>    
<td>CPU utilization</td>
<td>CpuUtilNode</td>
<td>%</td>
<td>Average CPU utilization</td></tr>
<tr>
<td>Memory usage</td>
<td>StorageNodeMin</td>    
<td>Memory usage</td>
<td>MemUsedNode</td>
<td>MB</td>
<td>Memory capacity actually used, including data and cache</td></tr>
<tr>  
<td>Memory utilization</td>
<td>StorageUsNodeMin</td>    
<td>Memory utilization</td>
<td>MemUtilNode</td>
<td>%</td>
<td>The ratio of the memory actually used to the total memory requested</td></tr> 
<tr>
<td>Keys</td>
<td>KeysNodeMin</td>    
<td>Keys</td>
<td>KeysNode</td>
<td>-</td>
<td>Total number of keys stored in an instance (first-level keys)</td></tr>
<tr>
<td>Expired keys</td>
<td>ExpiredKeysNodeMin</td>    
<td>Expired keys</td>
<td>ExpiredNode</td>
<td>-</td>
<td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command.</td></tr>
<tr>
<td>Evicted keys</td>
<td>EvictedKeysNodeMin</td>    
<td>Evicted keys</td>
<td>EvictedNode</td>
<td>-</td>
<td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command.</td></tr>    
<tr>
<td>Total requests</td>
<td>QpsNodeMin</td>    
<td>Total requests</td>
<td>CommandsNode</td>
<td>Executions/sec</td>
<td>QPS, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td>
<td>StatGetNodeMin</td>    
<td>Read requests</td>    
<td>CmdReadNode</td>
<td>Executions/sec/td>
<td>The number of read command executions per second</td></tr>
<tr>
<td>Write requests</td>     
<td>StatSetNodeMin</td>    
<td>Write requests</td>
<td>CmdWriteNode</td>
<td>Executions/sec</td>
<td>The number of write command executions per second</td></tr>
<tr>
<td>Other requests</td>     
<td>StatOtherNodeMin</td>    
<td>Other requests</td>
<td>CmdOtherNode</td>
<td>Executions/sec</td>
<td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
    <td>Slow queries</td>
    <td>SlowQueryNodeMin</td>
    <td>Slow queries</td>
    <td>CmdSlowNode</td>
    <td>Times</td>
    <td>The number of command executions with a latency greater than the `slowlog-log-slower-than` configuration</td></tr>    
<tr>
<td>Read request hits</td>
<td>StatSuccessNodeMin</td>    
<td>Read request hits</td>    
<td>CmdHitsNode</td>
<td>Times</td>
<td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command.</td></tr>
<tr>
<td>Read request misses</td>
<td>StatMissedNodeMin</td>    
<td>Read request misses</td>    
<td>CmdMissNode</td>
<td>Times</td>
<td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command.</td></tr>
<tr>
<td>Execution errors</td>
<td>CmdErrNodeMin</td>     
<td>Execution errors</td>   
<td>CmdErr</td>
<td>Times</td>
<td>Number of command execution errors, such as errors occurred when a command does not exist or a parameter is invalid.</td></tr>
<tr>
<td>Read request hit rate</td> 
<td>CacheHitRatioNodeMin</td>      
<td>Read request hit rate</td>
<td>CmdHitsRatioNode</td>
<td>%</td>
<td>Key hits/(key hits + key misses). This metric can reflect the situation of cache miss. When the access request quantity is 0, the value of this metric will be null.</td></tr>    
</tbody></table>


#### Description of parameters in each dimension

| Parameter (5-Second) | Dimension Name | Dimension Description | Format | 1-Minute Granularity Description |
| ------------------------------ | ---------- | ---------------------- | ------------------------------------------------------------ | --------------------------- |
| Instances.N.Dimensions.0.Name | instanceid | Dimension name of the instance ID | Enter a string-type dimension name, such as instanceid | Consistent with the 5-second granularity |
| Instances.N.Dimensions.0.Value | instanceid | Specific instance ID | Enter a specific Redis instance ID such as `tdsql-123456` or instance SN such as `crs-ifmymj41`, which can be queried by calling the [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065) API | Consistent with the 5-second granularity |
| Instances.N.Dimensions.1.Name | rnodeid | Dimension name of the Redis node ID | Enter a string-type dimension name, such as rnodeid | Corresponding dimension name at the minute level: clusterid |
| Instances.N.Dimensions.1.Value | rnodeid | Specific Redis node ID | Enter a specific Redis node ID, which can be obtained by calling the [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/api/product/239/38627) API | Corresponding dimension name at minute level: clusterid |

