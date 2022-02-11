This document describes common SQL commands.

For more information on SQL commands, including command parameters and restrictions, see [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/?spm=a2c4g.11186623.0.0.1987457aTFGg7y).

## Querying Version
Method 1:
```
MySQL [(none)]> SELECT CYNOS_VERSION();
+------------------------+
| CYNOS_VERSION() |
+------------------------+
| 5.7.mysql_cynos.1.3.10 |
+------------------------+
1 row in set (0.00 sec)
```
Method 2:
```
MySQL [(none)]> SELECT @@CYNOS_VERSION;
+------------------------+
| @@CYNOS_VERSION |
+------------------------+
| 5.7.mysql_cynos.1.3.10 |
+------------------------+
1 row in set (0.00 sec)
```
Method 3:
```
MySQL [(none)]> SHOW VARIABLES LIKE 'CYNOS_VERSION'; 
+---------------+------------------------+
| Variable_name | Value |
+---------------+------------------------+
| cynos_version | 5.7.mysql_cynos.1.3.10 |
+---------------+------------------------+
1 row in set (0.01 sec)
```

## Database Commands

| Command | Example | 
|---------|---------|
| Creates database and specifies character set | `create database db01 DEFAULT CHARACTER SET gbk COLLATE gbk_chinese_ci;` |
| Drops database | `drop database db01;` |

## Account Commands

| Command | Example | 
|---------|---------|
| Creates account | `CREATE USER 'username'@'host' IDENTIFIED BY 'password';` | 
| Drops account | `DROP USER 'username'@'host';` | 
| Grants permission | `GRANT SELECT ON db01.* TO 'username'@'host';` | 
| Queries accounts in database | `SELECT user,host,password FROM mysql.user_view;`<br>or <br>`show grants for xxx` | 
| Revokes permission | Revokes all permissions: `REVOKE ALL PRIVILEGES,GRANT OPTION FROM 'username'@'host';`<br>Revokes specified permission: `REVOKE UPDATE ON *.* FROM 'username'@'host';` | 



