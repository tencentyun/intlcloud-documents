## 機能の説明
ある種のユースケースでは、DML操作後に、直前に操作したデータ行を返す必要があります。このニーズを実現するには一般的に2つの方法があります。
- 1つ目は、トランザクションの開始後、DMLステートメントのすぐ後にSELECTステートメントを続けることです。
- 2つ目は、トリガー等を使用する比較的複雑な操作です。

前者では主にSELECTステートメントの分のオーバーヘッドが増え、後者ではSQLの実装がより複雑になり、なおかつ柔軟性も不十分になります（トリガーの作成が必要）。
このため、RETURNING構文の設計では主にそのケースに合わせた最適化が必要です。DMLステートメントの後にRETURNINGキーワードを追加することで、上記のニーズを柔軟かつ高効率に実現できます。

## サポートするバージョン
カーネルバージョン MySQL 5.7 20210330およびそれ以降

## ユースケース
現時点で、MySQL 5.7 20210330およびそれ以降のカーネルバージョンでは、それぞれ、INSERT ... RETURNING、REPLACE ... RETURNING、DELETE ... RETURNINGをサポートしています。この構文では、INSERT/REPLACE/DELETEステートメントによって操作されたすべての行（statment単位）を返すことができます。また、RETURNINGはprepared statements、ストアドプロシージャでの使用もサポートしています。

この機能を使用する場合は、次のいくつかの点に注意してください。
1. RETURNINGを使用する際、DELETE...RETURNINGステートメントは前のイメージデータを返し、INSERT/REPLACE...RETURNINGステートメントは後のイメージデータを返します。
2. 現時点ではUPDATE...RETURNINGステートメントはサポートしていません。
3. INSERT/REPLACEのケースで、外部テーブルの列はreturning中のサブクエリステートメントに対し、現時点では可視性を有しません。
4. INSERT/REPLACEのRETURNINGステートメントがlast_insert_id()を返す必要がある場合、このlast_insert_id()の値は、そのステートメントが実行に成功する前の値です。正確なlast_insert_id()値が必要な場合は、RETURNINGを使用してそのテーブルの自動インクリメント列IDを直接返すことをお勧めします。

## 利用説明
#### INSERT... RETURNING
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

#### ストアドプロシージャ
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

