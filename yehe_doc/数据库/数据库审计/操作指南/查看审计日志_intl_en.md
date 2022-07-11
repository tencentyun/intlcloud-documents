
## Viewing Log
1. Log in to the [TencentDB for MySQL](https://console.cloud.tencent.com/dls/mysql), [TDSQL-C for MySQL](https://console.cloud.tencent.com/dls/cynosdb/instance), or [TencentDB for MongoDB](https://console.cloud.tencent.com/dls/mongodb) console, select **Database Audit** on the left sidebar, select a region at the top, and click the **Audit Log** tab.
2. In the audit instance section on the **Audit Log** tab, select a database instance with audit enabled to view its SQL audit logs. Or, on the **Audit Instance** tab, click an instance ID to enter the **Audit Log** tab and view audit logs.
>?The audit log display time is down to milliseconds, facilitating more precise sorting and problem analysis of SQL commands.

### Tool list
![](https://qcloudimg.tencent-cloud.cn/raw/a285a1b3e7e1dba10b34127448f9c0f3.png)
 - In the **time box**, select a time period to view audit results in the selected time period.
>?You can select any time period with data for search. Up to the first 60,000 eligible records can be displayed.
 - You can search by key tag to view related audit results. Common key tags include SQL command, client IP, database name, database account, SQL type, policy name, execution time, affected rows, and returned rows.
  - When entering multiple key tags for search, you can separate them by pressing "Enter".
  - You can filter IP addresses using the wildcard "*". For example, if you enter "client IP: 9.223.23.2*", IP addresses that start with "9.223.23.2" will be searched.
  - Combo search is supported. Selecting the key tag "SQL Command" allows you to separate filters using commas or spaces, and the logic relationship between them is AND. You may also use vertical bars ("|") to separate filters, and the logic relationship between them is OR.
>?When filtering by SQL command, the symbol `*` does not represent a fuzzy match. All SQL command searches are fuzzy searches.
>

### Log list
- In the **SQL Type** drop-down list, you can select multiple SQL types for filtering.
- The **Returned Rows** field represents the specific number of rows returned by executing the SQL command, which is mainly used to determine the impact of `SELECT` commands.
 ![](https://qcloudimg.tencent-cloud.cn/raw/8a035147191070ae4789aec12e67faf1.png)

## SQL Audit Fields
### TencentDB for MySQL and TDSQL-C for MySQL
The following fields are supported in TencentDB for MySQL and TDSQL-C for MySQL audit logs. You can click the following icon on the **Audit Log** tab in the [TencentDB for MySQL](https://console.cloud.tencent.com/dls/mysql) or [TDSQL-C for MySQL](https://console.cloud.tencent.com/dls/cynosdb/instance) console to get and view the complete SQL audit logs.
![](https://qcloudimg.tencent-cloud.cn/raw/40f34d23921fb707599548204d0dda6a.png)

| No. | Field Name | Description | Remarks |
| ---- | ------------- | ------------------------------------------------------------ | -------------------------------------- |
| 1    | host          | Client IP                                                     |   -                                           |
| 2    | dbname        | Database name                                                     |  -                                            |
| 3    | user          | Username                                                       |      -                                        |
| 4    | sql           | SQL statement                                                      |    -                                          |
| 5    | sqlType       | SQL statement type                                                  |   -                                           |
| 6    | errCode       | Error code                                                       | 0 indicates success                                    |
| 7    | affectRows    | Number of affected rows                                                     |     -                                         |
| 8    | checkRows     | Number of scanned rows                                                     |     -                                         |
| 9    | sentRows      | Number of returned rows                                                     |    -                                          |
| 10   | threadId      | Thread ID                                                       |       -                                       |
| 11   | ruleNum       | Audit rule ID                                                   |     -                                         |
| 12   | policyName    | Audit policy name                                                   |    -                                          |
| 13   | instanceName  | Instance name                                                       |    -                                          |
| 14   | timestamp     | Start time (s)                                               |   -                                           |
| 15   | nsTime        | Start Time (ns), which forms the start time accurate down to the nanosecond together with `timestamp` | Example: timestamp.nsTime 1577953020.887984015 |
| 16   | execTime      | Execution time (ms)                                            |    -                                          |
| 17   | cpuTime       | CPU time (μs)                                              |     -                                         |
| 18   | lockWaitTime  | Lock wait time (μs)                                           |    -                                          |
| 19   | ioWaitTime    | IO wait time (μs)                                           |     -                                         |
| 20   | trxLivingTime | Transaction execution time (μs)                                   |      -                                        |


