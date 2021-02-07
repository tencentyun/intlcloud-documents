You can use the real-time session feature of DBbrain to view the real-time session information of your instance, including performance monitoring, connection monitoring, running thread monitoring, SQL throttling, and hotspot update protection. This document describes how to use the real-time session feature.

>?Currently, the real-time session feature (including SQL throttling and hotspot update protection) is supported only for TencentDB for MySQL (excluding the Basic Edition).
## Performance and Connection Monitoring
Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/session) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Real-Time Session** tab.
- The **Performance Monitoring** module displays in real time the number of running threads and the CPU utilization of the instance.
- The **Connection Monitoring** module displays in real time the maximum number of connections and the number of active connections of the instance.
![](https://main.qcloudimg.com/raw/03c23c17ff637f50f40a8b4d8e8e8dce.png)

## Running Threads
This section visually displays the `SHOW PROCESSLIST` command execution result of your database instance, and the displayed data is refreshed once every five seconds by default. You can filter data based on your needs using the following dimensions:
- Thread types: All, Query, or Not Sleep.
- Number of entries: 20, 50, or 100.
- Refresh intervals: 5 seconds, 15 seconds, or 30 seconds.
- You can choose to stop refresh or enable auto-refresh.
![](https://main.qcloudimg.com/raw/baf2ebab28d566ad37730b489379a309.png)

## Killing Sessions
DBbrain supports killing sessions in the console for ease of management. In the "Running Threads" section, you can select the lines of sessions in the list and click **Kill Session** in the upper-right corner to kill them.
- You can kill one or more sessions at a time. Currently, up to 100 sessions can be killed at a time.
- To kill sessions, you need to select the lines of the sessions first. 

## SQL Throttling
>?SQL throttling is supported only for TencentDB for MySQL (excluding the Basic Edition).
>
DBbrain supports the SQL throttling feature to ensure service availability. You can create SQL throttling tasks to control the database requests and SQL concurrency by setting the SQL type, maximum concurrency, throttling duration, and SQL keywords. Multiple tasks do not conflict with each other.
>?
>- To create a SQL throttling task, you need to log in to the database account first.
>- If SQL throttling prevents a SQL statement from being executed, the error message `SQL rejected by CDB_SQL_FILTER` will be displayed.
>
- SQL types: SELECT, UPDATE, DELETE, INSERT, or REPLACE.
- Maximum concurrency: the maximum number of concurrent SQL executions. If the number of concurrent SQL executions containing keywords reaches the maximum concurrency value, the SQL throttling policy will be triggered. If this value is set to 0, all matched SQL executions will be restricted.
- Execution mode: scheduled stop or manual stop.
- Throttling duration: if the scheduled stop is set as the execution mode, you need to set how long the SQL throttling task runs.
- SQL keywords: SQL executions containing keywords will be restricted. Multiple keywords should be separated by commas and are evaluated using the logical `AND` operator. Commas are not keywords.

In the "SQL Throttling" tab, the list displays the SQL type, status, keywords, start time, remaining time, maximum concurrency, and operations.
- Click **Details** in the **Operation** column to view SQL throttling details.
- After a SQL throttling task starts, it will remain in the "Running" status until its remaining time decreases to zero. Click **Close** in the **Operation** column to terminate the task in advance, and its status will change to "Terminated".
- After a SQL throttling task starts, its status will change to "Terminated" once its remaining time decreases to zero.
- Click **Delete** in the **Operation** column to delete a SQL throttling task in the "Terminated" or "Completed" status.


## Hotspot Update Protection
>?Hotspot update protection is supported only for TencentDB for MySQL (excluding the Basic Edition).
>
DBbrain provides the hot update protection feature. According to the statement queuing mechanism, the hot update protection feature queues the statements with the same conflict in the memory queue. The hot update protection feature reduces the overhead of lock conflict and improves the database performance in high concurrency scenarios.

In the "Hotspot Update Protection" tab, click **Create Task** to create a hotspot update protection task. You can set the wait timeout threshold and execution mode (scheduled stop or manual stop). If the scheduled stop is set as the execution mode, you can set the execution time.

In the "Hotspot Update Protection" tab, the list displays the status, start time, execution time, remaining time, wait timeout threshold, and operations.
- For a task in the "Running" status, click **Close** in the **Operation** column to terminate it in advance.
- For a task in the "Terminated" or "Completed" status, click **Delete** in the **Operation** column to delete it.
