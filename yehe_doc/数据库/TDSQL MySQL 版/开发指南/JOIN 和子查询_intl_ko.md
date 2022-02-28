TDSQL for MySQL에서 데이터는 노드 간에 수평으로 분할됩니다. 데이터베이스 성능을 향상시키려면 테이블 구조 및 SQL 문의 최적화를 우선시하고 노드 간에 데이터를 조작하지 않는 것이 좋습니다.

## 권장 SQL Statements
### 동일한 샤드 키의 where 조건이 있는 여러 샤딩된 테이블의 경우
```sql
MySQL > select * from test1 join test2 where test1.a=test2.a;     
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 1 |    2 | record1 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL > select * from test1 left join test2 on test1.a<test2.a where test1.a=1;
+---+------+---------+------+------+---------------+
| a | b    | c       | a    | d    | e             |
+---+------+---------+------+------+---------------+
| 1 |    2 | record1 |    2 |    3 | test2_record2 |
+---+------+---------+------+------+---------------+
1 row in set (0.00 sec)

MySQL> select * from test1 where test1.a in (select a from test2);        
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
| 2 |    3 | record2 |
+---+------+---------+
2 rows in set (0.00 sec)

MySQL> select a, count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;        
+---+----------+
| a | count(1) |
+---+----------+
| 1 |        1 |
| 2 |        1 |
+---+----------+
2 rows in set (0.00 sec)

MySQL> select distinct count(1) from test1 where exists (select * from test2 where test2.a=test1.a) group by a;   
+----------+
| count(1) |
+----------+
|        1 |
+----------+
1 row in set (0.00 sec)

MySQL> select count(distinct a) from test1 where exists (select * from test2 where test2.a=test1.a);        
+-------------------+
| count(distinct a) |
+-------------------+
|                 2 |
+-------------------+
1 row in set (0.00 sec)
```

### 샤딩되지 않은 테이블의 경우
```sql
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)

mysql> create table noshard_table_2 ( a int, b int key);
Query OK, 0 rows affected (0.00 sec)

mysql> select * from noshard_table,noshard_table_2;
Empty set (0.00 sec)

mysql> insert into noshard_table (a,b) values(1,2),(3,4);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> insert into noshard_table_2 (a,b) values(10,20),(30,40);
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from noshard_table,noshard_table_2;
+------+---+------+----+
| a    | b | a    | b  |
+------+---+------+----+
|    1 | 2 |   10 | 20 |
|    3 | 4 |   10 | 20 |
|    1 | 2 |   30 | 40 |
|    3 | 4 |   30 | 40 |
+------+---+------+----+
4 rows in set (0.00 sec)
```

### 브로드캐스트 테이블용
```sql
 MySQL> create table global_test(a int key, b int)shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.00 sec)

MySQL> insert into global_test(a, b) values(1,1),(2,2);
Query OK, 2 rows affected (0.00 sec)

MySQL> select * from test1, global_test;
+---+------+---------+---+------+
| a | b    | c       | a | b    |
+---+------+---------+---+------+
| 1 |    2 | record1 | 1 |    1 |
| 2 |    3 | record2 | 1 |    1 |
| 1 |    2 | record1 | 2 |    2 |
| 2 |    3 | record2 | 2 |    2 |
+---+------+---------+---+------+
4 rows in set (0.00 sec)
```

### 서브 쿼리에 shardkey가 있는 derived table의 경우
```
mysql> select a from (select * from test1 where a=1) as t;
+---+
| a |
+---+
| 1 |
+---+
1 row in set (0.00 sec)
```
>?서브 쿼리에 shardkey를 지정하지 않고도 결과를 쿼리할 수 있습니다.

## 복잡한 SQL Statements
권장 명령문으로 최적화할 수 없는 SQL문의 경우 노드 간 데이터 상호 작용이 필요하므로 상대적으로 성능이 저하됩니다.
포함:
- 서브 쿼리가 있는 쿼리.
- shardkey가 다르거나 유형이 다른 여러 테이블에 대한 join 쿼리(예시: 비샤딩 테이블 및 샤딩 테이블).

이러한 복잡한 쿼리에서 쿼리 조건은 백엔드 데이터베이스에서 쿼리에 실제로 참여하는 데이터를 추출하기 위해 샤드로 전송됩니다. 추출된 데이터는 로컬 임시 테이블에 저장된 다음 계산됩니다.

따라서 많은 양의 데이터 추출로 인한 성능 저하를 방지하기 위해 테이블의 쿼리 조건을 명시적으로 지정해야 합니다.
```sql
mysql> create table test1 ( a int key, b int, c char(20) ) shardkey=a;
Query OK, 0 rows affected (1.56 sec)

mysql> create table test2 ( a int key, d int, e char(20) ) shardkey=a;
Query OK, 0 rows affected (1.46 sec)

mysql> insert into test1 (a,b,c) values(1,2,"record1"),(2,3,"record2");
Query OK, 2 rows affected (0.02 sec)

mysql> insert into test2 (a,d,e) values(1,3,"test2_record1"),(2,3,"test2_record2");
Query OK, 2 rows affected (0.02 sec)

mysql> select * from test1 join test2 on test1.b=test2.d;
+---+------+---------+---+------+---------------+
| a | b    | c       | a | d    | e             |
+---+------+---------+---+------+---------------+
| 2 |    3 | record2 | 1 |    3 | test2_record1 |
| 2 |    3 | record2 | 2 |    3 | test2_record2 |
+---+------+---------+---+------+---------------+
2 rows in set (0.00 sec)

MySQL> select * from test1 where exists (select * from test2 where test2.a=test1.b);
+---+------+---------+
| a | b    | c       |
+---+------+---------+
| 1 |    2 | record1 |
+---+------+---------+
1 row in set (0.00 sec)
```

TDSQL은 또한 많은 복잡한 update/delete/insert 작업을 지원합니다.

이러한 작업은 select 작업을 기반으로 합니다. 데이터를 게이트웨이의 임시 테이블로 추출해야 하므로 대량의 데이터 추출로 인한 성능 저하를 방지하기 위해 쿼리 조건을 명시적으로 지정하는 것이 좋습니다.
또한 게이트웨이는 기본적으로 추출된 데이터를 잠그지 않습니다. 이는 공식 MySQL과 약간 다릅니다. 데이터를 잠가야 하는 경우 proxy 구성을 수정합니다.

```sql
MySQL [th]> update test1 set test1.c="record" where exists(select 1 from test2 where test1.b=test2.d);
Query OK, 1 row affected (0.00 sec)

MySQL [th]> update test1, test2 set test1.b=2 where test1.b=test2.d;
Query OK, 1 row affected (0.00 sec)

MySQL [th]> insert into test1 select cast(rand()*1024 as unsigned), d, e from test2;
Query OK, 2 rows affected (0.00 sec)

MySQL [th]> delete from test1 where b in (select b from test2);
Query OK, 6 rows affected (0.00 sec)

MySQL [th]> delete from test2.* using test1 right join test2 on test1.a=test2.a where test1.a is null;
Query OK, 2 rows affected (0.00 sec)
```
