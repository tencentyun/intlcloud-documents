## 機能の説明
- DDLはNO_WAITおよびWAITオプションをサポートします。DDL操作に対し、WAITを設定することで、MDL LOCKの秒数待機し、設定した時間内にMDL LOCKを取得できなければ直接返すことができます。あるいは、NO_WAITオプションを指定し、MDL LOCKを取得できなければ直接返すこともできます。
- SELECT FOR UPDATEはNOWAITおよびSKIP LOCKEDオプションをサポートします。従来のSELECT FOR UPDATEロジックでは、目的の行データが別のトランザクションによってロックされた場合、そのトランザクションがロックをリリースするまで待つ必要がありました。しかし、seckillのようなケースで、ロックを待機したくない場合は、SKIP LOCKEDおよびNOWAITオプションによって、ロック待機不要の機能を利用できるようになりました。SKIP LOCKEDステートメントはロックされている行をスキップでき、これらの行は結果セットに表示されません。NOWAITステートメントではロックされた行に遭遇しても待機せず、エラーを表示します。

この2種類のNO WAITを使用する際のキーワードは異なることに注意する必要があります。

## サポートするバージョン
- カーネルバージョン MySQL 5.7 20171130およびそれ以降では、DDLステートメントがNO_WAITおよびWAITオプションをサポートします。
- カーネルバージョン MySQL 5.7 20200630およびそれ以降（この機能はMySQL 8.0から移植されています。バージョン8.0ではネイティブサポートのため）では、SELECT FOR UPDATEステートメントがNOWAITおよびSKIP LOCKEDオプションをサポートします。

## ユースケース
DevAPI/XPluginは現時点ではSELECT FOR UPDATE/SHAREステートメントのSKIP LOCKEDおよびNOWAITオプション使用をサポートしていません。過去の理由により、DDLのNO_WAITキーワードとSELECT FOR UPDATEのNOWAITキーワードは異なるものになっているため、注意して区別する必要があります。

## 利用説明
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

#### DDLステートメントのNO_WAITおよびWAITオプション
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
