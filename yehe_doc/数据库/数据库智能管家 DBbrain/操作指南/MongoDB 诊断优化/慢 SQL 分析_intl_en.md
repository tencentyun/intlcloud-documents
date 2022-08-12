
## Feature description
The slow log analysis feature calculates, samples, and aggregates records and execution information (source information, number of executions, execution time, result set, scan set, etc.) of slow logs in the instance.

## Overview
![](https://qcloudimg.tencent-cloud.cn/raw/5f4a5d0fa152d96e76b6895919e0ff8d.png)

## Viewing slow SQL analysis
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/slow-sql) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Slow SQL Analysis** tab.
The **Slow Log Statistics** section displays the **Slow Queries** and **Max Cluster CPU Utilization** of the instance. You can adjust the time range to view slow SQL statements. If the instance has slow SQL statements, the quantity and occurrence points in time will be displayed in the view.
  - You can quickly set the time dimension for statistics collection to **Last 5 minutes**, **Last 10 minutes**, **Last hour**, **Last 3 hours**, **Last 24 hours**, or **Last 3 days**.
  - You can select **Instance** or **Mongod Node** as the statistical dimension.
2. You can click a single time range or drag to select multiple time ranges for slow queries in the **Slow Log Statistics** section, and the aggregated slow log template and execution information (including the number of executions, total execution duration, scanned rows, and returned rows) will be displayed below. Each column of data can be sorted in ascending or descending order.
    The consumed time distribution section on the right displays the overall consumed time distribution of slow logs in the selected time range.
    ![](https://qcloudimg.tencent-cloud.cn/raw/71fc967460f02fda40b9885936313e14.png)
3. Click an aggregated slow log, and its statistics and details will be displayed on the right.
 - On the **Statistics** tab, you can view the **Consumed Time Distribution**, **Time Consumed Ratio**, **Ratio of Scanned Rows**, and **Average Scanned Rows**.
 - On the **Details** tab, you can view the details of the **Command Template**, including the **SQL Statement**, **Namespace**, **Execution Time**, **Scanned Indexes**, **Returned Rows**, and **Scanned Rows**. You can also filter logs by **Time Range**, **Namespace**, or **Time Consumed** to query the details of historical SQL statements.
    You can pull the **Details** tab to the left to expand it horizontally or view the enlarged statistical chart on the **Details** tab on the homepage.
4. Export the data of slow logs.
   Click **Export** on the right of the slow log list to export the data of slow log analysis in CSV format for easier viewing.
