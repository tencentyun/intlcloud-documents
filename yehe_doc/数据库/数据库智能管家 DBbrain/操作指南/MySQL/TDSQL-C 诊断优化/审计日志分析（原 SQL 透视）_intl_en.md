The audit log analysis (formerly SQL Pivot) feature can carry out in-depth SQL analysis for a database instance. It can statistically analyze, sample, and aggregate all SQL statements and their execution information (source, number of executions, execution duration, result set, scan set, etc.) based on the audit logs generated by the database within a specified time range.

The audit log analysis feature analyzes the SQL performance based on the execution plan result, comprehensive resource consumption, sizes of scan and result sets, and index usage rationality of the aggregated SQL statements. Then, it provides optimization suggestions for poorly performing SQL statements by taking into account the index conditions and database/table design. This document describes how to perform full SQL analysis and view analysis details.
## Prerequisites
You need to enable the database audit feature for your instance first as instructed in [Enabling TencentDB for MySQL Audit](https://intl.cloud.tencent.com/document/product/1102/41311).

## SQL view
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/performance/sql-audit/log-audit) and select **Performance Optimization** on the left sidebar. On the displayed page, select the **Audit Log Analysis** tab at the top to view the **QPS**, **Slow Queries**, and **CPU Utilization** metrics of the selected database instance. Drag the slider on the gray bar to zoom in the diagnosis view during the period and view it at a finer granularity.

## Creating an analysis task
1. On the [Audit Log Analysis](https://console.cloud.tencent.com/dbbrain/performance/sql-audit/log-audit) tab, click **Create Analysis Task**.
2. In the pop-up window, select the **Start Time** and **Time Range** for the task and click **OK**.
3. After the task is created, you can view the analysis result and delete the task in the task list. Click **View SQL Analysis** to enter the SQL analysis page.

## Viewing SQL analysis
1. On the SQL analysis page, you can select a view in the **SQL Type**, **Host**, **User**, **SQL Code**, or **Time** dimension. You can also specify a time range to zoom in the view and check out data at specific time points. The aggregated details and execution information of SQL statements in the specified time range are displayed in the table below.
   - If you select a time range and zoom in it in the table, the SQL data will change accordingly, and only the SQL analysis results in the selected time range will be displayed. After zooming in the view, you can click **Reset** in the top-right corner to restore the view.
   - You can select **SQL Type** or click a legend to filter SQL data, and the data will change accordingly in the table. For example, if you want to view only SELECT requests, you can click other legends to gray them out.
   - In the chart, click a point of the curve to view the monitoring data in the point of time, including the data of SELECT, INSERT, UPDATE, DELETE, REPLACE, and other requests.
2. Click the SQL template on the target row, and the SQL statement details will be displayed on the right.
   - On the analysis page, you can view and copy a specific SQL statement and optimize it based on the provided optimization suggestion or description.
 In the **Analysis** pop-up window, click **Optimization Comparison** in the top-right corner to view the SQL statement's execution plan, index advice, table structure, and performance before and after optimization.
 The performance of an optimized SQL statement is estimated based on the analysis of the statistics of database tables related to the statement, the OPTIMIZER_SWITCH configuration, and the index selectivity. A chart is used to visually show the decrease in the performance. You can also compare the execution plans before and after SQL optimization to further verify the optimization results.
- On the **Statistics** tab, you can view the statistical analysis and execution duration track of the specified types of SQL statements by **Host**, **User**, or **SQL Code**.

## Advanced audit capabilities of TDSQL-C for MySQL
In addition to the **All Request Analysis** feature, TDSQL-C for MySQL also supports **Request Time Consumption Analysis (P99)** and **Request Time Consumption Analysis (P95)**, which are more accurate and in-depth.

>! This feature is supported for TDSQL-C 2.0.12 or later. If your database instance is on an earlier version, you need to upgrade it first.
>
Advanced analysis capabilities are provided for SQL access latency based on real-time full audit log analysis.

## Content audit for uncommitted transactions

After enabling the audit log feature, you can get the content and audit analysis result of an uncommitted transaction.
On the **Exception Diagnosis** tab, if an uncommitted transaction is detected, an alarm will be displayed in **Diagnosis Prompt**. You can click **View** to enter the event alarm details page.
On the **Transaction Details** tab, you can view the real-time analysis of the audit log, where DBbrain analyzes and aggregates the content of the uncommitted transaction for display.
You can click a SQL statement to get its audit result items.

