## Problem Description
Generally, high CPU utilization of a TencentDB for MySQL instance will cause system exceptions, such as slow response, failure to get connections, and timeout. Performance drop is usually caused by a high number of retries upon timeout, and high CPU utilization is usually caused by exceptional SQL statements. High numbers of lock conflicts, lock waits, or uncommitted transactions may also cause high CPU utilization of TencentDB for MySQL instances.

When a database executes business query or statement modification tasks, the CPU will request data blocks (8 KB by default) from the memory.
- If the memory has the target data, the CPU will execute the computation task and return the result to you, which may involve actions requiring high CPU usage such as sorting.
- If the memory does not have the target data, the database will get the data from the disk.

The two data acquisition processes above are called logical read and physical read, respectively. Therefore, poorly performing SQL statements can easily cause the database to generate a lot of logical reads during the execution, resulting in high CPU utilization. They may also make the database generate a lot of physical reads, resulting in high IOPS and I/O latency.

## Solutions
DBbrain provides three key features you can use to troubleshoot and optimize exceptional SQL statements that cause high CPU utilization.
- Exception diagnosis: detects and diagnoses exceptions 24/7 and provides optimization suggestions in real time.
- Slow SQL analysis: analyzes slow SQL statements of the current instance and provides corresponding optimization suggestions.
- Audit log analysis: performs in-depth analysis on SQL statements and provides optimization suggestions based on TencentDB audit data (full SQL).


### Method 1 (recommended). Use the **exception diagnosis** feature to troubleshoot database exceptions
The exception diagnosis feature can proactively locate and perform optimization for failures, and does not require OPS experience. It can diagnose not only exceptions of high CPU utilization but also all common exceptions and failures of TencentDB for MySQL instances.

Directions:
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **Exception Diagnosis** at the top.

2. Select (enter or search for) an instance ID in the top-left corner to switch to the target instance.
3. On this page, select "Real Time" or "History" and select the time period to be queried. If any failures exist in this period, the overview information will be displayed in "Diagnosis Prompt" on the right.  
4. Click **View Details** in the "Real-Time" or "Historical" tab or the target diagnosis item in "Diagnosis Prompt" to access the diagnosis details page.
 - Event Overview: includes the diagnosis items, start and end times, risk level, duration, and overview.
 - Symptom: includes symptom snapshots and performance trends of the exception event or health check event.
 - Intelligent Analysis: analyzes the root cause of the performance exception to help you locate the specific operation.
 - Expert Suggestion: provides optimization suggestions, including but not limited to SQL optimization (index and rewrite), resource configuration optimization, and parameter fine-tuning.

5. Select the **Expert Advice** tab to view the optimization suggestion provided by DBbrain for this failure. In this example, the optimization suggestion is provided for the SQL statement, which lacks the corresponding index during execution. In this case, full-table scan needs to be performed and a single execution is costly. Therefore, the CPU utilization tends to be high or even 100% in high-concurrence scenarios.


### Method 2. Use the "slow SQL analysis" feature to troubleshoot SQL statements that lead to high CPU utilization
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **Slow SQL Analysis** at the top.
2. Select (enter or search for) an instance ID in the top-left corner to switch to the target instance.
3. On this page, select the time period to be queried. If slow SQL statements exist in this period, the time points of occurrence and the number of statements will be displayed in a bar chart in "SQL Statistics".
Click the bar chart, and the information of all corresponding slow SQL statements (those aggregated by template) will be displayed in the list below, and the duration distribution of SQL statements in the specified time period will be displayed on the right.

4. You can identify and filter SQL statement execution data in the SQL statement list through the following method:
 1. Sort the SQL statements by average duration (or maximum duration). Examine the top SQL statements in terms of duration. We do not recommend you sort the statements by total duration, as the data may be affected by a high number of executions.
 2. Then, examine the numbers of returned rows and scanned rows.
    - If there is an SQL statement with the same "number of returned rows" and "number of scanned rows", it is very likely that the full table has been queried and returned.

    - If there are several SQL statements with a large number of scanned rows but no or few returned rows, it means that the system generated a lot of logical and physical reads. If the volume of the data to be queried is too high and memory is insufficient, the request will generate many physical I/O requests and consume lots of I/O resources. Too many logical reads will occupy too many CPU resources, resulting in high CPU utilization.

5. Click an SQL statement to view its details, resource consumption, and optimization suggestions.
 - On the analysis page, you can view the complete SQL template, SQL statement samples, optimization suggestions, and description. You can optimize your SQL statements based on the expert suggestions provided by DBbrain to improve SQL performance and reduce SQL execution duration.

 - On the statistics page, you can perform cross-sectional analysis of the root cause of a slow SQL statement based on the percentages of total lock wait time, total scanned rows, and total returned rows in the statistics report, and then optimize the statement accordingly.
 - On the duration distribution page, you can view the execution duration distribution intervals of the specified type of aggregated SQL statements and the access percentage of source IPs.

### Method 3. Use the "audit log analysis" feature to troubleshoot SQL statements that cause high CPU utilization
Prerequisites: the instance needs to have the database audit feature enabled.

1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **Audit Log Analysis** at the top.
2. Select (enter or search for) an instance ID in the top-left corner to switch to the target instance. 
3. You can select to display the insight view by QPS or the number of slow queries. Click **Create Audit Task** in the top-right corner of the view. and select the task start time and duration. Then, click **Confirm**.
After the task is created, it will be displayed in the task list. After the task is completed, find the target record and click **View SQL Analysis** to access the SQL analysis details page.

4. On the SQL analysis page, you can display the view by SQL Type, Host, User, or SQL Code. You can specify a time period to expand the view and view data at specific time points.
The aggregated details and execution information of SQL statements in the specified time period are displayed in the table below. If you select a time period and stretch it in the table, the SQL data will change accordingly, and only the SQL analysis result of the selected time period will be displayed.

5. The aggregated SQL statement execution information (including the number of executions, total, maximum, and minimum delay, and total, maximum, and minimum numbers of affected rows) is displayed in the table in the bottom of the SQL analysis details page. You can sort SQL statements by multiple metrics to identify the ones that require optimization.
Example:
Sort the SQL statements by the number of executions to identify the ones whose number of executions is high or has an exception change. Then, analyze the rationality of the number of executions and optimize the statements based on DBbrain's suggestions.

 - By viewing the number of executions, total delay, and maximum delay, you can find that the average execution delay of the first and second SQL statements with the highest numbers of executions is very short, which indicates that the performance of the two SQL statements is normal.
 You can see that the single execution time of the third statement is about 100 seconds. Since its number of executions is relatively low, its total delay ranks third. However, this SQL type must be optimized. You can click the SQL to view information such as expert suggestions, the resource consumption analysis curve, and the source IP analysis provided by DBbrain.

 - There is another type of SQL statement that requires your attention. You can see that the difference between the maximum and minimum delays of the fourth statement is large (more than 200 seconds). This indicates that the entire system is fluctuating, and you need to analyze whether the fluctuation is caused by network problems or changes in the execution plan due to data volume change.

 - If the number of executions and the average duration of SQL statements are relatively rational and the SQL statements with a large number of executions are optimal, it means that the performance has reached a bottleneck. We recommend you [upgrade the instance specification configuration](https://intl.cloud.tencent.com/document/product/236/19707) or use [read/write separation](https://intl.cloud.tencent.com/document/product/236/7270) to disperse SQL statements with a large number of executions, or use the preset cache database for optimization.


