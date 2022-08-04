
## Overview
Slow log analysis in Redis is different from that in MySQL and TDSQL-C and counts the slow logs in two dimensions: instance and proxy.
- In the instance (Redis database instance) dimension, you can clearly view the CPU utilization, number of slow queries, consumed time statistics by log segment, and information of the entire slow log list.
- In the proxy (middleware cluster node) dimension, you can view the proxy's slow log statistics, consumed time statistics by segment, and details of the slow log list.

## Directions
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Slow Log Analysis** tab.
2. On the **Slow Log Analysis** tab, you can view instance-level and proxy-level slow logs.
   You can quickly set the time dimension for statistics collection to **Last 5 minutes**, **Last 10 minutes**, **Last hour**, **Last 3 hours**, **Last 24 hours**, or **Last 3 days**.
 - Instance-level slow log:   
![](https://qcloudimg.tencent-cloud.cn/raw/b85871fbf8926009a2b84e03bb6eefa7.png)
   - Slow Log Statistics: Click a single time range or drag to select multiple time ranges in the slow log statistics chart to view the slow log statistics in the corresponding time ranges.
   - Slow Query Statistics: This section displays the overall consumed time distribution of slow logs in the selected time range. The horizontal axis is the proportion of slow logs, and the vertical axis is the statistical period. When the cursor is over a certain statistical period, the proportion of slow logs in this period will be displayed.
   - Slow Log List: Click a slow log to view its analysis and statistics details. 
 - Proxy-level slow log.
3. Perform chart interaction for logs.
In the **Slow Log Statistics** module, click the time point you want to locate, and the information of the slow log generated at the time point and specific time consumed will be synchronously displayed.
4. On the **Slow Log Analysis** tab, click **Monitoring Details** in the top-right corner to add multiple time ranges or monitoring metrics for comparison.
5. In the **Slow Log List** below, click an aggregated command template, and specific command analysis and statistics will be displayed on the right.
 - On the **Analysis** tab, you can view:
    - Command template.
    - Command sample.
    - Optimization suggestion and description.
 - On the **Statistics** tab, you can view:
    - Execution duration distribution ranges of the specified type of aggregated commands.
    - Access distribution and proportion of source IPs (available for proxy nodes but not Redis nodes).
6. Export the data of slow log analysis.
   Click **Export** on the right of the slow log list to export the data of slow log analysis in CSV format for easier viewing.
   
   
