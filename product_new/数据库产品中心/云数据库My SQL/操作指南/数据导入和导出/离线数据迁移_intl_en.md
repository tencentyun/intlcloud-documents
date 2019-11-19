## Migrating Data in the Console
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and download backup files and logs. For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/7274" target="_blank">Downloading a Backup File<a/>.
2. A database can be restored with the MySQL command line tool by running the following command:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Here, "hostname" is the target server for data restoration, "port" is the port of target server, "username" is the username of the database on the target server, and "bak_pathname" is the full path to the backup file.  
3. Log in to the MySQL database and restore the tables by running the `shell > source bak_pathname` command.
   Here, "bak_pathname" is the full path to the backup file.

<span id="AA"></span>
## Migrating Data with the Command Line Tool

1. Generate the SQL file to be imported with the MySQL command line tool "mysqldump" in the following way:
> !The data files exported using mysqldump must be compatible with the SQL specification of your purchased TencentDB for MySQL version. You can log in to the database and get the MySQL version information by running the `select version();` command. The name of the generated SQL file can contain letters, digits, and underscores but not "test".</blockquote>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
Here, "options" is the export option, "db_name" is the database name, "tbl_name" is the table name, and "bak_pathname" is the export path.
For more information on how to export data with mysqldump, see [MySQL's official documentation](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).

2. A database can be restored with the MySQL command line tool by running the following command:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Here, "hostname" is the target server for data restoration, "port" is the port of target server, "username" is the username of the database on the target server, and "bak_pathname" is the full path to the backup file.

### Migrating Data on Windows
1. Export the data using the mysqldump tool on Windows.
>Make sure that the same database version, mysqldump tool version, and database character set are used. You can specify the character set using the parameter ```--default-character-set```.
2. Enter the command prompt and restore the data with the MySQL command line tool.
![](https://main.qcloudimg.com/raw/0d9caa9bbccfa840a88222fe31af980e.png)
3. Log in to the MySQL database and you can see the backed up database has already been restored to the server.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### Migrating Data on a Linux CVM Instance
For more information on how to access a database on a CVM instance, see <a href="https://intl.cloud.tencent.com/document/product/236/3130" target="_blank">Accessing a MySQL Database</a>.

1. Take the db_blog database in TencentDB for example. Log in to the CVM instance and generate the SQL file to be imported with the MySQL command line tool "mysqldump".
![](https://main.qcloudimg.com/raw/8ad9eae7ce6d428fc6887a83c37f9bfc.png)
2. Restore the data with the MySQL command line tool. In this example, data is restored to the CVM instance. You can see that the backed up database has been imported to the database corresponding to the target CVM instance.
![](https://main.qcloudimg.com/raw/8f06ab4159acb61fe7143a959647f02e.png)

## Issues with Character Set of Imported Data Files
1. If no character set is specified for during data file import to the TencentDB instance, the one set by the database will be used.
2. Otherwise, the specified character set will be used.
3. If the specified character set is different from that of the TencentDB instance, garbled text will be displayed.

For more information, see the character set description in <a href="https://intl.cloud.tencent.com/document/product/236/7259#.E5.AD.97.E7.AC.A6.E9.9B.86.E8.AF.B4.E6.98.8E" target="_blank">Use Limits</a>.

