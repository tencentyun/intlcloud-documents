### What is the slow query collection threshold in TencentDB for SQL Server?
The default slow query collection threshold in TencentDB for SQL Server is one second. SQL statements whose execution duration exceeds one second will be recorded into slow logs.

### Can I modify the slow query collection threshold in TencentDB for SQL Server?
The default slow query collection threshold in TencentDB for SQL Server is one second, which cannot be modified in the console. To modify it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. The threshold modification won't affect your business.

### Do slow query logs in TencentDB for SQL Server use my storage space?
No.

### Can I view the slow SQL table in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the target instance ID in the instance list. On the slow query log page, query and download slow query logs as instructed in [Querying and Downloading Slow Query Log](https://www.tencentcloud.com/document/product/238/47569). The slow SQL table of TencentDB for SQL Server is not displayed by default. You can view it after connecting to the instance through SSMS. If you don't have relevant permissions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for escalating your database account permissions.

### How do I analyze slow SQL queries in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver#/) and click the ID of the target instance to enter the slow query log page. For more information, see [Querying and Downloading Slow Query Log](https://www.tencentcloud.com/document/product/238/47569). Download slow logs from the console. The downloaded file is in .xel format. You can open the .xel file in SSMS to view specific slow SQL queries. To optimize slow queries, you can copy them, enable the execution plan feature to view their specific execution plans, and optimize them accordingly. For more information, see [Display an Actual Execution Plan](https://docs.microsoft.com/en/sql/relational-databases/performance/display-an-actual-execution-plan?view=sql-server-ver16).

[](id:SFHZDQL)
### Will transaction logs in TencentDB for SQL Server be automatically cleared?
TencentDB for SQL Server transaction logs will be cleared automatically once every 30 minutes.

### Can I view audit logs in TencentDB for SQL Server?
No.

### Can I view error logs in TencentDB for SQL Server?
Currently, you cannot view error logs in the TencentDB for SQL Server console. However, you can directly view instance logs in SSMS.

### How do I get the error logs of TencentDB for SQL Server through commands?
Log in to the SQL Server client and run the following query statement in the query box to query error logs:
```
Exec master.sys.sp_readerrorlog FileID,LogType,FilterText
```
- FileID: File ID of the error log. `0` indicates the latest log.
- LogType: Log type. Valid values: 1 (error logs); 2 (agent logs).
- FilterText: Query keyword, which can be `NULL`.

Sample:
```
exec master.sys.sp_readerrorlog 0,1,'error'
