## Feature description

The SQL throttling feature is suitable for scenarios involving high CPU utilization caused by high traffic. You can create SQL throttling tasks to control the database requests and SQL concurrency by setting the **SQL Type**, **Max Concurrency**, **Throttling Duration**, and **SQL Keyword**.

> ?
>- SQL throttling is supported only for TencentDB for MongoDB 4.0. To upgrade to this version, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- If SQL throttling prevents a SQL statement from being executed, the error message `SQL rejected by CDB_SQL_FILTER` will be displayed.

## Creating a SQL throttling task

1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Real-Time Session** tab to view the **SQL Throttling** module.
2. Create a SQL throttling task.
    To create a SQL throttling task, you need to log in to your database first.
 - SQL Type: Select **Find**, **Insert**, **Update**, or **Delete**.
 - Max Concurrency: Set the maximum number of concurrent SQL executions. If the number of concurrent SQL executions containing specified keywords reaches this value, the SQL throttling policy will be triggered. If this value is set to 0, it restricts all matched SQL executions.
 - Execution Mode: Select **Scheduled stop** or **Manual stop**.
 - Throttling Duration: If you select **Scheduled stop**, you need to set how long the SQL throttling task runs.
 - SQL Keyword: Set the keywords. SQL statements containing the specified keywords will be restricted. Multiple keywords should be separated by comma and are evaluated by using the logical `AND` operator. Comma cannot be used as a keyword.
3. View the status and details of the SQL throttling task.
 - Click **Details** in the **Operation** column to view SQL throttling details.
 - After a SQL throttling task is enabled, it will remain in the **Running** status until its remaining time decreases to zero. You can click **Disable** in the **Operation** column to disable the task, and its status will change to **Terminated**.
 - After a SQL throttling task is enabled, its status will change to **Terminated** once its remaining time decreases to zero.
 - Click **Delete** in the **Operation** column to delete a SQL throttling task in the **Terminated** or **Completed** status.

## Use case and effect of SQL throttling 

The database traffic was too high, resulting in a high CPU utilization.

1. The **MongoTop** tab in the console shows that the traffic of the `test.test11` table was too high. If the main business traffic was the read traffic to the `test.test10` table, then the traffic to the `test.test11` table was abnormal traffic.
![](https://qcloudimg.tencent-cloud.cn/raw/31da85a5dd4435e6866ad42a7c02cad2.png)
2. SQL throttling was enabled to throttle the traffic to the `test.test11` table.
3. As shown in the CPU performance trend chart below, CPU utilization dropped rapidly after throttling was enabled.
![](https://qcloudimg.tencent-cloud.cn/raw/b42387ee155cf4bdeb13763403189070.png)

 
