This document describes how to create a database and manage database account permissions on the **Database Management** tab in the TDSQL-C for MySQL console.


## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click the ID of the target cluster in the cluster list or **Manage** in the **Operation** column to enter the cluster management page.
2. On the cluster management page, select the **Database Management** page and click **Create Database**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IkZn375_43.png)
3. In the pop-up window, configure the following parameters and click **OK**:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AD5i472_44.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Database Name</td>
<td>Enter the database name, which can contain up to 64 letters, digits, hyphens, and underscores and must start with a letter and end with a letter or digit.</td></tr>
<tr>
<td>Character Set</td>
<td>Set the character set supported by the database. For more information, see <a href="https://dev.mysql.com/doc/">MySQL documentation</a>.</td></tr>
<tr>
<td>Collation</td>
<td>Set the sorting rule of the database. For more information, see <a href="https://dev.mysql.com/doc/">MySQL documentation</a>.</td></tr>
<tr>
<td>Authorize User</td>
<td>Click <strong>Add</strong> and select the account to be authorized, permissions to be granted, and host information. You can also delete the authorization record. </td></tr>
<tr>
<td>Remarks</td>
<td>Enter remarks for the database, which can contain up to 256 characters.</td></tr>
</tbody></table>

## [Account authorization details](id:ZHQXSQMX)
You can grant an account the read-only, read-write, DML, DDL, and read-only & index permissions of the created database. The permissions and corresponding SQL statements are as follows:

| Permission | Authorization Details | Authorization SQL Statement |
|---------|---------|---------|
| Read-only | SELECT<br>LOCK TABLES<br>SHOW VIEW | ```GRANT SELECT, LOCK TABLES, SHOW VIEW ON `database`.* TO 'account'@'%'``` |
| Read-write | ALL PRIVILEGES | ```GRANT ALL PRIVILEGES ON `database`.* TO 'account'@'%'``` |
| DML | SELECT<br>INSERT<br>UPDATE<br>DELETE<br>CREATE TEMPORARY TABLES<br>LOCK TABLES<br>EXECUTE<br>SHOW VIEW<br>EVENT<br>TRIGGER | ```GRANT SELECT, INSERT, UPDATE, DELETE, CREATE TEMPORARY TABLES, LOCK TABLES, EXECUTE, SHOW VIEW, EVENT, TRIGGER ON `database`.* TO 'account'@'%'``` |
| DDL | CREATE<br>DROP<br>INDEX<br>ALTER<br>CREATE TEMPORARY TABLES<br>LOCK TABLES<br>CREATE VIEW<br>SHOW VIEW<br>CREATE ROUTINE<br>ALTER ROUTINE | ```GRANT CREATE, DROP, INDEX, ALTER, CREATE TEMPORARY TABLES, LOCK TABLES, CREATE VIEW, SHOW VIEW, CREATE ROUTINE, ALTER ROUTINE ON `database`.* TO 'account'@'%'``` |
| Read-only & index | SELECT<br>INDEX<br>LOCK TABLES<br>SHOW VIEW | ```GRANT SELECT, INDEX, LOCK TABLES, SHOW VIEW ON `database`.* TO 'account'@'%'``` |

