### How to modify the configuration parameters of a TencentDB for MySQL instance?
- **In the TencentDB for MySQL Console**
In the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name to enter the management page, and select **Database Management** > **Parameter Settings**. Common var\_names include:
<table class="t">
<tbody><tr>
<th>  Variable
</th><th>  Description
</th></tr>
<tr>
<td> character_set_server
</td><td> Default character set of the server
</td></tr>
<tr>
<td> connect_timeout
</td><td> Connection timeout period
</td></tr>
<tr>
<td> long_query_time
</td><td> A query that takes longer than this time is a slow query
</td></tr>
<tr>
<td> max_allowed_packet
</td><td> Maximum packet length
</td></tr>
<tr>
<td> max_connections
</td><td> Maximum number of connections
</td></tr>
<tr>
<td> sql_mode
</td><td> Current SQL mode of the server
</td></tr>
<tr>
<td> table_open_cache
</td><td> Number of tables opened by all threads. Increasing this value will increase the number of file descriptors that mysqld is requested to open
</td></tr>
<tr>
<td> wait_timeout
</td><td> Non-interactive connection timeout period.
</td></tr></tbody></table>

- **In the phpMyAdmin Console**
Log in to the TencentDB for MySQL instance through phpMyAdmin and click **Variables** on the top menu. Click **Edit** next to the variable to be modified in the variable list, modify it, and click **Save**.
![](https://main.qcloudimg.com/raw/214fec618ff4e166c6e4d747be3fea0b.png)

You can view more configuration parameters in **Database Management** > **Parameter Settings** in the console.

### How to set Chinese queries in TencentDB for MySQL?
No Chinese characters are supported in TencentDB for MySQL for the time being.

### How to enable the scheduler function in TencentDB for MySQL?
In the TencentDB for MySQL Console, click the instance name to enter the management page, select **Database Management** > **Parameter Settings**, and set the event_scheduler parameter to "ON".

### How to increase the connection timeout period in TencentDB for MySQL?
In the TencentDB for MySQL Console, click the instance name to enter the management page, select **Database Management** > **Parameter Settings**, and modify the wait_timeout parameter.

### How to modify the group_concat_max_len parameter in TencentDB for MySQL?
In the TencentDB for MySQL Console, click the instance name to enter the management page, select **Database Management** > **Parameter Settings**, and modify the group_concat_max_len parameter.

### How to locate the SQL statement for full table scan in TencentDB for MySQL?
The statement for full table scan is not recorded by default. To do so, set the log_queries_not_using_indexes parameter to "ON" on the **Parameter Settings** page in the TencentDB for MySQL Console. Note: Do not keep it on for too long.

#### How to change the default character set in TencentDB?
The default character set in TencentDB for MySQL is the same as that in MySQL: latin1 (i.e., ISO-8859-1). You can change the server-side character set of a database. Currently, four character sets are supported: latin1, gbk, utf8, and utf8mb4.
Even though TencentDB supports changing the default character set, you are recommended to explicitly specify the table encoding format when creating it and specify the connection encoding during connection establishment. In this way, your application will be more portable. For more information on the default MySQL character set and how to change it, see <a href="https://intl.cloud.tencent.com/document/product/236/7259#6-.E5.AD.97.E7.AC.A6.E9.9B.86.E8.AF.B4.E6.98.8E6" target="_blank">Use Limits</a>. You can change the character set in the TencentDB Console.
