## Feature Description

The performance trends feature monitors the key performance metrics of database instances, Redis nodes, and proxy nodes in real time, including CPU, memory, key information, network usage, network utilization, requests, and responses. It collects monitoring data at the second granularity, dynamically displays the change trends of metrics as well as their maximum, minimum, and average values in tables graphically. You can compare the metrics of multiple nodes and different time periods and zoom in on and drag the monitoring view as needed.
The powerful statistical analysis capabilities, diversified display methods, and extremely high real-timeness of the performance trends feature can meet your needs in various routine Ops and troubleshooting scenarios of database instances. They help you quickly get a holistic picture of the database performance and prevent risks.

## Monitoring Metrics

Supported monitoring metrics are displayed in three dimensions: instance, Redis node, and proxy node.

### Instance

<table>
<thead>
<tr><th width="15%">Metric Category</th><th width="25%">Metric</th><th width="10%">Parameter</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody><tr>
<td rowspan="2">CPU</td>
<td>CPU utilization</td>    <td>cpu_util</td><td>%</td><td>Average CPU utilization</td></tr>
<tr>
<td>Max CPU utilization of node</td><td>cpu_max_util</td><td>%</td><td>The maximum among all node (shard or replica) CPU utilizations in an instance</td></tr>    
<tr>
<td rowspan="3">Memory information</td> 
<td>Used memory</td><td>mem_used</td><td>MB</td><td>Actually used memory capacity, including the capacity for data and cache</td></tr>
<tr>   
<td>Memory utilization</td><td>mem_util</td><td>%</td><td>The ratio of the actually used memory to the requested total memory</td></tr>
<tr>    
<td>Max memory utilization of node</td><td>mem_max_util</td><td>%</td><td>The maximum among all node (shard or replica) memory utilizations in an instance</td></tr>
<tr>
<td rowspan="3">Key information</td>  
<td>Total keys</td><td>keys</td><td>-</td><td>The total number of keys (level-1 keys) stored in the instance</td></tr>
<tr>
<td>Expired keys</td><td>expired</td><td>-</td><td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command</td></tr>
<tr> 
<td>Evicted keys</td><td>evicted</td><td>-</td><td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command</td></tr>
<tr>
<td rowspan="3">Network usage</td> 
<td>Connections</td><td>connections</td><td>-</td><td>The number of TCP connections to an instance</td></tr>    
<tr>   
<td>Inbound traffic</td><td>in_flow</td><td>MB/s</td><td>Private inbound traffic</td></tr>
<tr>    
<td>Outbound traffic</td><td>out_flow</td><td>MB/s</td><td>Private outbound traffic</td></tr>
<tr>
<td rowspan="3">Network utilization</td>     
<td>Connection utilization</td><td>connections_util</td><td>%</td><td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>    
<tr> 
<td>Inbound traffic utilization</td><td>in_bandwidth_util</td><td>%</td><td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>    
<tr>  
<td>Outbound traffic utilization</td><td>out_bandwidth_util</td><td>%</td><td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td rowspan="7">Request</td>    
<td>Total requests</td><td>commands</td><td>counts/sec</td><td>QPS, that is, the number of command executions per second</td></tr>
<tr> 
<td>Read requests</td>    <td>cmd_read</td><td>counts/sec</td><td>The number of read command executions per second</td></tr>
<tr>
<td>Write requests</td><td>cmd_write</td><td>counts/sec</td><td>The number of write command executions per second</td></tr>
<tr>
<td>Other requests</td> <td>cmd_other</td><td>counts/sec</td><td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr> 
<td>Big value requests</td>    <td>cmd_big_value</td><td>counts/sec</td><td>The number of executions of requests larger than 32 KB per second</td></tr>
<tr> 
<td>Key requests</td>    <td>cmd_key_count</td><td>counts/sec</td><td>The number of keys requested per second</td></tr>
<tr> 
<td>MGET executions</td>    <td>cmd_cmget</td><td>counts/sec</td><td>The number of requests made through MGET per second</td></tr>    
<tr>
<td rowspan="4">Response</td>
<td>Slow queries</td><td>cmd_slow</td><td>-</td><td>The number of command executions with a latency greater than the configured `slowlog-log-slower-than` value</td></tr>
<tr>
<td>Read request hits</td>    <td>cmd_hits</td><td>-</td><td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td></tr>
<tr>
<td>Read request misses</td>    <td>cmd_miss</td><td>-</td><td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td></tr>
<tr>   
<td>Read request hit rate</td><td>cmd_hits_ratio</td><td>%</td><td>Key hits/(key hits + key misses). This metric reflects cache misses. When the access request quantity is 0, the value of this metric will be null</td></tr>
<tr>
<td>Execution error</td>
<td>Execution errors</td>   <td>cmd_err</td><td>-</td><td>The number of command execution errors. For example, the command does not exist, or parameters are incorrect.</td></tr>
<tr>
<td rowspan=6>Latency</td>
<td>Average execution latency</td><td>latency_avg</td><td>ms</td><td>The average execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Max execution latency</td><td>latency_max</td><td>ms</td><td>The maximum execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>P99 execution latency</td><td>latency_p99</td><td>ms</td><td>The 99th percentile execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Average read latency</td><td>latency_read</td><td>ms</td><td>The average execution latency of read commands between the proxy and the Redis server. For more information on read command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Average write latency</td><td>latency_write</td><td>ms</td><td>The average execution latency of write commands between the proxy and the Redis server. For more information on write command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Average latency of other commands</td><td>latency_other</td><td>ms</td><td>The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server</td></tr>
</tbody></table>

### Redis node

<table>
<thead>
<tr><th width="15%">Metric Category</th><th width="25%">Metric</th><th width="10%">Parameter</th><th width="5%">Unit</th><th width="45%">Description</th></tr>
</thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU utilization</td><td>cpu_util</td><td>%</td><td>Average CPU utilization</td></tr>
<tr>
<td  rowspan=2>Network usage</td>
<td>Connections</td><td>connections</td><td>-</td><td>The number of connections between the proxy and a node</td></tr>
<tr>
<td>Connection utilization</td><td>connections_util</td><td>%</td><td>The connection utilization of a node</td></tr>
<tr>
<td  rowspan=2>Memory information</td>
<td>Used memory</td><td>mem_used</td><td>MB</td><td>Actually used memory capacity, including the capacity for data and cache</td></tr>
<tr>
<td>Memory utilization</td><td>mem_util</td><td>%</td><td>The ratio of the actually used memory to the requested total memory</td></tr>
<tr>
<td rowspan=3>Key information</td>
<td>Total keys</td><td>keys</td><td>-</td><td>The total number of keys (level-1 keys) stored in the instance</td></tr>
<tr>
<td>Expired keys</td><td>expired</td><td>-</td><td>The number of keys expired in a time window, which is equal to the value of `expired_keys` output by the `info` command</td></tr>
<tr>
<td>Evicted keys</td><td>evicted</td><td>-</td><td>The number of keys evicted in a time window, which is equal to the value of `evicted_keys` output by the `info` command</td></tr>
<tr>
<td>Replication delay</td><td>Replication delay</td><td>repl_delay</td><td>Byte</td><td>The command delay between the replica node and the master node</td></tr>
<tr>
<td  rowspan=4>Request</td>
<td>Total requests</td><td>commands</td><td>counts/sec</td><td>QPS, that is, the number of command executions per second</td></tr>
<tr>
<td>Read requests</td><td>cmd_read</td><td>counts/sec</td><td>The number of read command executions per second. For more information on read command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Write requests</td><td>cmd_write</td><td>counts/sec</td><td>The number of write command executions per second. For more information on write command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Other requests</td><td>cmd_other</td><td>counts/sec</td><td>The number of command (excluding write and read commands) executions per second</td></tr>
<tr>
<td  rowspan=4>Response</td>
<td>Slow queries</td><td>cmd_slow</td><td>-</td><td>The number of command executions with a latency greater than the configured `slowlog-log-slower-than` value</td></tr>
<tr>
<td>Read request hits</td><td>cmd_hits</td><td>-</td><td>The number of keys successfully requested by read commands, which is equal to the value of the `keyspace_hits` metric output by the `info` command</td></tr>
<tr>
<td>Read request misses</td><td>cmd_miss</td><td>-</td><td>The number of keys unsuccessfully requested by read commands, which is equal to the value of the `keyspace_misses` metric output by the `info` command</td></tr>
<tr>
<td>Read request hit rate</td><td>cmd_hits_ratio</td><td>%</td><td>Key hits/(key hits + key misses). This metric reflects cache misses.</td></tr>
</tbody></table>

### Proxy node

<table>
<thead><tr><th width="20%">Metric Category</th><th width="30%">Metric</th><th width="20%">Parameter</th><th width="5%">Unit</th><th width="25%">Description</th></tr></thead>
<tbody>
<tr>
<td>CPU</td>
<td>CPU utilization</td><td>cpu_util</td><td>%</td><td>Proxy CPU utilization</td></tr>
<tr>
<td rowspan=5>Request</td>
<td>Total requests</td><td>proxy_commands</td><td>counts/sec</td><td>The number of proxy command executions per second</td></tr>
<tr>
<td>Key requests</td><td>cmd_key_count</td><td>keys/second</td><td>The number of keys accessed by a command per second</td></tr>
<tr>
<td>MGET requests</td><td>cmd_mget</td><td>counts/sec</td><td>The number of MGET command executions per second</td></tr>
<tr>
<td>Execution errors</td><td>cmd_err</td><td>counts/sec</td><td>The number of proxy command execution errors per second. For example, the command does not exist, or parameters are incorrect.</td></tr>
<tr>
<td>Big value requests</td><td>cmd_big_value</td><td>counts/sec</td><td>The number of executions of requests larger than 32 KB per second</td></tr>
<tr>
<td rowspan=2>Traffic</td>
<td>Inbound traffic</td><td>in_flow</td><td>MB/s</td><td>Private inbound traffic</td></tr>
<tr>
<td>Outbound traffic</td><td>out_flow</td><td>MB/s</td><td>Private outbound traffic</td></tr>
<tr>   
<td rowspan=4>Network usage</td>
<td>Connections</td><td>connections</td><td>-</td><td>The number of TCP connections to an instance</td></tr>
<tr>
<td>Connections per sec</td><td>client_connections_received_per_second</td><td>-</td><td>The number of TCP connections established per second</td></tr>
<tr>
<td>Disconnections per second</td><td>client_connections_closed_per_second</td><td>-</td><td>The number of TCP connections closed per second</td></tr>
<tr>
<td>Abnormal disconnections per sec</td><td>client_connections_aborted_per_second</td><td>-</td><td>The number of TCP connections aborted per second</td></tr> 
<tr>
<td rowspan=5>Network utilization</td>
<td>Connection utilization</td><td>connections_util</td><td>%</td><td>The ratio of the number of TCP connections to the maximum number of connections</td></tr>
<tr>
<td>Inbound traffic utilization</td><td>in_bandwidth_util</td><td>%</td><td>The ratio of the actually used private inbound traffic to the maximum traffic</td></tr>
<tr>
<td>Inbound traffic limit count</td><td>in_flow_limit</td><td>-</td><td>The number of times inbound traffic triggers a traffic limit</td></tr>
<tr>
<td>Outbound traffic utilization</td><td>out_bandwidth_util</td><td>%</td><td>The ratio of the actually used private outbound traffic to the maximum traffic</td></tr>
<tr>
<td>Outbound traffic limit count</td><td>out_flow_limit</td><td>-</td><td>The number of times outbound traffic triggers a traffic limit</td></tr>
<tr>
<td rowspan=6>Latency</td>
<td>Average execution latency</td><td>latency_avg</td><td>ms</td><td>The average execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Max execution latency</td><td>latency_max</td><td>ms</td><td>The maximum execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>P99 execution latency</td><td>latency_p99</td><td>ms</td><td>The 99th percentile execution latency between the proxy and the Redis server</td></tr>
<tr>
<td>Average read latency</td><td>latency_read</td><td>ms</td><td>The average execution latency of read commands between the proxy and the Redis server. For more information on read command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Average write latency</td><td>latency_write</td><td>ms</td><td>The average execution latency of write commands between the proxy and the Redis server. For more information on write command types, see <a href="https://intl.cloud.tencent.com/document/product/239/38743">Command types</a>.</td></tr>
<tr>
<td>Average latency of other commands</td><td>latency_other</td><td>ms</td><td>The average execution latency of commands (excluding write and read commands) between the proxy and the Redis server</td></tr>
</tbody></table>

## Viewing Monitoring Data
### Step 1. Select monitoring metrics
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/471e4894326f328c2648539c861006b4.png)
4. Click the **Performance Trends** tab, select the target performance metrics in the metric category drop-down list, and click **Save**.
To apply the selected performance metrics to all the TencentDB for Redis instances under your account, click **Save and Apply to All Instances** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2aed7a308b1a907643325d736b213ae2.png)

### Step 2. Set the collection granularity
In the top-right corner of the **Performance Trends** tab, set the collection granularity of the monitoring data in the drop-down list on the right of **Auto-Refresh** to **5s**, **15s**, or **30s** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/62c0653020be652ddc4072a971437655.png)

### Step 3. View the change trends of the monitoring metrics
#### Viewing monitoring metrics in different dimensions
Below the metric categories on the **Performance Trends** tab, you can view the monitoring metric data by instance, Redis node, and proxy node as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/b4a6898a6a71bee1c0800e35073ca8a9.png)
![img](https://qcloudimg.tencent-cloud.cn/raw/b16542ef1ece75dd1c737b728952b289.png)

#### Comparing the performance metrics of multiple nodes
1. On the **Performance Trends** tab, click **Multi-Node Performance Comparison**.
2. In the **Multi-Node Performance Comparison** panel, click **Create Multi-Node Performance Comparison Task**.
3. In the **Create Multi-Node Performance Comparison Task** window, click <img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" /> in the selection box next to **Monitoring Time** to select the monitoring time period, select the target monitoring metric in the **Monitoring Metric** drop-down list, and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/99cd1e438fbe817a9177a44fb5fb8d86.png" style="zoom:67%;" />
4. Wait for the **Status** to become **Successful** in the task list in the **Multi-Node Performance Comparison** panel.
![](https://qcloudimg.tencent-cloud.cn/raw/475d8977ce18651b964b228515031df0.png)
5. Click **View** in the **Operation** column to view the comparison data of all Redis nodes. The connections metric is used as an example as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/87d678d8f47f9f5e0b25165559fa3a5f.png)

#### Switching between real-time and historical views
On the **Performance Trends** tab, the real-time monitoring data is displayed by default.
- In routine Ops monitoring, database instance metrics can be monitored in real time.
- When you need to locate exceptions, you can click **Historical** to analyze the monitoring data in a past time period.
  - The monitoring data in the last 1 hour, 3 hours, and 7 days can be viewed.
  - Click <img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" /> to view the monitoring data in any time period in the last 30 days.
![](https://qcloudimg.tencent-cloud.cn/raw/fead86e3fbdad4920f39bae59ad40af2.png)

#### Comparing performance metrics in different time periods
1. On the **Performance Trends** tab, click **Historical** and then click **Add Time Comparison**.
2. In the time selection box, select two time periods for comparison.
3. Select the target monitoring metrics and hover over the change trend in the monitoring view to compare the monitoring data in the two time periods.
![](https://qcloudimg.tencent-cloud.cn/raw/21587e43c6c891a2c90cb01ab073fa2b.png)

#### Displaying monitoring metric data in chart
- Click <img src="https://qcloudimg.tencent-cloud.cn/raw/dde18545656758e343c3ec19099f62ce.png" style="zoom:50%;" /> next to **Show Statistics** as shown below to display the max, min, and average values of each monitoring metric in a table.
  ![](https://qcloudimg.tencent-cloud.cn/raw/acbed97fab46af985dfbd18edfa01523.png)
- Click <img src="https://qcloudimg.tencent-cloud.cn/raw/1ae8fbf920c91e7fc2b1caad2022eecd.png" style="zoom: 50%;" /> in the top-right corner of any monitoring view to display the max, min, and average values of the monitoring metric in a table.
The **Network Usage** metric is used as an example as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/8f8d632745bead98b62dd4e38f6d2184.png)

#### Viewing monitoring data through chart interaction
The **Chart Interaction** feature is suitable for analyzing the data of a monitoring view and its associated monitoring views.

1. In the top-right corner of the **Performance Trends** tab, click <img src="https://qcloudimg.tencent-cloud.cn/raw/dde18545656758e343c3ec19099f62ce.png" style="zoom:33%;" /> next to **Chart Interaction**.
2. In any of the monitoring views to be analyzed, select a time point and click it, and the data at the same time point will be fixed for display in other monitoring views.
3. You can click **Deselect the Time Point** in the top-right corner of the monitoring view to cancel the fixed display.
![img](https://qcloudimg.tencent-cloud.cn/raw/47b690c8cb3c1cd4a4e5fdff8c8ecd76.png)

#### Customizing monitoring metric for comparative analysis
Click <img src="https://qcloudimg.tencent-cloud.cn/raw/b71f9ac5a20130276b98f188345f0db6.png" style="zoom:50%;" /> in the top-right corner of any monitoring view to add monitoring metrics of other types for comparative display and analysis.
![](https://qcloudimg.tencent-cloud.cn/raw/4c493cf9c9dfd744e46632b5b96fe9b0.png)

#### Switching between one-column and two-column mode of monitoring view
Click <img src="https://qcloudimg.tencent-cloud.cn/raw/fffff5c980c476e903a35c4b5659b22c.png" style="zoom:50%;" /> on the right of **Chart Interaction** in the top-right corner to switch between the one-column and two-column modes. The former is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/76409901331ba51070907b5710ccfa90.png)

#### Dragging monitoring view
The monitoring views can be freely dragged to flexible adjust their order for efficient display and analysis.

#### Zooming in on monitoring view
Drag the icon in the bottom-right corner of any monitoring view to zoom in on the image for clearer display of the metric trends.
![](https://qcloudimg.tencent-cloud.cn/raw/732985ec960628dc9b2885cb23be3d9c.png)
