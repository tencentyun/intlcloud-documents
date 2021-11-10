The solution for data importing from one distributed database to another is special. mysqldump is used as an example below to summarize the importing steps:

## 1. Install mysqldump (for MariaDB)
Purchase a Linux CVM instance and run `yum install mariadb-server` to install mysqldump.

## 2. Export the table structure
```
mysqldump --compact --single-transaction -d -uxxx -pxxx  -hxxx.xxx.xxx.xxx -Pxxxx  db_name table_name   >  schema.sql
```
>?Please select the `db_name` and `table_name` parameters as needed.

## 3. Export data
Export data by using mysqldump:
Set the `net_write_timeout` parameter in the parameter settings in the [TDSQL for MySQL Console](https://console.cloud.tencent.com/dcdb): set global net_write_timeout=28800
```
mysqldump --compact --single-transaction --no-create-info -c -uxxx  -pxxx -hxxx.xxx.xxx.xxx -Pxxxx db_name table_name  > data.sql
```
>?The `db_name` and `table_name` parameters should be selected as needed. If the exported data is to be imported into another set of TDSQL for MySQL environment, the `-c` option must be added, and there should be a space between `-c` and `db_name`.
>
![](https://main.qcloudimg.com/raw/567f47f17939e809a7e0aa2f06627353.png)

## 4. Create a database in the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx -e "create database dbname;";
```
- --default-character-set=utf8: set based on your target table.
- -uxxx: a privileged account (`-u` is a keyword).
- -pxxx: password (`-p` is a keyword).
- -hxxx.xxx.xxx.xxx -Pxxxx: IP and port of the database instance.
- dbname: database name.

## 5. Import the table structure into the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < schema.sql
```
- --default-character-set=utf8: set based on your target table.
- -uxxx: a privileged account (`-u` is a keyword).
- -pxxx: password (`-p` is a keyword).
- -hxxx.xxx.xxx.xxx -Pxxxx: IP and port of the database instance.
- dbname: database name.

## 6. Import table data into the target instance
```
mysql --default-character-set=utf8 -uxxx -pxxx -hxxx.xxx.xxx.xxx -Pxxxx dbname < data.sql
```
>?If an auto-increment field is used in the source table, and the "Column 'xx' specified twice" error occurs during import, the `schema.sql` needs to be processed.
   Remove the back quotes from the auto-increment field (cat schema.sql | tr "`" " " > schema_tr.sql), drop database, and repeat steps 3–5 by using the processed `schema_tr.sql`.
	 
![](https://main.qcloudimg.com/raw/b55fe0763f4e8fd1795fec478e9dc0c1.png)
