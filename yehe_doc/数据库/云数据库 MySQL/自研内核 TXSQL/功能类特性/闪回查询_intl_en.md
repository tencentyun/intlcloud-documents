## Overview
Maloperations may occur in the process of database Ops and severely affect the business. Rollback and cloning are common recovery methods for maloperations, but they are error-prone and time-consuming in case of minor data changes and urgent troubleshooting, and are uncontrollable in recovery time when dealing with major data changes.
The TXSQL team has developed and implemented the flashback query feature for the InnoDB engine. It allows you to query the historical data before a maloperation with a simple SQL statement and query the data at a specified time point through specific SQL syntax. This greatly saves the data query and recovery time and enables fast data recovery for better business continuity.

## Supported Versions
- Kernel version: MySQL 5.7 20220715 and later.
- Kernel version: MySQL 8.0 20220331 and later.

- For more information on how to view or upgrade the minor kernel version, see [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/236/36816).

## Use Cases
The flashback query feature is used to quickly query the historical data after a maloperation during database Ops.
Notes:
- Flashback query is supported only for InnoDB physical tables but not views, other engines, or functions without actual columns such as `last_insert_id()`.
- Only second-level flashback query is supported, and the accuracy cannot be fully guaranteed. If there are multiple changes within one second, any of them may be returned.
- Flashback query is supported only for primary keys (or GEN_CLUST_INDEX).
- Flashback query cannot be used in prepared statements or stored procedures.
- Flashback query does not support DDL. If you perform DDL on a table (such as TRUNCATE TABLE, which should be recovered through the recycle bin), the results obtained by flashback query may not be as expected.
- In the same statement, if multiple flashback query times are specified for the same table, the earliest time will be selected.
- Due to the time difference between the source and replica instances, if you specify the same time for flashback query, the results obtained for the instances may be different.
- Enabling the flashback query feature will delay undo log cleanup and increase the memory usage. We recommend you not set `Innodb_backquery_window` to a large value (preferably between 900 and 1,800), especially for instances with frequent business access requests.
- If the database instance restarts or crashes, the historical information before the restart or crash cannot be queried. The specified time should be within the supported range (which can be viewed through the status variables `Innodb_backquery_up_time` and `Innodb_backquery_low_time` by running `show status like '%backquery%'`).

## Instructions
Flashback query provides a new AS OF syntax. You can set the `Innodb_backquery_enable` parameter to `ON` to enable the flashback query feature and then query data at the specified time through the following syntax:
```
SELECT ... FROM <table name>
AS OF TIMESTAMP <time>;
```
**Example of querying data at the specified time**
```
MySQL [test]> create table t1(id int,c1 int) engine=innodb;
Query OK, 0 rows affected (0.06 sec)

MySQL [test]> insert into t1 values(1,1),(2,2),(3,3),(4,4);
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0

MySQL [test]> select now();
+---------------------+
| now()               |
+---------------------+
| 2022-02-17 16:01:01 |
+---------------------+
1 row in set (0.00 sec)

MySQL [test]> delete from t1 where id=4;
Query OK, 1 row affected (0.00 sec)

MySQL [test]> select * from t1;
+------+------+
| id   | c1   |
+------+------+
|    1 |    1 |
|    2 |    2 |
|    3 |    3 |
+------+------+
3 rows in set (0.00 sec)

MySQL [test]> select * from t1 as of timestamp '2022-02-17 16:01:01';
+------+------+
| id   | c1   |
+------+------+
|    1 |    1 |
|    2 |    2 |
|    3 |    3 |
|    4 |    4 |
+------+------+
4 rows in set (0.00 sec)
```
**Example of creating a table from historical data**
```
create table t3 select * from t1 as of timestamp '2022-02-17 16:01:01';
```
**Example of inserting historical data into a table**
```
insert into t4 select * from t1 as of timestamp '2022-02-17 16:01:01';
```

## Parameters
The following table lists the configurable parameters of the flashback query feature.

| Parameter | Scope | Type | Default Value | Value Range/Valid Values | Restart Required | Description | 
|---------|---------|---------|---------|---------|---------|---------|
| Innodb_backquery_enable | Global | Boolean | OFF | ON/OFF | No | The switch of the flashback query feature. | 
| Innodb_backquery_window | Global | Integer | 900 | 1–86400 | No | The time range for flashback query in seconds. The larger the value of this parameter, the longer the historical data query time supported for flashback query, and the more storage space used by the undo tablespace. | 
| Innodb_backquery_history_limit | Global | Integer | 8000000 | 1–9223372036854476000 | No | The length of the undo linked list for flashback query. If this value is exceeded, `Innodb_backquery_window` will be ignored and a purge will be triggered until the historical linked list length is lower than this value. | 




