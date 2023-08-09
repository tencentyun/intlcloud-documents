## Overview
- DDL statements support `NO_WAIT` and `WAIT` options. If a DDL statement with `WAIT` enabled fails to obtain an MDL lock, it will wait for `WAIT` seconds before it directly returns the query result. If a DDL statement with `NO_WAIT` enabled, it will directly return the query result without waiting for the MDL lock.
- SELECT FOR UPDATE statements support `NOWAIT` and `SKIP LOCKED` options. If target rows are locked by another transaction, a SELECT FOR UPDATE statement is supposed to wait for the transaction to release the lock. But in some use cases like flash sales, you do not want to wait for a lock. You can use `SKIP LOCKED` to skip locked rows (as a result, the locked rows won't be returned in the query result set) or `NOWAIT` to return an error without waiting for the lock.

Note that `NO_WAIT` and `NOWAIT` are different keywords.

## Supported Versions
- `NO_WAIT` and `WAIT` in DDL statements are supported in kernel version MySQL 5.7 20171130 and above.
- `NOWAIT` and `SKIP LOCKED` in SELECT FOR UPDATE statements are supported in kernel version MySQL 5.7 20200630 and above (not just limited to MySQL 8.0 that natively supports the feature).

## Use Cases
Currently, DevAPI/XPlugin does not support using `SKIP LOCKED` or `NOWAIT` in SELECT FOR UPDATE/SHARE statements. Note that `NO_WAIT` in DDL statements and `NOWAIT` in SELECT FOR UPDATE statements are different keywords for historical reasons.

## Instructions
#### SELECT FOR UPDATE NOWAIT/SKIP LOCKED
```
###############session 1###############
MySQL [test]> create table t1(seat_id int, state int, primary key(seat_id)) engine=innodb;
Query OK, 0 rows affected (0.03 sec)
 
MySQL [test]> INSERT INTO t1 VALUES(1,0), (2,0), (3,0), (4,0);
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0
 
MySQL [test]> begin;
Query OK, 0 rows affected (0.01 sec)
 
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR SHARE;
+---------+-------+
| seat_id | state |
+---------+-------+
|       1 |     0 |
|       2 |     0 |
+---------+-------+
2 rows in set (0.00 sec)
 
###############session 2###############
MySQL [test]> SET SESSION innodb_lock_wait_timeout=1;
Query OK, 0 rows affected (0.00 sec)
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR UPDATE;
ERROR 1205 (HY000): Lock wait timeout exceeded; try restarting transaction
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR UPDATE NOWAIT;
ERROR 5010 (HY000): Do not wait for lock.
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR UPDATE SKIP LOCKED;
+---------+-------+
| seat_id | state |
+---------+-------+
|       3 |     0 |
|       4 |     0 |
+---------+-------+
2 rows in set (0.00 sec)
 
MySQL [test]> SELECT * FROM t1 WHERE seat_id > 0 LIMIT 2 FOR UPDATE NOWAIT;
ERROR 5010 (HY000): Do not wait for lock.
MySQL [test]> SELECT * FROM t1 WHERE seat_id > 0 LIMIT 2 FOR UPDATE SKIP LOCKED;
+---------+-------+
| seat_id | state |
+---------+-------+
|       3 |     0 |
|       4 |     0 |
+---------+-------+
2 rows in set (0.00 sec)
 
MySQL [test]> commit;
Query OK, 0 rows affected (0.00 sec)
```

#### SELECT FOR SHARE NOWAIT/SKIP LOCKED
```
###############session 1###############
MySQL [test]> begin;
Query OK, 0 rows affected (0.01 sec)
 
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR UPDATE;
+---------+-------+
| seat_id | state |
+---------+-------+
|       1 |     0 |
|       2 |     0 |
+---------+-------+
2 rows in set (0.00 sec)
 
###############session 2###############
MySQL [test]> SET SESSION innodb_lock_wait_timeout=1;
Query OK, 0 rows affected (0.00 sec)
 
MySQL [test]> begin;
Query OK, 0 rows affected (0.00 sec)
 
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 LOCK IN SHARE MODE;
ERROR 1205 (HY000): Lock wait timeout exceeded; try restarting transaction
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR SHARE;
ERROR 1205 (HY000): Lock wait timeout exceeded; try restarting transaction
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR SHARE NOWAIT;
ERROR 5010 (HY000): Do not wait for lock.
MySQL [test]> SELECT * FROM t1 WHERE state = 0 LIMIT 2 FOR SHARE SKIP LOCKED;
+---------+-------+
| seat_id | state |
+---------+-------+
|       3 |     0 |
|       4 |     0 |
+---------+-------+
2 rows in set (0.00 sec)
 
MySQL [test]> commit;
Query OK, 0 rows affected (0.00 sec)
```

#### NO_WAIT and WAIT in DDL statements
```
ALTER TABLE `table` [NO_WAIT | WAIT [n]] `command`;
DROP TABLE `table` [NO_WAIT | WAIT [n]];
TRUNCATE TABLE `table` [NO_WAIT | WAIT [n]];
OPTIMIZE TABLE `table` [NO_WAIT | WAIT [n]];
RENAME TABLE `table_src` [NO_WAIT | WAIT [n]] TO `table_dst`;
CREATE INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
CREATE FULLTEXT INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
CREATE SPATIAL INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
DROP INDEX `index` ON `table` [NO_WAIT | WAIT [n]];
```
