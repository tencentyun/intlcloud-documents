### How do I modify the configuration parameters of a TencentDB for MySQL instance?
In the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID in the instance list and enter the management page. Select **Database Management** > **Parameter Settings**. Common `var\_name` includes:
<table>
<tbody><tr>
<th>Variable</th><th>Description</th></tr>
<tr>
<td>character_set_server</td><td>Default character set of the server</td></tr>
<tr>
<td>connect_timeout</td><td>Connection timeout period</td></tr>
<tr>
<td>long_query_time</td><td>A query that takes longer than this time is a slow query.</td></tr>
<tr>
<td>max_allowed_packet</td><td>Maximum packet length</td></tr>
<tr>
<td>max_connections</td><td>Maximum number of connections</td></tr>
<tr>
<td>sql_mode</td><td>Current SQL mode of the server</td></tr>
<tr>
<td>table_open_cache</td><td>Number of tables opened by all threads. Increasing this value will increase the number of file descriptors that mysqld is requested to open.</td></tr>
<tr>
<td>wait_timeout</td><td>Non-interactive connection timeout period</td></tr>
</tbody></table>

You can view more configuration parameters in **Database Management** > **Parameter Settings** in the console.

### How do I set Chinese queries in TencentDB for MySQL?
Chinese characters are currently not supported in TencentDB for MySQL.

### How do I enable the scheduler feature in TencentDB for MySQL?
In the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID in the instance list and enter the management page. Select **Database Management** > **Parameter Settings** and set the `event_scheduler` parameter to `ON`.

### How do I increase the connection timeout period in TencentDB for MySQL?
In the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID in the instance list and enter the management page. Select **Database Management** > **Parameter Settings** and modify the `wait_timeout` parameter.

### How do I modify the `group_concat_max_len` parameter in TencentDB for MySQL?
In the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click the instance ID in the instance list and enter the management page. Select **Database Management** > **Parameter Settings** and modify the `group_concat_max_len` parameter.

### How do I locate the SQL statements for full-table scan in TencentDB for MySQL?
Full-table scan statements are not recorded by default. To locate them, set the `log_queries_not_using_indexes` parameter to `ON` in **Parameter Settings** in the TencentDB for MySQL console. We recommend that you only enable this parameter for a short period of time.

### How do I change the default character set in TencentDB?
TencentDB for MySQL supports LATIN1, GBK, UTF8 (default), and UTF8MB4 character sets.

Although TencentDB supports changing the default character set, we recommend that you explicitly specify the table encoding when creating a table and specify the connection encoding when establishing a connection for more portable application experience. For more information on MySQL default character set and how to modify it, see <a href="https://www.tencentcloud.com/document/product/236/7259" target="_blank">Use Limits</a>. You can also modify the character set in the [MySQL Console](https://console.cloud.tencent.com/cdb).

### How do I view the character set collation in TencentDB?
TencentDB for MySQL allows you to set the character set collation when creating an instance. You can select a character set to provide a case-sensitive, accent-sensitive, or binary collation for your data, but doing so will affect the results of relevant database operations.
You can run the `show collation` command to view the collation.
**Sample:**
```
show collation where charset ='utf8mb4';
```
**Collation description**

| Collation Option | Description | 
|---------|---------|
| _CS | Case-sensitive. | 
| _CI | Case-insensitive. | 
| _AS | Accent-sensitive. This option indicates that the sorting will be accent-sensitive; for example, "a" and "ấ" are different characters. | 
| _AI | Accent-insensitive. | 
| _BIN | Binary. | 

**Character set suffix description**

| Instance Character Set Suffix | Description | 
|---------|---------|
|_CI_AI| Case-insensitive and accent-insensitive |
|_CI_AS| Case-insensitive and accent-sensitive |
|_CS_AI| Case-sensitive and accent-insensitive |
|_CS_AS| Case-sensitive and accent-sensitive |

### What should I do if the `lower_case_table_names` parameter failed to be modified?
You can modify the `lower_case_table_names` parameter in the TencentDB for MySQL console. If it is set to `1`, the case-insensitive mode is enabled. Pay attention to the following when modifying the parameter:
- Modifying the parameter will restart the instance.
- Before modifying the parameter, make sure that all database and table names in the instance are lowercase; otherwise, an error will be reported if any of them is uppercase.
- The parameter cannot be modified in MySQL 8.0 as it supports the case-sensitive mode by default.

Check uppercase table names:
```
select table_schema,table_name from information_schema.tables where   table_schema not in("mysql","information_schema") and (md5(table_name)<>md5(lower(table_name)) or md5(table_schema)<>md5(lower(table_schema)));
```
Check uppercase database names:
```
select SCHEMA_NAME from information_schema.SCHEMATA where md5(SCHEMA_NAME)<>md5(lower(SCHEMA_NAME));
```
