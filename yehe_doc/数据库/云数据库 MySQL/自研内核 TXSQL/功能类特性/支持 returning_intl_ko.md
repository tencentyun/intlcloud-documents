## 기능 소개
일부 사용 시나리오에서는 DML 작업 후 방금 작업된 데이터 행을 반환해야 합니다. 일반적으로 이를 구현하는 방법은 두 가지가 있습니다.
- 첫 번째는 트랜잭션 활성화 후 DML 명령 뒤에 SELECT 명령을 붙이는 것입니다.
- 두 번째는 트리거 등 더 복잡한 작업을 사용하여 달성하는 것입니다.

전자는 주로 SELECT 명령의 오버헤드를 증가시키는 반면 후자는 SQL 구현이 더 복잡하고 유연성은 떨어지도록 만듭니다(트리거 생성 필요).
따라서 RETURNING 구문의 설계는 주로 이 시나리오의 최적화를 목표로 하며, DML 명령 뒤에 RETURNING 키워드를 추가함으로써 상기 요구 사항을 유연하고 효율적으로 구현할 수 있습니다.

## 지원 버전
커널 버전 MySQL 5.7 20210330 이상

## 적용 시나리오
현재 MySQL 5.7 20210330 이상의 커널 버전은 INSERT ... RETURNING, REPLACE ... RETURNING, DELETE ... RETURNING을 지원합니다. 이 구문을 사용하면 INSERT/REPLACE/DELETE 명령(단위 statment)으로 작업된 모든 행을 반환할 수 있습니다. 또한, RETURNING은 prepared statements과 저장 과정 중의 사용도 지원합니다.

이 기능을 사용할 때 다음 사항에 주의해야 합니다.
1. RETURNING 사용 시, DELETE...RETURNING 명령은 이전 미러링 이미지 데이터를 반환하고, INSERT/REPLACE...RETURNING 명령은 이후 데이터를 미러링 이미지 데이터를 반환합니다.
2. UPDATE...RETURNING 명령은 현재 지원되지 않습니다.
3. INSERT/REPLACE 시나리오에서 외부 계층 테이블 열은 returning의 서브 쿼리 명령에서 가시적으로 나타나지 않습니다.
4. INSERT/REPLACE의 RETURNING 명령이 last_insert_id()를 반환해야 하는 경우, last_insert_id()의 값은 명령이 성공적으로 실행되기 전의 값입니다. 정확한 last_insert_id() 값을 얻으려면 RETURNING을 사용하여 테이블의 자동 증가 열 ID를 직접 반환하는 것이 좋습니다.

## 사용 설명
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

#### 스토리지 과정
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

