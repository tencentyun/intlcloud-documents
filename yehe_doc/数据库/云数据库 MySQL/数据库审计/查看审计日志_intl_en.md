This document describes how to view database audit logs and their list field.

>?
>- A new version of the audit log page was released on July 12, 2023. The new version added a new audit log search field "Scanned Rows". For existing audit logs before this release date, the data in this field will be displayed as "-", and the corresponding downloaded files and APIs will be displayed as "-1".
>- The units of the audit log fields "Execution Time" and "CPU Time" in the console and downloaded audit log files are all adjusted to microseconds.
>- When searching audit logs, the character used to separate multiple search items is changed from **comma** to **line break**.

## Prerequisite
You have enabled the audit service. For more information, see [Enabling Audit Service](https://www.tencentcloud.com/document/product/236/52086).
## Viewing Audit Log
>?The audit log display time is down to milliseconds, facilitating more precise sorting and problem analysis of SQL commands.
>

1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/dls/mysql).
2. On the left sidebar, click **Database Audit**.
3. Select **Region** at the top, click the **Audit Instance** tab, and click **Enabled** to filter audit-enabled instances.
4. Find the target instance in the **Audit Instance** list, or search for it by resource attribute in the search box, and click **View Audit Log** in the **Operation** column to enter the **Audit Log** tab and view logs.

### Tool list
- In **the audit instance search box**, you switch to other audit-enabled instances.
- In the **time box**, select a time period to view audit results in the selected time period.
   >?You can select any time period with data for search. Up to the first 60,000 eligible records can be displayed.
   > 
- In the **search box**, you can view the audit results by selecting search items, such as SQL details, client IP, user account, database name, SQL type, error code, execution time (μs), lock wait time (μs), IO wait time (μs), transaction duration (μs), CPU time (μs), thread ID, scanned rows, affected rows, and returned rows. Multiple search items are separated by line breaks.
<table><thead><tr><th>Item</th><th>Operator</th><th>Descsription</th></tr></thead><tbody>
<tr>
<td>SQL Details</td>
<td>Include<br>Exclude</td>
<td><li>Enter SQL command details with multiple keywords separated by line break. </li><li>SQL command details search is case-insensitive. </li><li>When the operator is "Include/Exclude", only fuzzy search by segment is supported while fuzzy search by wildcard is not. <br>For example, if the SQL command details are "SELECT * FROM test_db LIMIT 1", you can search by segment keywords such as "SELECT", "select * from", "*", "SELECT * FROM test_db LIMIT 1;", "from Test_DB". However, you can't search by wildcard keywords such as "SEL", "sel", and "test".</li></td>
</tr>
<tr>
<td>Client IP</td>
<td>Include<br>Exclude<br> Equal to<br>Not equal to</td>
<td>You can filter client IP addresses by using the wildcard "*" and separate them by line break. For example, if you enter "client IP: 9.223.23.2*", IP addresses that start with "9.223.23.2" will be searched.</td>
</tr>
<tr>
<td>User Account</td>
<td>Include<br>Exclude<br>Equal to<br>Not equal to</td>
<td>Enter a user account and separate multiple keywords by line break.</td>
</tr>
<tr>
<td>Database Name</td>
<td>Include<br>Exclude<br>Equal to<br>Not equal to</td>
<td>Enter a database name and separate multiple keywords by line break.</td>
</tr>
<tr>
<td>SQL Type</td>
<td>Equal to<br>Not equal to</td>
<td>Pull down the list to select a SQL type (ALTER, CHANGEUSER, CREATE, DELETE, DROP, EXECUTE, INSERT, LOGOUT, OTHER, REPLACE, SELECT, SET, UPDATE). You can select multiple types.</td>
</tr>
<tr>
<td>Error Code</td>
<td>Equal to<br>Not equal to</td>
<td>Enter an error code and separate multiple keywords by line break.</td>
</tr>
<tr>
<td>Execution Time (μs)</td>
<td>Range format</td>
<td>Enter an execution time in the format of M-N, such as 10-100 or 20-200.</td>
</tr>
<tr>
<td >Lock Wait time (μs)</td>
<td>Range format</td>
<td>Enter a lock wait time in the format of M-N, such as 10-100 or 20-200.</td>
</tr>
<tr>
<td>I/O Wait Time(μs)</td>
<td>Range format</td>
<td>Enter an IO wait time in the format of M-N, such as 0-100 or 20-200.</td>
</tr>
<tr>
<td>Transaction Duration (μs)</td>
<td>Range format</td>
<td>Enter a transaction duration in the format of M-N, such as 0-100 or 20-200.</td>
</tr>
<tr>
<td>CPU Time (μs)</td>
<td>Range format</td>
<td>Enter a CPU time in the format of M-N, such as 0-100 or 20-200.</td>
</tr>
<tr>
<td >Thread ID</td>
<td>Equal to<br>Not equal to</td>
<td>Enter a thread ID and separate multiple keywords by line break.</td>
</tr>
<tr>
<td>Scanned Rows</td>
<td>Range format</td>
<td>Enter a range of scanned rows in the format of M-N, such as 10-100 or 20-200.</td>
</tr>
<tr>
<td>Affected Rows</td>
<td>Range format</td>
<td>Enter a range of affected rows in the format of M-N, such as 10-100 or 20-200.</td>
</tr>
<tr>
<td>Returned Rows</td>
<td>Range format</td>
<td>Enter a range of returned rows returned in the format of M-N, such as 10-100 or 20-200.</td>
</tr>
</tbody></table>

### Log list
- In the **SQL Type** drop-down list, you can select multiple SQL types for filtering.
- The **Returned Rows** field represents the specific number of rows returned by executing the SQL command, which is mainly used to determine the impact of `SELECT` commands.

## Audit Fields
The following fields are supported in TencentDB for MySQL audit logs. On the **Audit Log** tab, click the download icon on the top-right corner. After download, click the file list icon. On the page redirected to, copy the download address and access it to get the complete SQL audit logs.

>!
>- Currently, you can download audit log files of a database instance only at the Tencent Cloud private network address by using a CVM instance in the same region.
>- Log files are valid for 24 hours. Download them promptly.
>- Up to 30 log files can be retained for one database instance. Delete files promptly after download.
>- The status of a very large log may fail to display. Shorten the log time range, split the large log to multiple logs, and download them.

<table><thead>
<tr><th>No.</th>
<th>Field Name</th>
<th>Remarks</th></tr></thead><tbody>
<tr>
<td rowspan="1" colSpan="1" >1</td>
<td rowspan="1" colSpan="1" >Time</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >2</td>
<td rowspan="1" colSpan="1" >Client IP</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >3</td>
<td rowspan="1" colSpan="1" >Database Name</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4</td>
<td rowspan="1" colSpan="1" >User Account</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >5</td>
<td rowspan="1" colSpan="1" >SQL Type</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >6</td>
<td rowspan="1" colSpan="1" >SQL Details</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >7</td>
<td rowspan="1" colSpan="1" >Error Code</td>
<td rowspan="1" colSpan="1" >`0` means success.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8</td>
<td rowspan="1" colSpan="1" >Thread ID</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >9</td>
<td rowspan="1" colSpan="1" >Scanned Rows</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >10</td>
<td rowspan="1" colSpan="1" >Returned Rows</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >11</td>
<td rowspan="1" colSpan="1" >Affected Rows</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12</td>
<td rowspan="1" colSpan="1" >Transaction Duration (μs)</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >13</td>
<td rowspan="1" colSpan="1" >CPU Time (μs)</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >14</td>
<td rowspan="1" colSpan="1" >Lock Wait Time (μs)</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >15</td>
<td rowspan="1" colSpan="1" >IO Wait Time (μs)</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >16</td>
<td rowspan="1" colSpan="1" >Transaction Duration (μs)</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</tbody></table>

## Relationship Between SQL Statement Type and SQL Statement Mapping Object
<table><thead>
<tr>
<th rowspan="1" colSpan="1" >No.</th>
<th rowspan="1" colSpan="1" >SQL Statement Type</th>
<th rowspan="1" colSpan="1" >SQL Statement Mapping Object</th>
</tr></thead><tbody>
<tr>
<td rowspan="1" colSpan="1" >1</td>
<td rowspan="1" colSpan="1" >OTHER</td>
<td rowspan="1" colSpan="1" >All other SQL statement types except the following</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >2</td>
<td rowspan="1" colSpan="1" >SELECT</td>
<td rowspan="1" colSpan="1" >SQLCOM_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >3</td>
<td rowspan="1" colSpan="1" >INSERT</td>
<td rowspan="1" colSpan="1" >SQLCOM_INSERT，SQLCOM_INSERT_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4</td>
<td rowspan="1" colSpan="1" >UPDATE</td>
<td rowspan="1" colSpan="1" >SQLCOM_UPDATE，SQLCOM_UPDATE_MULTI</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >5</td>
<td rowspan="1" colSpan="1" >DELETE</td>
<td rowspan="1" colSpan="1" >SQLCOM_DELETE，SQLCOM_DELETE_MULTI，SQLCOM_TRUNCATE</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >6</td>
<td rowspan="1" colSpan="1" >CREATE</td>
<td rowspan="1" colSpan="1" >SQLCOM_CREATE_TABLE，SQLCOM_CREATE_INDEX，SQLCOM_CREATE_DB，SQLCOM_CREATE_FUNCTION，SQLCOM_CREATE_USER，SQLCOM_CREATE_PROCEDURE，SQLCOM_CREATE_SPFUNCTION，SQLCOM_CREATE_VIEW，SQLCOM_CREATE_TRIGGER，SQLCOM_CREATE_SERVER，SQLCOM_CREATE_EVENT，SQLCOM_CREATE_ROLE，SQLCOM_CREATE_RESOURCE_GROUP，SQLCOM_CREATE_SRS</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >7</td>
<td rowspan="1" colSpan="1" >DROP</td>
<td rowspan="1" colSpan="1" >SQLCOM_DROP_TABLE，SQLCOM_DROP_INDEX，SQLCOM_DROP_DB，SQLCOM_DROP_FUNCTION，SQLCOM_DROP_USER，SQLCOM_DROP_PROCEDURE，SQLCOM_DROP_VIEW，SQLCOM_DROP_TRIGGER，SQLCOM_DROP_SERVER，SQLCOM_DROP_EVENT，SQLCOM_DROP_ROLE，SQLCOM_DROP_RESOURCE_GROUP，SQLCOM_DROP_SRS</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8</td>
<td rowspan="1" colSpan="1" >ALTER</td>
<td rowspan="1" colSpan="1" >SQLCOM_ALTER_TABLE，SQLCOM_ALTER_DB，SQLCOM_ALTER_PROCEDURE，SQLCOM_ALTER_FUNCTION，SQLCOM_ALTER_TABLESPACE，SQLCOM_ALTER_SERVER，SQLCOM_ALTER_EVENT，SQLCOM_ALTER_USER，SQLCOM_ALTER_INSTANCE，SQLCOM_ALTER_USER_DEFAULT_ROLE，SQLCOM_ALTER_RESOURCE_GROUP</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >9</td>
<td rowspan="1" colSpan="1" >REPLACE</td>
<td rowspan="1" colSpan="1" >SQLCOM_REPLACE，SQLCOM_REPLACE_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >10</td>
<td rowspan="1" colSpan="1" >SET</td>
<td rowspan="1" colSpan="1" >SQLCOM_SET_OPTION，SQLCOM_RESET，SQLCOM_SET_PASSWORD，SQLCOM_SET_ROLE，SQLCOM_SET_RESOURCE_GROUP</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >11</td>
<td rowspan="1" colSpan="1" >EXECUTE</td>
<td rowspan="1" colSpan="1" >SQLCOM_EXECUTE</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12</td>
<td rowspan="1" colSpan="1" >LOGIN</td>
<td rowspan="1" colSpan="1" >Database login is not subject to audit rules.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >13</td>
<td rowspan="1" colSpan="1" >LOGOUT</td>
<td rowspan="1" colSpan="1" >Database logout is not subject to audit rules.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >14</td>
<td rowspan="1" colSpan="1" >CHANGEUSER</td>
<td rowspan="1" colSpan="1" >User change is not subject to audit rules.</td>
</tr>
</tbody></table>


