This document describes how to view database audit logs and fields.

## Prerequisite
You have enabled audit in TDSQL-C for MySQL. For more information, see [Enabling Audit in TDSQL-C for MySQL](https://intl.cloud.tencent.com/document/product/1098/44614).

## Viewing Audit Logs
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
  - Combo search is supported. Selecting the key tag "SQL Command" allows you to separate filters by using commas or spaces, and the logic relationship between them is AND. You may also use vertical bars ("|") to separate filters, and the logic relationship between them is OR.
>?When you filter by SQL command, the symbol `*` does not represent a fuzzy match. All SQL command searches are fuzzy searches.
>

### Log list
- In the **SQL Type** drop-down list, you can select multiple SQL types for filtering.
- The **Returned Rows** field represents the specific number of rows returned by executing the SQL command, which is mainly used to determine the impact of `SELECT` commands.
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/BIIN020_45.png)

## Audit Fields
The following fields are supported in TDSQL-C for MySQL audit logs. On the **Audit Log** tab, click the download icon. After download, click the file list icon. On the page redirected to, copy the download address and access it to get the complete SQL audit logs.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NEW5155_46.png)

>!
>- Currently, you can download audit log files of a database instance only at the Tencent Cloud private network address by using a CVM instance in the same region. For example, to download the audit logs of database instances in Beijing region, download them with a CVM instance in Beijing.
>- Log files are valid for 24 hours. Download them promptly.
>- Up to 30 log files can be retained for one database instance. Delete unwanted files promptly after download.
>- The download may fail if you download too many logs at a time. To solve this problem, shorten the time range and download logs in batches.

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
| 15   | nsTime        | Start time (ns), which forms the start time accurate down to the nanosecond together with `timestamp` | Example: timestamp.nsTime 1577953020.887984015 |
| 16   | execTime      | Execution time (ms)                                            |    -                                          |
| 17   | cpuTime       | CPU time (μs)                                              |     -                                         |
| 18   | lockWaitTime  | Lock wait time (μs)                                           |    -                                          |
| 19   | ioWaitTime    | I/O wait time (μs)                                           |     -                                         |
| 20   | trxLivingTime | Transaction execution time (μs)                                   |      -                                        |

## Relationship Between SQL Statement Type and SQL Statement Mapping Object

| No. | SQL Statement Type | SQL Statement Mapping Object |
|---------|---------|---------|
| 0 | OTHER | All other SQL statement types except the following |
| 1 | SELECT | SQLCOM_SELECT |
| 2 | INSERT | SQLCOM_INSERT, SQLCOM_INSERT_SELECT |
| 3 | UPDATE | SQLCOM_UPDATE, SQLCOM_UPDATE_MULTI |
| 4 | DELETE | SQLCOM_DELETE, SQLCOM_DELETE_MULTI, SQLCOM_TRUNCATE |
| 5 | CREATE | SQLCOM_CREATE_TABLE, SQLCOM_CREATE_INDEX, SQLCOM_CREATE_DB, SQLCOM_CREATE_FUNCTION, SQLCOM_CREATE_USER, SQLCOM_CREATE_PROCEDURE, SQLCOM_CREATE_SPFUNCTION, SQLCOM_CREATE_VIEW, SQLCOM_CREATE_TRIGGER, SQLCOM_CREATE_SERVER, SQLCOM_CREATE_EVENT, SQLCOM_CREATE_ROLE, SQLCOM_CREATE_RESOURCE_GROUP, SQLCOM_CREATE_SRS |
| 6 | DROP | SQLCOM_DROP_TABLE, SQLCOM_DROP_INDEX, SQLCOM_DROP_DB, SQLCOM_DROP_FUNCTION, SQLCOM_DROP_USER, SQLCOM_DROP_PROCEDURE, SQLCOM_DROP_VIEW, SQLCOM_DROP_TRIGGER, SQLCOM_DROP_SERVER, SQLCOM_DROP_EVENT, SQLCOM_DROP_ROLE, SQLCOM_DROP_RESOURCE_GROUP, SQLCOM_DROP_SRS |
| 7 | ALTER | SQLCOM_ALTER_TABLE, SQLCOM_ALTER_DB, SQLCOM_ALTER_PROCEDURE, SQLCOM_ALTER_FUNCTION, SQLCOM_ALTER_TABLESPACE, SQLCOM_ALTER_SERVER, SQLCOM_ALTER_EVENT, SQLCOM_ALTER_USER, SQLCOM_ALTER_INSTANCE, SQLCOM_ALTER_USER_DEFAULT_ROLE, SQLCOM_ALTER_RESOURCE_GROUP |
| 8 | REPLACE | SQLCOM_REPLACE, SQLCOM_REPLACE_SELECT |
| 9 | SET | SQLCOM_SET_OPTION, SQLCOM_RESET, SQLCOM_SET_PASSWORD, SQLCOM_SET_ROLE, SQLCOM_SET_RESOURCE_GROUP |
| 10 | EXECUTE | SQLCOM_EXECUTE |
| 11 | LOGIN | Database login is not subject to audit rules. |
| 12 | LOGOUT | Database logout is not subject to audit rules. |
| 13 | CHANGEUSER | User change is not subject to audit rules. |

