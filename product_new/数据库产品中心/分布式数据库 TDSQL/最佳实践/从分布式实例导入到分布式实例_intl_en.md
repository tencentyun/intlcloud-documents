As the solution for data importing from one distributed database to another is special, mysqldump is used as an example below to summarize the importing steps:

## 1. Install mysqldump (for MariaDB)
Purchase a Linux-based CVM instance and run `yum install mariadb-server` to install mysqldump.

## 2. Export data
Export data using mysqldump:
Set the `net_write_timeout` parameter in the parameter settings in the [TDSQL Console](https://console.cloud.tencent.com/dcdb): set global net_write_timeout=28800
```
mysqldump --compact --single-transaction --no-create-info -cdb_name table_name -uxxx -hxxx.xxx.xxx.xxx -Pxxxx -pxxx
```
>The db and table name parameters should be selected based on the actual situation. If the exported data is to be imported into another set of TDSQL environment, the `-c` option must be added.

## 3. Create a db in the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx -e "create database dbname;";
```
>
>- --default-character-set=utf8: Set based on your target table.
>- -uxxx: A privileged account (`-u` is a keyword).
>- -pxxx: Password (`-p` is a keyword).
>- -hxxx.xxx.xxx.xxx -Pxxxx: IP and port of the database instance.
>- dbname: Name of the db.

## 4. Import the table structure to the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < schema.sql
```
>
>- --default-character-set=utf8: Set based on your target table.
>- -uxxx: A privileged account (`-u` is a keyword).
>- -pxxx: Password (`-p` is a keyword).
>- -hxxx.xxx.xxx.xxx -Pxxxx: IP and port of the database instance.
>- dbname: Name of the db.

## 5. Import table data to the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < data.sql
```
>If an auto-increment field is used in the source table, and the "Column 'xx' specified twice" error occurs during import, the schema.sql needs to be processed.
>Remove the back quotes from the auto-increment field (cat schema.sql | tr "\`" " " > schema_tr.sql), drop database, and repeat steps 3-5 using the processed schema_tr.sql.
