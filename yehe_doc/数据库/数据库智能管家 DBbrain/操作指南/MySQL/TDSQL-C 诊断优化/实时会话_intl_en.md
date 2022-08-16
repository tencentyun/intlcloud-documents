## Feature description

You can use DBbrain's real-time session feature to view the real-time session information of your instance, including **Performance Monitoring**, **Connection Monitoring**, **Active Session**, **SQL Throttling**, and **Hotspot Update Protection**.

## SQL statistics/Session statistics/Performance monitoring

Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/session) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Real-Time Session** tab.

The **Refreshing Frequency** is **15s** by default and can be modified as needed. You can also disable refresh.
![](https://qcloudimg.tencent-cloud.cn/raw/fc9833aba2b9ccfa1f873b346e23f237.png)

## Active session

On the **Active Session** tab, you can set the limit, filter by field, and enable or disable **Show Sleep Connection**.

- You can set the limit to 20, 50, or 100.
- **Filter by Field** supports filtering by **ID**, **USER**, **HOST**, **STATE**, **DB**, **COMMAND**, **INFO**, and **TIME** fields.
  You can filter threads by **All**, **Not Sleep**, or **Others** (including Binlog Dump, Change user, Close stmt, Connect, Connect Out, Create DB, Daemon, Debug, Delayed insert, Drop DB, Error, Execute, Fetch, Field List, Init DB, Kill, Long Data, Ping, Prepare, Processlist, Query, Quit, Refresh, Register Slave, Reset stmt, Set option, Shutdown, Sleep, Statistics, Table Dump, and Time).
- You can also enable **Show Sleep Connection**.
![](https://qcloudimg.tencent-cloud.cn/raw/a6a97e76d66ac9aa6aae42ddd9c65e82.png)

## Killing sessions
DBbrain allows you to kill sessions for easier session management.

**Kill current sessions**
Select target sessions and click **Kill Session**.
You can kill 1–100 sessions at a time.
![](https://qcloudimg.tencent-cloud.cn/raw/a23d6d6b859a22ed7f26f2ca6d2a52d5.png)
**Kill sessions during a period**
DBbrain offers the feature of killing sessions during a period. You can set the conditions for killing sessions, so that when the conditions are met, sessions will be killed automatically.

1. Task Settings.
   Set the conditions for killing sessions during a period (including **USER**, **HOST**, **DB**, **COMMAND**, **INFO**, and **TIME**) and set the **Execution Mode**.
>!
>- You can set one or more filter conditions which are evaluated using the logical AND operator. Then, all sessions that meet the conditions except system connections will be killed.
>- If only **Time** and **Duration** are set, all sessions that meet the conditions will be killed quickly.
>
![](https://main.qcloudimg.com/raw/4877a34820444c3cc521d4b5725f9a12.png)
2. Session Preview.
   After setting the task, you can preview the sessions to be killed in the **Session Preview** section. After killing sessions during a period is enabled, the generated sessions that meet the conditions will be automatically killed.
![](https://main.qcloudimg.com/raw/5bf56f57f7f895853aa7470befdc4c96.png)
3. Task Details.
   After setting the task, click **Details** in the top-right corner to view the details of the sessions killed during a period.

**View the history of killed sessions**
DBbrain provides the feature of viewing the history of killed sessions. To use this feature, click **History**.

## SQL throttling

DBbrain supports the SQL throttling feature to ensure service availability. You can create SQL throttling tasks to control the database requests and SQL concurrency by setting the **SQL Type**, **Max Concurrency**, **Throttling Duration**, and **SQL Keyword**. Multiple tasks do not conflict with each other.

>?
>- SQL throttling is supported only for TencentDB for MySQL (excluding the Basic Edition).
>- To create a SQL throttling task, you need to log in to the database account first.
>- If SQL throttling prevents a SQL statement from being executed, the error message `SQL rejected by CDB_SQL_FILTER` will be displayed.

- SQL Type: Select **SELECT**, **UPDATE**, **DELETE**, **INSERT**, or **REPLACE**.
- Max Concurrency: Set the maximum number of concurrent SQL executions. If the number of concurrent SQL executions containing specified keywords reaches this value, the SQL throttling policy will be triggered. If this value is set to 0, it restricts all matched SQL executions.
- Execution Mode: Select **Scheduled stop** or **Manual stop**.
- Throttling Duration: If you select **Scheduled stop**, you need to set how long the SQL throttling task runs.
- SQL Keyword: Set the keywords. SQL statements containing the specified keywords will be restricted. Multiple keywords should be separated by comma and are evaluated by using the logical `AND` operator. Comma cannot be used as a keyword.
![](https://main.qcloudimg.com/raw/55f634cf8d9367c122f694b1e8fbc88b.png)
On the **SQL Throttling** tab, the list displays the **SQL Type**, **Status**, **Keyword**, **Start Time**, **Remaining Time**, **Max Concurrency**, and **Operation**.

- Click **Details** in the **Operation** column to view SQL throttling details.
- After a SQL throttling task is enabled, it will remain in the **Running** status until its remaining time decreases to zero. You can click **Disable** in the **Operation** column to disable the task, and its status will change to **Terminated**.
- After a SQL throttling task is enabled, its status will change to **Terminated** once its remaining time decreases to zero.
- Click **Delete** in the **Operation** column to delete a SQL throttling task in the **Terminated** or **Completed** status.
![](https://main.qcloudimg.com/raw/5925c45ce935ae8f7e990214ae4c568b.png)
## Hotspot update protection

DBbrain provides the hotspot update protection feature. According to the statement queuing mechanism, this feature queues the statements with the same conflict in the memory queue. It reduces the overheads of lock conflict and improves the database performance in high concurrency scenarios.
>?Hotspot update protection is supported only for TencentDB for MySQL (excluding the Basic Edition).

On the **Hotspot Update Protection** tab, click **Create Task** to create a hotspot update protection task. You can set the **Wait Timeout Threshold** and **Execution Mode** (**Scheduled stop** or **Manual stop**). If you select **Scheduled stop**, you can set the **Execution Time**.
![](https://main.qcloudimg.com/raw/0d25d8a3eeb8c4cf8542c66a7681dfc4.png)
On the **Hotspot Update Protection** tab, the list displays the **Status**, **Start Time**, **Execution Time**, **Remaining Time**, **Wait Timeout Threshold**, and **Operation**.
- For a task in the **Running** status, click **Disable** in the **Operation** column to terminate it.
- For a task in the **Terminated** or **Completed** status, click **Delete** in the **Operation** column to delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/11bc030a620090e3bb020b9551a20c32.png)
