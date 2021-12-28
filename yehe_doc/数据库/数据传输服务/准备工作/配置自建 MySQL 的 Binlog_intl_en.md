## Overview
If the source database in a data migration, sync, or subscription task is a self-built MySQL, TDSQL for MySQL, or TDSQL-C for MySQL database, you need to set the binlog in the self-built database to meet the requirements for the source database during verification.

## Operation Impact
This operation requires database restart, which affects the business. We recommend you perform it during off-peak hours. 

## Directions
1. Log in to the source database.
2. Modify the `my.cnf` configuration file as follows: 
> ?The default path of the `my.cnf` configuration file is `/etc/my.cnf`, subject to the actual conditions. 
> 
```
log_bin = MYSQL_BIN
binlog_format = ROW
server_id = 2 // We recommend you set it to an integer above 1. The value here is only an example
binlog_row_image = FULL
```
3. Restart the MySQL process. 
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
> ?`[\$Mysql_Dir]` is the installation path of the source database. Replace it with the actual path. 

