This document describes how to view database audit logs and fields.

## Prerequisites
You have enabled the audit service as instructed in [Enabling Audit Service](https://intl.cloud.tencent.com/document/product/1098/44614).

## Viewing an Audit Log
>?The audit log display time is down to milliseconds, facilitating more precise sorting and problem analysis of SQL commands.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Database Audit** on the left sidebar and select the region at the top.
3. Click **Enabled** after **Audit Status** to filter instances for which the audit service is enabled.
4. Find the target instance in the audit instance list, or search for it by resource attribute in the search box, and click **View Audit Log** in the **Operation** column to enter the **Audit Log** tab and view logs.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mTL3750_43.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/puNd887_44.png)

### Tool list
 - In the **time box**, select a time period to view corresponding audit results.
>?You can select any time period with data for search. Up to the first 60,000 eligible records can be displayed.
 - In the **search box**, you can search by key tag to view corresponding audit results. Common key tags include SQL command details, client IP, database account, database name, thread ID, policy name, SQL type, duration (ms) longer than, affected rows more than, and returned rows more than.
  - You can separate multiple keywords by vertical bar "|" and separate multiple filter tags by carriage return.
  - You can filter IP addresses using the wildcard "*". For example, if you enter "client IP: 9.223.23.2*", IP addresses that start with "9.223.23.2" will be searched.
  - Combo search is supported. Selecting the key tag "SQL Command" allows you to separate filters using commas or spaces, and the logic relationship between them is AND. You may also use vertical bars ("|") to separate filters, and the logic relationship between them is OR.
>?When filtering by SQL command, the symbol `*` does not represent a fuzzy match. All SQL command searches are fuzzy searches.
>

### Log list
- In the **SQL Type** drop-down list, you can select multiple SQL types for filtering.
- The **Returned Rows** field represents the specific number of rows returned by executing the SQL command, which is mainly used to determine the impact of `SELECT` commands.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/BIIN020_45.png)

## Audit Fields
The following fields are supported in TDSQL-C for MySQL audit logs. On the **Audit Log** tab, click the download icon. After download, click the file list icon. On the page redirected to, copy the download address and access it to get the complete SQL audit logs.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NEW5155_46.png)
>!
>- Currently, you can download audit log files of a database instance only at the Tencent Cloud private network address by using a CVM instance in the same region.
>- Log files are valid for 24 hours. Download them promptly.
>- Up to 30 log files can be retained for one database instance. Delete files promptly after download.
>- The status of a very large log may fail to display. Shorten the log time range, split the large log to multiple logs, and download them.

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

