This document describes how to migrate data through the console and command line tool.

## Data Migration Through Console
There are two modes for migrating data through the console: physical backup and logical backup. For more information, see:
- [Restoring Database from Physical Backup](https://intl.cloud.tencent.com/document/product/236/31910)
- [Restoring Database from Logical Backup](https://intl.cloud.tencent.com/document/product/236/31909)

## [Data Migration with Command Line Tool](id:AA)
1. Generate the SQL file to be imported with the MySQL command line tool "mysqldump" in the following way:
>!
>- The data files exported using mysqldump must be compatible with the SQL specification of your purchased TencentDB for MySQL version. You can log in to the database and get the MySQL version information by running the `select version();` command. The name of the generated SQL file can contain letters, digits, and underscores but not "test".
>- Make sure that the same source and target database versions, character sets, and mysqldump tool versions are used. You can specify the character set with the `--default-character-set` parameter.
>
```
shell > mysqldump [options] db_name [tbl_name ...] > bak_pathname
```
Here, `options` is the export option, `db_name` is the database name, `tbl_name` is the table name, and `bak_pathname` is the export path.
For more information on how to export data with mysqldump, see [MySQL's official documentation](https://dev.mysql.com/doc/refman/5.6/en/mysqldump.html).
2. Import data to the target database with the MySQL command line tool as follows:
```
shell > mysql -h hostname -P port -u username -p < bak_pathname
```
Here, `hostname` is the target server for data restoration, `port` is the port of target server, `username` is the username of the database on the target server, and `bak_pathname` is the full path to the backup file.

### Migrating data (Windows)
1. Use the Windows version of mysqldump to generate the SQL file to be imported. For more information, see the description in [Data Migration with Command Line Tool](#AA).
2. Enter the command prompt and import the data into the target database with the MySQL command line tool.
![](https://main.qcloudimg.com/raw/82fece0fed5c61437215836a6a5fdc54.png)
3. [Log in to the target MySQL database](https://dev.mysql.com/doc/refman/5.7/en/connecting.html), run the `show databases;` command, and you can see that the backup database has been imported into the target database.
![](https://main.qcloudimg.com/raw/ac73c7b6cd2dd6682dffce3cb696a3dd.png)

### Migrating data (Linux)
This document uses a Linux CVM instance as an example. For more information on how to access a database from a CVM instance, see <a href="https://intl.cloud.tencent.com/document/product/236/37788" target="_blank">Accessing MySQL Database</a>.

1. [Log in to the CVM instance](https://intl.cloud.tencent.com/document/product/213/10517) and generate the SQL file to be imported with the MySQL command line tool "mysqldump". Take the `db_blog` database in TencentDB as an example:
![](https://qcloudimg.tencent-cloud.cn/raw/033ea149db540571f7bb50a172a27808.png)
2. Use the MySQL command line tool to restore the data to the target database.
3. Log in to the target MySQL database, run the `show databases;` command, and you can see that the backup database has been imported into the target database.
![](https://qcloudimg.tencent-cloud.cn/raw/4ea82604868dd99e092c2f828f5caae3.png)

## Issues with Character Set of Imported Data Files
1. If no character set is specified during data file import into TencentDB, the one set by the database will be used.
2. Otherwise, the specified character set will be used.
3. If the specified character set is different from that of TencentDB, garbled text will be displayed.

For more information, see the character set description in <a href="https://intl.cloud.tencent.com/document/product/236/7259" target="_blank">Use Limits</a>.

