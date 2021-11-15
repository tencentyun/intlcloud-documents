
## MySQL/TDSQL for MySQL/TDSQL-C Check Details
You need to configure the source database's binlog parameters in compliance with the following requirements. If the verification fails, fix it as instructed in this document.
- The `log_bin` variable must be set to `ON`.
- The `binlog_format` variable must be set to `ROW`.
- `binlog_row_image` must be set to `FULL`.
- If the source database is MySQL 5.6 or above, `gtid_mode` can be set to only `ON` or `OFF`. We recommend you set it to `ON`, because if it is set to `OFF`, an alarm will be triggered, and if it is set to `ON_PERMISSIVE` or `OFF_PERMISSIVE`, an error will be reported.
- The `server_id` parameter must be set manually and cannot be `0`.
- It is not allowed to set `do_db` and `ignore_db`.
- If the source database is a slave database, the `log_slave_updates` variable must be set to `ON`.

## Fix
### Enabling binlog 
`log_bin` controls the binlog switch. You need to enable binlog to log all database table structure and data changes. 

If a similar error occurs, fix it as follows:
1. Log in to the source database.
2. Modify the `my.cnf` configuration file of the source database as follows:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
log_bin = MYSQL_BIN
binlog_format = ROW
server_id = 2         // We recommend you set it to an integer above 1. The value here is only an example
binlog_row_image = FULL
```
3. Run the following command to restart the source database:
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?`[\$Mysql_Dir]` is the installation path of the source database. You need to replace it with the actual path.
4. Check whether the binlog feature has been enabled.
```
show variables like '%log_bin%';
```
The system should display a result similar to the following:
```
mysql> show variables like '%log_bin%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| log_bin       | ON    |
+---------------+-------+
1 row in set (0.00 sec)
```
5. Run the verification task again.

### Modifying `binlog_format` parameter
`binlog_format` specifies one of the following three binlog formats:
- `STATEMENT`: each SQL statement that modifies the data will be logged into the binlog of the master. When replicating data, the slave will run the same SQL statements as those in the master. This format can reduce the binlog size. However, the slave may not be able to properly replicate certain functions.
- `ROW`: the binlog will log the modifications of each data row, and the slave will modify the same data. This format guarantees the correct master-slave replication, but the binlog size will increase.
- `MIXED`: it is a combination of the above two formats. MySQL will automatically select `STATEMENT` or `ROW` format to log each executed SQL statement. 

Therefore, to ensure the correct master-slave replication, the `binlog_format` parameter should be set to `ROW`. If a similar error occurs, fix it as follows:
>?You can modify this parameter without restarting the database, but you need to close all business connections to the database. If the source database is a slave, you also need to restart the master/slave sync SQL thread to prevent current business connections from continuing writing data in the mode before modification.

1. Log in to the source database.
2. Modify the `my.cnf` configuration file as follows:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
binlog_format = ROW
```
3. Check whether the parameter modification takes effect:
```
show variables like "%binlog_format%";
```
The system should display a result similar to the following:
```
mysql> show variables like '%binlog_format%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| binlog_format | ROW   |
+---------------+-------+
1 row in set (0.00 sec)
```
5. Run the verification task again.

### Modifying `binlog_row_image` parameter
The `binlog_row_image` parameter determines how the binlog logs the pre-image (content before modification) and post-image (content after modification), which directly affects features such as data flashback and master-slave replication.
The `binlog_row_image` parameter takes effect only if `binlog_format` is set to `ROW`. The following describes the effects of specific values:
- `FULL`: in `ROW` format, binlog will log all column data information of the pre-image and post-image.
- `MINIMAL`: in `ROW` format, if a table has no primary key or unique key, the pre-image will log all columns, and the post-image will log the modified columns. If it has a primary key or unique key, both the pre-image and post-image will only log the affected columns.

Therefore, you need to set `binlog_row_image` to `FULL` to make the source database binlog log the full image. If an error occurs, fix it as follows:
>?You can modify this parameter without restarting the database, but you need to close all business connections to the database. If the source database is a slave, you also need to restart the master/slave sync SQL thread to prevent current business connections from continuing writing data in the mode before modification.

1. Log in to the source database.
2. Modify the `my.cnf` configuration file of the source database as follows:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
binlog_row_image = FULL
```
3. Check whether the parameter modification takes effect.
```
show variables like "%binlog_row_image%";
```
The system should display a result similar to the following:
```
mysql> show variables like '%binlog_row_image%';
+------------------+-------+
| Variable_name    | Value |
+------------------+-------+
| binlog_row_image | FULL  |
+------------------+-------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

### Modifying `gtid_mode` parameter
A global transaction identifier (GTID) uniquely identifies a transaction in the binlog. Using GTIDs can prevent disordered data or master-slave inconsistency due to repeated transaction executions.
GTID is a new feature on MySQL 5.6. Therefore, this problem may only occur on MySQL 5.6 or above. DTS only allows you to set `gtid_mode` to `ON` or `OFF`. We recommend you set it to `ON`; otherwise, an alarm will be triggered during verification.

The alarm does not affect the migration or sync task but affects the business: after GTID is set, during incremental data sync, if HA switch occurs in the source database, DTS will be switched and restarted, which is almost imperceptible to the task; if GTID is not set, the task will fail after disconnection and cannot be recovered.

Below are the valid values of `gtid_mode`. When modifying the value, you can only do so in the specified sequence step by step: for example, if you want to change `OFF` to `ON`, you should modify the `gtid_mode` value in the following sequence: `OFF` > `OFF_PERMISSIVE` > `ON_PERMISSIVE` > `ON`.
- `OFF`: all new transactions in the master database and all transactions in the slave database must be anonymous.
- `OFF_PERMISSIVE`: all new transactions in the master database must be anonymous. Transactions in the slave database can be anonymous or GTID transactions but cannot be only GTID transactions.
- `ON_PERMISSIVE`: all new transactions in the master database must be GTID transactions, and transactions in the slave database can be anonymous or GTID transactions.
- `ON`: all new transactions in the master database and all transactions in the slave database must be GTID transactions.

If a similar alarm is triggered, fix it as follows:
1. Log in to the source database.
2. Set `gtid_mode = OFF_PERMISSIVE` on both the master and slave databases.
```
set global gtid_mode = OFF_PERMISSIVE;
```
3. Set `gtid_mode = ON_PERMISSIVE` on both the master and slave databases.
```
set global gtid_mode = ON_PERMISSIVE;
```
4. Run the following command on each instance node to check whether consumption of anonymous transactions is completed. If the parameter value is `0`, the consumption is completed.
```
show variables like "%ONGOING_ANONYMOUS_TRANSACTION_COUNT%";
```
The system should display a result similar to the following:
```
mysql> show variables like '%ONGOING_ANONYMOUS_TRANSACTION_COUNT%';
+-------------------------------------+-------+
| Variable_name                       | Value |
+-------------------------------------+-------+
| Ongoing_anonymous_transaction_count | 0     |
+-------------------------------------+-------+
1 row in set (0.00 sec)
```
5. Set `gtid_mode = ON` on both the master and slave databases.
```
set global gtid_mode = ON;
```
6. Add the following content to the `my.cnf` file:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
gtid_mode = on
enforce_gtid_consistency = on
```
7. (Optional) Run the following command to restart the database. Databases on versions below MySQL 5.7.6 need to be restarted, while databases on 5.7.6 or above do not need to be restarted, but all business connections must be closed.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
8. Run the verification task again. 

### Modifying `server_id` parameter
The `server_id` parameter must be set manually and cannot be set to `0`. The system default value of this parameter is `1`, but the configuration isn't necessarily correct even if the queried parameter value is `1`. You still need to manually set it.
>?You can modify this parameter without restarting the database, but you need to close all business connections to the database. If the source database is a slave, you also need to restart the master/slave sync SQL thread to prevent current business connections from continuing writing data in the mode before modification.

1. Log in to the source database.
2. Modify the `my.cnf` configuration file of the source database as follows:
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
>
```
server_id = 2         // We recommend you set it to an integer above 1. The value here is only an example
```
3. Check whether the parameter modification takes effect.
```
show global variables like "%server_id%";
```
The system should display a result similar to the following:
```
mysql> show global variables like '%server_id%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| server_id     | 2     |
+---------------+-------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

### Deleting `do_db` and `ignore_db` settings
The binlog logs all executed DDL and DML statements in the database, while `do_db` and `ignore_db` are used to set the filter conditions for binlog.
- `binlog_do_db`: only the specified databases will be logged in the binlog (all databases will be logged by default).
- `binlog_ignore_db`: the specified databases will not be logged in the binlog.

After `do_db` and `ignore_db` are set, some cross-database operations will not be logged in the binlog, and master-slave replication will be exceptional; therefore, we recommend you not set them. If a similar error occurs, fix it as follows:
1. Log in to the source database.
2. Modify the `my.cnf` configuration file in the source database to delete `do_db` and `ignore_db` settings.
>?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions.
3. Run the following command to restart the source database:
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?`[\$Mysql_Dir]` is the installation path of the source database. You need to replace it with the actual path.
4. Check whether the parameter modification takes effect.
```
show master status;
```
The system should display a result similar to the following:
```
mysql> show master status;
+---------------+----------+--------------+------------------+-------------------+
| File          | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+---------------+----------+--------------+------------------+-------------------+
| binlog.000011 | 154      |              |                  |                   |
+---------------+----------+--------------+------------------+-------------------+
```
5. Run the verification task again.

### Modifying `log_slave_updates` parameter
In the master-slave reuse structure, if the `log-bin` parameter is enabled in the slave database, data operations directly performed in the slave database can be logged in the binlog, but data replications from the master database to the slave database cannot be logged. Therefore, if the slave database is to be used as the master database of another slave database, the `log_slave_updates` parameter needs to be enabled. 
1. Log in to the source database.
2. Set `log_slave_updates` to `1`.
```
set global log_slave_updates = 1;
```
3. Run the following command to restart the source database:
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?`[\$Mysql_Dir]` is the installation path of the source database. You need to replace it with the actual path.
4. Check whether the configuration takes effect.
```
show global variables like '%log_slave_updates%';
```
The system should display a result similar to the following:
```
mysql> show global variables like '%log_slave_updates%';
+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| log_slave_updates | 1     |
+-------------------+-------+
1 row in set (0.00 sec)
```
5. Run the verification task again.
