By default, ClickHouse uses its own database engine, which provides configurable [table engines](https://intl.cloud.tencent.com/document/product/1129/44436) and all the supported [SQL syntax](https://intl.cloud.tencent.com/document/product/1129/44435). You can also use the MySQL engine.

## Lazy Engine
It stores a table in memory since the last `expiration_time_in_seconds` (for `\*Log` engine tables only). Due to the long interval to access this kind of table, it is optimized to store a large number of `\*Log` engine tables.

## MySQL Engine
The MySQL engine is used to map tables from remote MySQL servers to ClickHouse and allow INSERT and SELECT queries on tables to exchange data between ClickHouse and MySQL.

The MySQL engine converts queries to MySQL statements and sends them to the MySQL server, so that you can perform SHOW TABLES and SHOW CREATE TABLE operations. **You cannot perform RENAME, CREATE TABLE, and ALTER operations on them**.

### CREATE DATABASE 
```
 CREATE DATABASE [IF NOT EXISTS] db_name [ON CLUSTER cluster]ENGINE = MySQL('host:port', ['database' | database], 'user', 'password')
```
MySQL engine parameters are as described below:

| Parameter | Description |
|---------|-------|
| host:port |  Connected MySQL address  |
| database | Connected MySQL database |
| user |  Connected MySQL user  |
| password |  Connected MySQL user password  |

The types supported by MySQL and ClickHouse are as described below:

| **MySQL**                         | **ClickHouse**                                               |
| --------------------------------- | ------------------------------------------------------------ |
| UNSIGNED TINYINT                  | [UInt8](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| TINYINT                           | [Int8](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| UNSIGNED SMALLINT                 | [UInt16](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| SMALLINT                          | [Int16](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| UNSIGNED INT,  UNSIGNED MEDIUMINT | [UInt32](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| INT, MEDIUMINT                    | [Int32](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| UNSIGNED BIGINT                   | [UInt64](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| BIGINT                            | [Int64](https://clickhouse.tech/docs/zh/sql-reference/data-types/int-uint/) |
| FLOAT                             | [Float32](https://clickhouse.tech/docs/zh/sql-reference/data-types/float/) |
| DOUBLE                            | [Float64](https://clickhouse.tech/docs/zh/sql-reference/data-types/float/) |
| DATE                              | [Date](https://clickhouse.tech/docs/zh/sql-reference/data-types/date/) |
| DATETIME, TIMESTAMP               | [Datetime](https://clickhouse.tech/docs/zh/sql-reference/data-types/datetime/) |
| BINARY                            | [Fixedstring](https://clickhouse.tech/docs/zh/sql-reference/data-types/fixedstring/) |

- All other MySQL data types will be converted to [string](https://clickhouse.tech/docs/zh/sql-reference/data-types/string/).
- All the above types can be [nullable](https://clickhouse.tech/docs/zh/sql-reference/data-types/nullable/).

### Samples
Create a table in MySQL:
```
mysql> USE test;Database changed
mysql> CREATE TABLE `mysql_table` (
    ->   `int_id` INT NOT NULL AUTO_INCREMENT,
    ->   `float` FLOAT NOT NULL,
    ->   PRIMARY KEY (`int_id`));Query OK, 0 rows affected (0,09 sec)
mysql> insert into mysql_table (`int_id`, `float`) VALUES (1,2);Query OK, 1 row affected (0,00 sec)
mysql> select * from mysql_table;+--------+-------+| int_id | value |+--------+-------+|      1 |     2 |+--------+-------+1 row in set (0,00 sec)
```
Create a database of the MySQL type in ClickHouse and exchange data with the MySQL server:
```
CREATE DATABASE mysql_db ENGINE = MySQL('localhost:3306', 'test', 'my_user', 'user_password')
 SHOW DATABASES
 ┌─name─────┐
│ default  │
│ mysql_db │
│ system   │
└──────────┘
 SHOW TABLES FROM mysql_db
 ┌─name─────────┐
│  mysql_table │
└──────────────┘
 SELECT * FROM mysql_db.mysql_table
 ┌─int_id─┬─value─┐
│      1 │     2 │
└────────┴───────┘
 INSERT INTO mysql_db.mysql_table VALUES (3,4)
 SELECT * FROM mysql_db.mysql_table
 ┌─int_id─┬─value─┐
│      1 │     2 │
│      3 │     4 │
└────────┴───────┘
```

