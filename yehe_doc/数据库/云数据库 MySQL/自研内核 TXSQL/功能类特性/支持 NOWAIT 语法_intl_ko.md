## 기능 소개
- DDL은 NO_WAIT 및 WAIT 옵션을 지원합니다. DDL 작업의 경우 WAIT를 통해 MDL LOCK을 기다리는 시간(초)을 설정할 수 있으며, 설정된 시간 내에 MDL LOCK을 얻지 못하면 직접 반환하거나 NO_WAIT 옵션을 지정할 수 있으며 MDL LOCK을 가져오지 못한 경우 직접 반환할 수도 있습니다.
- SELECT FOR UPDATE는 NOWAIT 및 SKIP LOCKED 옵션을 지원합니다. 원래의 SELECT FOR UPDATE 논리에서는 타깃 행 데이터가 다른 트랜잭션에 의해 잠겨 있으면 트랜잭션이 잠금을 릴리스할 때까지 기다려야 하지만 스파이크와 같은 일부 시나리오에서는 잠금이 해제될 때까지 기다릴 필요가 없는 SKIP LOCKED 및 NOWAIT 기능을 제공합니다. SKIP LOCKED 명령은 잠긴 행을 건너뛰고 이러한 행은 결과 집합에 나타나지 않습니다. NOWAIT 명령은 잠긴 행을 기다리지 않고 동시에 오류를 보고합니다.

이 두 가지 유형의 NO WAIT에서 사용하는 키워드는 다르다는 점에 유의해야 합니다.

## 지원 버전
- 커널 버전 MySQL 5.7 20171130 이상, DDL 명령은 NO_WAIT 및 WAIT 옵션을 지원합니다.
- 커널 버전 MySQL 5.7 20200630 이상(이 기능은 MySQL 8.0에서 이식되었으므로 버전 8.0이 기본적으로 지원됨), SELECT FOR UPDATE 명령은 NOWAIT 및 SKIP LOCKED 옵션을 지원합니다.

## 적용 시나리오
DevAPI/XPlugin은 현재 SELECT FOR UPDATE/SHARE 명령의 SKIP LOCKED 및 NOWAIT 옵션을 지원하지 않습니다. 이런 이유로 DDL의 NO_WAIT 키워드와 SELECT FOR UPDATE의 NOWAIT 키워드는 서로 다른 두 개의 키워드이므로 구별해야 합니다.

## 사용 설명
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

#### DDL 명령 NO_WAIT 및 WAIT 옵션
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
