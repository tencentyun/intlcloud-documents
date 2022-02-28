‘auto_increment’ 키워드는 전역에서 고유하지만 단조 증가하지 않을 수 있는 전역 고유 자동 증분 필드를 만드는 데 사용할 수 있습니다. 아래 지침에 따라 auto_increment를 사용할 수 있습니다.

## 생성
```
mysql> create table auto_inc (a int,b int,c int auto_increment,d int,key auto(c),primary key p(a,d)) shardkey=d;
Query OK, 0 rows affected (0.12 sec)
```

## 삽입
```
mysql>  insert into shard.auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
Query OK, 2 rows affected (0.05 sec)
Records: 2  Duplicates: 0  Warnings: 0
	
mysql> select * from shard.auto_inc;
+---+------+---+---+
| a | b    | c | d |
+---+------+---+---+
| 1 |    2 | 2 | 4 |
| 1 |    2 | 1 | 3 |
+---+------+---+---+
2 rows in set (0.03 sec)
```

전환 또는 재시작과 같은 프로세스가 발생하면 자동 증가 필드에 구멍이 생깁니다. 예를 들면 다음과 같습니다.
```
mysql> insert into shard.auto_inc ( a,b,d,c) values(11,12,13,0),(21,22,23,0);
Query OK, 2 rows affected (0.03 sec)
mysql> select * from shard.auto_inc;
+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
| a | b | c | d |
+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
| 21 | 22 | 2002 | 23 |
| 1 | 2 | 2 | 4 |
| 1 | 2 | 1 | 3 |
| 11 | 12 | 2001 | 13 |
+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+‐‐‐‐‐‐+
4 rows in set (0.01 sec)
```

현재 값 변경:
```
alter table auto_inc auto_increment=100
```

`select last_insert_id()`를 사용하여 자동 증분 필드의 마지막 삽입 값을 쿼리합니다.
```	
mysql> insert into auto_inc ( a,b,d,c) values(1,2,3,0),(1,2,4,0);
Query OK, 2 rows affected (0.73 sec)
		
mysql> select * from auto_inc;
+---+------+------+---+
| a | b    | c    | d |
+---+------+------+---+
| 1 |    2 | 4001 | 3 |
| 1 |    2 | 4002 | 4 |
+---+------+------+---+
2 rows in set (0.00 sec)
	
mysql> select last_insert_id();
+------------------+
| last_insert_id() |
+------------------+
| 4001             |
+------------------+
1 row in set (0.00 sec)
```

현재 select last_insert_id()를 사용하여 shard 테이블 또는 브로드캐스트 테이블의 자동 증분 필드를 쿼리할 수 있습니다. 이러한 작업은 noshard 테이블에서 지원되지 않습니다.
