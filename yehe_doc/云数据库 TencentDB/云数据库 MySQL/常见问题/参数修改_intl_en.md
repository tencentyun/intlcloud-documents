
### How do I modify the configuration parameters of a TencentDB for MySQL instance?
- **In the TencentDB for MySQL Console**
In the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and enter the management page. Select **Database Management** > **Parameter Settings**. Common `var\_name` includes:
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
</td><td> Non-interactive connection timeout period
</td></tr></tbody></table>

- **In the phpMyAdmin Console**
Log in to the TencentDB for MySQL instance through phpMyAdmin and click **Variables** on the top menu. Click **Edit** next to the variable to be modified. Modify and click **Save**.
![](https://main.qcloudimg.com/raw/214fec618ff4e166c6e4d747be3fea0b.png)

To view more configuration parameters, click the instance name and go to **Database Management** > **Parameter Settings** in the TencentDB for MySQL Console.

### How do I set Chinese queries in TencentDB for MySQL?
Chinese characters are currently not supported in TencentDB for MySQL.

### How do I enable the scheduler feature in TencentDB for MySQL?
In the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and enter the management page. Select **Database Management** > **Parameter Settings** and set the `event_scheduler` parameter to "ON".

### How do I increase the connection timeout period in TencentDB for MySQL?
In the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and enter the management page. Select **Database Management** > **Parameter Settings** and modify the `wait_timeout` parameter.

### How do I modify the `group_concat_max_len` parameter in TencentDB for MySQL?
In the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb), click the instance name and enter the management page. Select **Database Management** > **Parameter Settings** and modify the `group_concat_max_len` parameter.

### How do I locate the SQL statements for full-table scan in TencentDB for MySQL?
Full-table scan statements are not recorded by default. To locate them, set the `log_queries_not_using_indexes` parameter to "ON" in **Parameter Settings** in the TencentDB for MySQL Console. We recommend that you only enable this parameter for a short period of time.

### How do I change the default character set in TencentDB?
TencentDB for MySQL supports LATIN1, GBK, UTF8 (default), and UTF8MB4 character sets.

Although TencentDB supports changing the default character set, we recommend that you explicitly specify the table encoding when creating a table and specify the connection encoding when establishing a connection for more portable application experience. For more information on MySQL default character set and how to modify it, please see <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">Use Limits</a>. You can also modify the character set in the [MySQL Console](https://console.cloud.tencent.com/cdb).
