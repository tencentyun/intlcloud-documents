## Feature Description

A slow query is defined as a query statement that takes more time than the specified value, and the statement is called a slow query statement. The slow log analysis feature performs statistical analysis on the number of slow queries by **instance** and **proxy** and gives expert optimization suggestions to help improve the database performance.

- In the instance (Redis database instance) dimension, you can view the CPU utilization, number of slow logs, consumed time statistics by log segment, and information of the entire slow log list.
- In the proxy (middleware cluster node) dimension, you can view the proxy's slow log statistics, consumed time statistics by segment, and details of the slow log list.

## Viewing Slow Log Analysis Data

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/46e8ecc4d95dcc99b11ca787ffa8ffc3.png)
4. Click the **Slow Log Analysis** tab. Then, select the dimension for viewing slow logs and set the query time period in the **Statistics** section.
   - Click **Instance** to view the instance's slow log statistics.
   - Click **Proxy Node** and select the target proxy ID in the drop-down list based on the change trend of the **CPU utilization** or the number of **slow queries**.
   - In the time box, click <img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" /> to select a time period of up to 4 days to view slow logs.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8cc3e8dc959866240ced4c9ad8b3c315.png" style="zoom: 50%;" />
5. View the slow log statistics change trend, slow query statistics, and slow log list.
 - **Slow log statistics change trend** 
   **Slow Log Statistics** displays the number of slow queries and CPU utilization. It enables you to quickly identify the CPU utilization value when the number of slow queries in the selected time period stays high. This helps you avoid computer lags or response failures caused by high CPU utilization.
 - **Slow query statistics**   
   **Slow Query Statistics** displays the proportion of the proxy node's slow queries by duration range, where the vertical axis represents the duration range, and the horizontal axis represents the proportion of slow queries.

 - **Slow log list**
    - **Slow Log List** displays the number and duration of slow query command executions. You can click **Export** to export the data to view and analyze it locally.
    - Click a command template to display the specific analysis, optimization suggestion, and statistics on the right.
      - The **Analysis** tab displays the command template, command sample, optimization suggestion, and description.
      - The **Statistics** tab displays the execution duration distribution of the aggregated commands, as well as the distribution and proportion of access source IPs (for proxies only and unavailable for Redis). 
 - **Chart interaction**
In the monitoring view of **Slow Log Statistics**, click the target time point to view the duration proportion of slow logs generated at the time point by range, as well as specific duration details. 
 - **Monitoring details**
On the **Slow Log Statistics** page, click **Monitoring Details** in the top-right corner. In the drop-down list, select the associated monitoring metrics and set the time period to compare the statistics of the maximum and average values of multiple metrics in the time period. Then, click **Add Time Comparison** to compare the statistics of two time periods.


