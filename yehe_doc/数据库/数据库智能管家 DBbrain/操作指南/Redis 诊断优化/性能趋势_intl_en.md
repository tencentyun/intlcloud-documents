## Feature description

You can select multiple performance metrics for Redis performance trends. Specifically, you can switch instances (Redis database instances), Redis nodes (between nodes, such as between node A and node B), and proxy nodes (middleware cluster nodes). You can also select performance metrics, such as real-time/historical views, monitoring granularities, single metric view/comparison view, and multiple views and comparison views of instances, Redis nodes, and proxy nodes.

## Supported performance metrics

DBbrain currently supports monitoring the following performance metrics of TencentDB for Redis:

<table>
<tr><th>Category</th><th>Subcategory</th><th>Metric</th></tr>
    <tr><td rowspan=7>Resource Monitoring</td>
<td>CPU</th><td>CPU</td></tr>
<tr>
<td rowspan=2 >Memory</td>
<td>Memory</td></tr>
<tr><td>Memory Usage</td></tr>
<tr>
<td rowspan=2>Storage Space</td>
<td>Storage Utilization</td></tr>
<tr><td>Used Storage Space</td></tr>
<tr>
<td rowspan=2>Traffic</td>
<td>Outbound Traffic</td></tr>
<tr><td>Inbound Traffic</td></tr>
<tr>
<tr><td rowspan=13>Redis</td>
<td>Key Information</th><td>Total Keys, Expired Keys, Evicted Keys</td></tr>
<tr>
<td rowspan=2 >Memory</td>
<td>Memory Usage</td></tr>
<tr><td>Memory Utilization</td></tr>
<tr>
<td rowspan=1>Replication Delay</td>
<td>Replication Delay</td></tr>
<tr>
<td rowspan=1>Network Usage</td>
<td>Network Usage</td></tr>
<tr>
<td rowspan=4>Request</td>
<td>Total Requests</td></tr>
<tr><td>Read Request</td></tr>
<tr><td>Write Request</td></tr>
<tr><td>Other Requests</td></tr>
<tr>
<td rowspan=4>Response</td>
<td>Slow Queries</td></tr>
<tr><td>Read Request Hit</td></tr>
<tr><td>Read Request Miss</td></tr>
<tr><td>Read Request Hit Rate</td></tr>
<tr>
<tr><td rowspan=23>Proxy</td>
<td>CPU</th><td>CPU Utilization</td></tr>
<tr>
<td rowspan=2 >Traffic</td>
<td>Inbound Traffic</td></tr>
<tr><td>Outbound Traffic</td></tr>
<tr>
<td rowspan=5>Request</td>
<td>Total Requests</td></tr>
<tr><td>Key Requests</td></tr>
<tr><td>Mget Requests</td></tr>
<tr><td>Execution Error</td></tr>
<tr><td>Big Value Request</td></tr>
<tr>
<td rowspan=4>Network Usage</td>
<td>Connections</td></tr>
<tr><td>Connections per Sec</td></tr>
<tr><td>Disconnections per Sec</td></tr>
<tr><td>Abnormal Disconnections per Sec</td></tr>
<tr>
<td rowspan=5>Network Utilization</td>
<td>Connection Utilization</td></tr>
<tr><td>Inbound Traffic Utilization</td></tr>
<tr><td>Outbound Traffic Utilization</td></tr>
<tr><td>Inbound Traffic Throttling Trigger</td></tr>
<tr><td>Outbound Traffic Throttling Trigger</td></tr>
<tr>
<td rowspan=6>Latency</td>
<td>Avg Execution Latency</td></tr>
<tr><td>Max Execution Latency</td></tr>
<tr><td>P99 Execution Latency</td></tr>
<tr><td>Avg Read Latency</td></tr>
<tr><td>Avg Write Latency</td></tr>
<tr><td>Avg Latency of Other Commands</td></tr>
</tbody></table>

## Viewing performance trends

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Performance Trends** tab.
2. Set monitoring metrics.  
   - Metric categories: Include CPU, memory, network, latency, request, and response.
   - Select performance metrics: You can select all metrics, custom metrics, and various views.
     - Filter global metrics
       ![](https://qcloudimg.tencent-cloud.cn/raw/2f57f8179bc1a0bb5254f12775ee6302.png)
     - Filter one single metric
       ![](https://qcloudimg.tencent-cloud.cn/raw/c8c0b91ba2546aa97d1a960a061c21fa.png)
     - Switch between chart views
       ![](https://qcloudimg.tencent-cloud.cn/raw/c9c080f6f598bf0ebcadcae9522b45a5.png)   
3. Set the monitoring dimension.
   You can set the monitoring dimension to **Instance**, **Redis Node**, or **Proxy Node**. 
    - Instance: It displays the monitoring view of the entire instance.
    - Redis Node: It displays the comparison trend views of relevant metrics on each Redis node.
    - Proxy Node: It displays the comparison trend views of relevant metrics on each proxy node.  
   If you select **Proxy Node**, you can select the **Aggregate view** or **Node view**.
   - In **Aggregate view** mode, the information of all proxy nodes is displayed. You need to select a metric in the top-left corner to display the single-metric information of all nodes. Click **Details** next to each metric to enter the **Node view**.
     ![](https://qcloudimg.tencent-cloud.cn/raw/4ddbcd931e487408ae55d4a9ee4f9df0.png)
   - In **Node view** mode, the information of all monitoring metrics of a node is displayed.
      ![](https://qcloudimg.tencent-cloud.cn/raw/c549143800cc6366654d482e86bcac90.png)
4. Switch between the **Real-Time** and **Historical** views.
   DBbrain allows you to switch between real-time and historical data. According to the selected time view, different granularities are provided. Single metric view and comparison view are also available.
5. Enable chart interaction.  
   For one single instance, node, or proxy, you can view relevant metric trend comparison, add custom metrics, and view the performance metric trend comparison by time.
   After you enable chart interaction, when you hover over a data point in any monitoring view, the data at the same time point will be displayed in other monitoring views. Click the data point to pin it for display. To unpin it, click **Deselect the Time Point**.
![](https://qcloudimg.tencent-cloud.cn/raw/f306800350c58f544135f622ff098f47.png)  
6. Show statistics.
   Metric monitoring charts support displaying specific monitoring data simultaneously. After **Show Statistics** is enabled, the table data will be displayed below each monitoring chart.
   ![](https://qcloudimg.tencent-cloud.cn/raw/54733e708e0e6617ba45ef22d11c2de1.png)
7. Switch between the one-column and two-column modes, drag a monitoring view, or zoom in a monitoring view.
   - **Switching between the one-column and two-column modes**: Click the button on the right of **Chart Interaction** in the top-right corner to switch.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ca4757c9f39a3ee954710cd041269692.png)
   - **Dragging a monitoring view**: Click the border of a monitoring view to drag it to the desired position.
   - **Zooming in a monitoring view**: Drag the icon in the bottom-right corner of a monitoring view to zoom it in for fine-grained display of the trend of one single performance metric.
   ![](https://qcloudimg.tencent-cloud.cn/raw/66a644cc813bd68c20320f63f3008573.png)

