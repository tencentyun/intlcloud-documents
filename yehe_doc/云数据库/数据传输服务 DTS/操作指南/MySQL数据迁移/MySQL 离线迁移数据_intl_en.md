Data Migration Through Console

1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and download the desired backup file. For detailed directions, please see [Downloading Backup Files](https://intl.cloud.tencent.com/document/product/236/31910).
2. A database can be restored with the MySQL command line tool by running the following command:
```
shell > mysql -h hostname -P port -u username -p -d dbname < bak_pathname
```
Here, `hostname` is the target server for data restoration, `port` is the port of target server, `username` is the username of the database on the target server, `dbname` is the database name, and `bak_pathname` is the full path to the backup file.  
3. Log in to the MySQL database and restore the tables by running the `shell > source bak_pathname` command.
Here, `bak_pathname` is the full path to the backup file.

### Migrating database on Windows
 Use the database `db_blog` as an example:
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, find the instance from which you want to export data and click the instance name or **Manage** in the **Operation** column to enter the instance management page.
3. Select the **Backup and Restore** > **Backup List** tab, select the backup file to be downloaded, and click **Download** > **Partial Download**.

2. Select the database to be exported and click **Next**.

5. Click **Download** in **Local Download** to download the backup file to your local file system.
4. Record the full path.
The full path in this example is: F:\download\cdb147691_backup_20170717050142
5. Enter the command prompt and restore the data with the MySQL command line tool.
![][image-2]
6. Log in to the MySQL database and you can see the backed up database has already been restored to the server.
![][image-10]

### Migrating table on Windows
1. Taking the database table "t_blog" under "db_blog" as an example, download a backup file from the TencentDB Console.
2. Download the backup file from the TencentDB Console and record the full path.
The full path in this example is: F:\download\cdb147691_backup_20170718050146
3. Enter the command prompt and restore the data with the MySQL command line tool.
![][image-4]
4. Log in to the MySQL database and you can see the backed up table has already been restored to the server.
![][image-12]

## Data Migration Through Command Line Tool
1. Generate the SQL file to be imported with the MySQL command line tool "mysqldump" in the following way:
>**Note:**
>The data files exported through mysqldump must be compatible with the SQL specification of your purchased TencentDB for MySQL version. You can log in to the database and get the MySQL version information by running the `select version();` command. The name of the generated SQL file can contain letters, digits, and underscores but not "test".
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
Here, `options` is the export option, `db_name` is the database name, `tbl_name` is the table name, and `bak_pathname` is the export path.
For more information on how to export data with mysqldump, please see [mysqldump - A Database Backup Program](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).

2. A database can be restored with the MySQL command line tool by running the following command:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Here, `hostname` is the target server for data restoration, `port` is the port of target server, `username` is the username of the database on the target server, and `bak_pathname` is the full path to the backup file.

### Migrating data on Linux CVM instance
For more information on how to access a database on a CVM instance, please see "Accessing a MySQL Database".
1. Taking the `db_blog` database in TencentDB for example, log in to the CVM instance and generate the SQL file to be imported with the MySQL command line tool "mysqldump".
![][image-5]
2. Restore the data with the MySQL command line tool. In this example, data is restored to the CVM instance. You can see that the backed up database has been imported to the database corresponding to the target CVM instance.
![][image-6]

## Issues with Character Set of Imported Data Files
1. If no character set is specified during data file import into TencentDB, the one set by the database will be used.
2. Otherwise, the specified character set will be used.
3. If the specified character set is different from that of TencentDB, garbled text will be displayed.

For more information on character set encoding, please see "Notes on Character Set" in [Use Limits](https://intl.cloud.tencent.com/document/product/236/7259).

[image-1]:  https://mc.qcloudimg.com/static/img/ec1530d76dab094cfc76a49e05e34d3c/step11.png
[image-2]:  https://mc.qcloudimg.com/static/img/bb37805c3fa523664ea427923f79c747/step12.png
[image-3]:  https://mc.qcloudimg.com/static/img/42f282cf218253ba16ec51eb715ac76f/step13.png
[image-4]:  https://mc.qcloudimg.com/static/img/ec52232b7fab6e9d44b95ab1f774a0c1/step14.png
[image-5]:  https://main.qcloudimg.com/raw/13e670ec6b48b9abc1036789fcca850b.png
[image-6]:  https://main.qcloudimg.com/raw/770c5e4b5a7991542b3f6e70b812e379.png
[image-7]:  https://mc.qcloudimg.com/static/img/93e534bb662bd93cd1cc33f3e7e01fd8/step1.png
[image-8]:  https://mc.qcloudimg.com/static/img/85c72e3d044155342ec9375b42d7d597/step2.png
[image-9]:  https://mc.qcloudimg.com/static/img/fbd4f81256f71264d8616916673c3383/step3.png
[image-10]: https://mc.qcloudimg.com/static/img/3bae3de9bd92e262bcfc2d0ae73a85bf/step4.png
[image-11]: https://mc.qcloudimg.com/static/img/189a5828548563144959c91482b91694/step5.png
[image-12]: https://mc.qcloudimg.com/static/img/4f03808a5f93d2b2731431c12c1684ee/step6.png
