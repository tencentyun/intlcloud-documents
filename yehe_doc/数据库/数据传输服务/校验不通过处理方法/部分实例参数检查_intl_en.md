
## MySQL/TDSQL for MySQL/TDSQL-C/MariaDB/Percona Check Details
- `row_format` in the source database table cannot be `FIXED`.
- The `lower_case_table_names` variable in the source and target databases must be the same.
- The `max_allowed_packet` parameter of the target database must be set to 4 MB or above.
- The `connect_timeout` variable of the source database must be above 10.
- In migration from MySQL/TDSQL for MySQL/TDSQL-C to MySQL, if a time-consuming SQL statement is running on the source database, the warning "A time-consuming SQL statement is running on the source database, which may cause table locks. Please try again later or process the SQL statement on the source database" will be reported. 

## Fix
### Modifying `row_format` parameter in source database
If the value of `row_format` in the database table is `FIXED`, data overflow will occur if the storage length of each row in the table exceeds the limit, and an error will be reported. Therefore, you need to modify it to another format such as `DYNAMIC` to make the storage length of each row vary by content length. 

If a similar error occurs, fix it as follows:
1. Log in to the source database.
2. Set `row_format` to `DYNAMIC`.  
```
alter table table_name row_format = DYNAMIC
```
3. Check whether the configuration takes effect.
```
show table status like '%row_format%';
```
The system should display a result similar to the following:

```
mysql> show table status like '%row_format%';
+---------------+----------+
| Variable_name | Value    |
+---------------+----------+
| row_format    | DYNAMIC  |
+---------------+----------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

### Making `lower_case_table_names` have the same value in source and target databases
`lower_case_table_names` sets the letter case sensitivity in MySQL. It has the following valid values:
Windows and macOS environments are case-insensitive, but Linux environments are case-sensitive. To ensure the compatibility between different operating systems, you need to use the same letter case sensitivity rule.

- 0: the name of a stored table is in the specified letter case and is case-sensitive during comparison.
- 1: the name of a stored table is in lowercase on the disk and is case-insensitive during comparison.
- 2: the name of a stored table is in the specified letter case and is in lowercase during comparison.

If a similar error occurs, set the parameter in the source and target databases to the same value as follows:
1. Log in to the source database.
2. Check the values of `lower_case_table_names` in the source and target databases.
```
show variables like '%lower_case_table_names%';
```
3. Modify the `lower_case_table_names` parameter.
```
alter global lower_case_table_names = 1
```
4. Run the following command to restart the databases:
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
5. Check whether the configuration takes effect.
```
show variables like '%lower_case_table_names%';
```
The system should display a result similar to the following:

```
mysql> show variables like '%lower_case_table_names%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| lower_case_table_names | 1     |
+------------------------+-------+
1 row in set (0.00 sec)
```
6. Run the verification task again.

### Modifying `max_allowed_packet` parameter in target database 
`max_allowed_packet` is the maximum size of a packet that can be transferred. If its value is too large, more memory will be used, causing packet losses and inability to capture the SQL statements of large exception event packets. If its value is too small, program errors mat occur, causing backup failure and frequent sending/receiving of network packets, which compromises the system performance.

If a similar error occurs, fix it as follows:
1. Log in to the target database.
2. Modify the `max_allowed_packet` parameter. 
```
set global max_allowed_packet = 4M
```
3. Check whether the configuration takes effect.
```
show global variables like '%max_allowed_packet%';
```
The system should display a result similar to the following:

```
mysql> show global variables like '%max_allowed_packet%';
+------------------------+---------+
| Variable_name          | Value   |
+------------------------+---------+
| max_allowed_packet     | 4194304 |
+------------------------+---------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

### Modifying `connect_timeout` variable in source database
`connect_timeout` is the database connection time. Connection requests after `connect_timeout` elapses will be rejected. If this value is too small, database connections will be closed frequently, affecting the processing efficiency. Therefore, we recommend you set a value above 10.

If a similar error occurs, fix it as follows:
1. Log in to the source database.
2. Modify the `connect_timeout` parameter.
```
set global connect_timeout = 10
```
3. Check whether the parameter is successfully modified.
```
show global variables like '%connect_timeout%';
```
The system should display a result similar to the following:

```
mysql> show global variables like '%connect_timeout%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| connect_timeout        | 10    |
+------------------------+-------+
1 row in set (0.00 sec)
```
4. Run the verification task again.

