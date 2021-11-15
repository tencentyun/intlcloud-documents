## Overview
The slow SQL analysis feature calculates, samples, and aggregates records and execution information (source information, number of executions, execution duration, result set, scan set, etc.) of slow SQL statements on the instance. This feature analyzes the performance of slow SQL statements based on the execution plan, comprehensive resource consumption, sizes of scan and result sets, and index usage rationality of the aggregated SQL statements and provides optimization suggestions.
>Currently, slow SQL analysis is supported only for TencentDB for MySQL (excluding the basic single-node instance).


## Directions
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/slow-sql) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Slow SQL Analysis** tab.
>?The **SQL Statistics** section displays the number of slow queries and CPU utilization of the instance. You can adjust the time range to view slow SQL statements. If the instance has slow SQL statements, the quantity and occurrence points in time will be displayed in the view.
2. You can click to select a single time period or drag to select multiple time periods for slow logs in the **SQL Statistics** bar chart, and the aggregated SQL template and execution information (including the number of executions, total execution duration, scanned rows, and returned rows) will be displayed below. Each column of data can be sorted in ascending or descending order. The duration distribution section on the right displays the distribution intervals of the overall SQL statement execution duration in the selected time period.
![](https://main.qcloudimg.com/raw/0659dcb5dfb47bf00c4df2646946f0ce.png)
3. Click an aggregated SQL template, and specific SQL analysis and statistics will be displayed on the right.
 - On the analysis page, you can view the complete SQL template, SQL statement samples, optimization suggestions, and descriptions. You can optimize your SQL statements based on the expert suggestions provided by DBbrain to improve the SQL statement quality and reduce delay.
![](https://main.qcloudimg.com/raw/f72dcf38d05fc7381007502e930f3014.png)
 - On the statistics page, you can perform cross-sectional analysis on the root cause of a slow SQL statement based on the percentages of total lock wait time, total scanned rows, and total returned rows in the statistics report, and then optimize the statement accordingly. You can also view the execution duration distribution intervals of the specified type of aggregated SQL statements and the percentage of access source IPs.
![](https://main.qcloudimg.com/raw/a3d611bcbc75bdd0e74e369c277d1cb5.png)
