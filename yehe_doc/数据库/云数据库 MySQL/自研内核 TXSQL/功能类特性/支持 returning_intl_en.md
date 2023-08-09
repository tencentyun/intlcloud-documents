## Overview
In some scenarios, you need to retrieve the rows manipulated by DML statements. There are generally two ways to do so:
- Add a SELECT statement after the DML statement if the transaction is enabled.
- Use a trigger or other complex operations.

However, running a SELECT statement increases query costs, and creating a trigger makes SQL implementation more complex and inflexible.
Therefore, TXSQL supports the RETURNING keyword to optimize such scenarios. The above requirements can be flexibly and efficiently met by appending RETURNING to a DML statement.

## Supported Versions
Kernel version: MySQL 5.7 20210330 and above.

## Use Cases
MySQL 5.7 20210330 and above support INSERT ... RETURNING, REPLACE ... RETURNING, and DELETE ... RETURNING. The RETURNING keyword returns all rows that have been manipulated by an INSERT/REPLACE/DELETE statement. RETURNING can also be used in prepared statements and stored procedures.

Notes:
1. For DELETE ... RETURNING, the returned data rows are pre-images, while for INSERT/REPLACE ... RETURNING, they are post-images.
2. Currently, UPDATE ... RETURNING is not supported.
3. For INSERT/REPLACE ... RETURNING, columns in the outer table are currently invisible to the subquery in the RETURNING clause.
4. INSERT/REPLACE ... RETURNING only returns the value of `last_insert_id()` before the statement is executed successfully. To obtain the true value of `last_insert_id()`, you should use RETURNING to return the auto-increment column ID of the table.

## Instructions
#### INSERT ... RETURNING
```
MySQL [test]> CREATE TABLE `t1` (id1 INT);
Query OK, 0 rows affected (0.04 sec)

MySQL [test]> CREATE TABLE `t2` (id2 INT);
Query OK, 0 rows affected (0.03 sec)

MySQL [test]> INSERT INTO  t2 (id2) values (1);
Query OK, 1 row affected (0.00 sec)

MySQL [test]> INSERT INTO t1 (id1) values (1) returning *, id1 * 2, id1 + 1, id1 * id1 as alias, (select * from t2); 
+------+---------+---------+-------+--------------------+
| id1  | id1 * 2 | id1 + 1 | alias | (select * from t2) |
+------+---------+---------+-------+--------------------+
|    1 |       2 |       2 |     1 |                  1 |
+------+---------+---------+-------+--------------------+
1 row in set (0.01 sec)

MySQL [test]> INSERT INTO t1 (id1) SELECT id2 from t2 returning id1;
+------+
| id1  |
+------+
|    1 |
+------+
1 row in set (0.01 sec)
```

#### REPLACE ... RETURNING
```
MySQL [test]> CREATE TABLE t1(id1 INT PRIMARY KEY, val1 VARCHAR(1));
Query OK, 0 rows affected (0.04 sec)

MySQL [test]> CREATE TABLE t2(id2 INT PRIMARY KEY, val2 VARCHAR(1));
Query OK, 0 rows affected (0.03 sec)

MySQL [test]> INSERT INTO t2 VALUES (1,'a'),(2,'b'),(3,'c');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0

MySQL [test]> REPLACE INTO t1 (id1, val1) VALUES (1, 'a');
Query OK, 1 row affected (0.00 sec)

MySQL [test]> REPLACE INTO t1 (id1, val1) VALUES (1, 'b') RETURNING *;
+-----+------+
| id1 | val1 |
+-----+------+
|   1 | b    |
+-----+------+
1 row in set (0.01 sec)
```

#### DELETE ... RETURNING
```
MySQL [test]> CREATE TABLE t1 (a int, b varchar(32));
Query OK, 0 rows affected (0.04 sec)

MySQL [test]> INSERT INTO t1 VALUES
    ->   (7,'ggggggg'), (1,'a'), (3,'ccc'),
    ->   (4,'dddd'), (1,'A'), (2,'BB'), (4,'DDDD'),
    ->   (5,'EEEEE'), (7,'GGGGGGG'), (2,'bb');
Query OK, 10 rows affected (0.03 sec)
Records: 10  Duplicates: 0  Warnings: 0

MySQL [test]> DELETE FROM t1 WHERE a=2 RETURNING *;
+------+------+
| a    | b    |
+------+------+
|    2 | BB   |
|    2 | bb   |
+------+------+
2 rows in set (0.01 sec)

MySQL [test]> DELETE FROM t1 RETURNING *;
+------+---------+
| a    | b       |
+------+---------+
|    7 | ggggggg |
|    1 | a       |
|    3 | ccc     |
|    4 | dddd    |
|    1 | A       |
|    4 | DDDD    |
|    5 | EEEEE   |
|    7 | GGGGGGG |
+------+---------+
8 rows in set (0.01 sec)
```

#### Stored procedure
```
MySQL [test]> CREATE TABLE `t` (id INT);
Query OK, 0 rows affected (0.03 sec)

MySQL [test]> delimiter $$
MySQL [test]> CREATE PROCEDURE test(in param INT)
    -> BEGIN
    ->     INSERT INTO t (id) values (param) returning *;
    -> END$$
Query OK, 0 rows affected (0.00 sec)
MySQL [test]> delimiter ;

MySQL [test]> CALL test(100);
+------+
| id   |
+------+
|  100 |
+------+
1 row in set (0.01 sec)

Query OK, 0 rows affected (0.01 sec)
```

