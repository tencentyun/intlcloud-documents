## Select
proxy를 통해 데이터베이스 인스턴스에 대한 SQL 요청의 직접 라우팅을 허용하는 hash 값의 shardkey 필드를 포함하는 것이 좋습니다. 그렇지 않으면 proxy가 클러스터의 모든 데이터베이스 인스턴스에 요청을 보내고 결과를 집계해야 하므로 성능이 저하됩니다.
```
mysql> select * from test1 where a=2;
+------+------+---------+
| a    | b    | c       |
+------+------+---------+
|    2 |    3 | record2 |
|    2 |    4 | record3 |
+------+------+---------+
2 rows in set (0.00 sec)
```

## insert/replace
proxy가 SQL에 대한 대상 백엔드 데이터베이스를 결정할 수 없기 때문에 오류를 방지하려면 shardkey 필드를 포함하십시오.
```
mysql> insert into test1 (b,c) values(4,"record3");
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table insert must has field spec

mysql> insert into test1 (a,c) values(4,"record3");
Query OK, 1 row affected (0.01 sec)
```

## delete/update
보안상의 이유로 오류를 피하기 위해 where 조건을 포함하십시오.
```
mysql> delete from test1;
ERROR 810 (HY000): Proxy ERROR:sql is too complex,need to send to only noshard table.
	Shard table delete/update must have a where clause

mysql> delete from test1 where a=1;
Query OK, 1 row affected (0.01 sec)
```
