Sequence 키워드 구문은 MariaDB/Oracle과 호환되지만 시퀀스는 전역적으로 증가하고 고유해야 합니다. 구체적인 사용법은 다음과 같습니다.

>?
>- TDSQL for MySQL에서 Sequence를 사용하는 경우 키워드에는 `tdsql_` 접두사가 있어야 하고 proxy 버전은 1.19.5-M-V2.0R745D005 이상이어야 합니다. `/*Proxy*/show status` 문을 실행하여 proxy 버전을 볼 수 있습니다. proxy가 이전 버전에 있는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 업그레이드할 수 있습니다.
>- 현재 Sequence는 분산 트랜잭션의 전역 고유성을 보장하기 위해 사용되며, 이는 상대적으로 성능이 낮아 동시성이 낮은 시나리오에만 적합합니다.

시퀀스를 생성하려면 CREATE SEQUENCE 시스템 권한이 필요합니다. 시퀀스를 생성하는 구문은 다음과 같습니다.
```
　　CREATE TDSQL_SEQUENCE 시퀀스 이름
　　[START WITH n]
　　[{TDSQL_MINALUE/ TDSQL_MAXMINVALUE n| TDSQL_NOMAXVALUE}]
　　[TDSQL_INCREMENT BY n]
　　[{TDSQL_CYCLE|TDSQL_NOCYCLE}]
```

## Sequence 생성
```
create tdsql_sequence test.s1 start with 12 tdsql_minvalue 10 maxvalue 50000 tdsql_increment by 5 tdsql_nocycle
create tdsql_sequence test.s2 start with 12 tdsql_minvalue 10 maxvalue 50000 tdsql_increment by 1 tdsql_cycle
```
- 상기 SQL 문에는 시작값, 최소값, 최대값, 증분, 버퍼 크기, 순환 여부 등 6개의 매개변수가 포함되어 있으며 모두 양의 정수여야 합니다.
- 이러한 매개변수의 기본값은 시작값(1), 최소값(1), 최대값(LONGLONG_MAX-1), 증분(1), 순환 여부(0)입니다.

## Sequence 삭제
```
drop tdsql_sequence test.s1
```

## Sequence 쿼리
```
show create tdsql_sequence test.s2
```

## Sequence 사용
#### Sequence 사용하여 다음 값 얻기
```
select tdsql_nextval(test.s2)
select next value for test.s2
```

```
mysql> select tdsql_nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select tdsql_nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 13 |
+----+
| 13 |
+----+
1 row in set (0.00 sec)

mysql> select next value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.01 sec)
```

#### insert 및 기타 명령문에서 nextval 사용
```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(tdsql_nextval(test.s2),3);
Query OK, 1 row affected (0.01 sec)

mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
| 14 |    3 |
+----+------+
2 rows in set (0.00 sec)
```

마지막 값은 관련 데이터를 결합하는 데 필요합니다. nextval 명령으로 얻은 적이 없으면 0이 반환됩니다.
```
select tdsql_lastval(test.s1)
select tdsql_previous value for test.s1;
```

```
mysql> select tdsql_lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

현재 값보다 커야 하는 시퀀스의 다음 값을 설정합니다. 그렇지 않으면 0이 반환됩니다.
```
select tdsql_setval(test.s2,1000,bool use)  //  use는 기본적으로 1이며, 이는 1000 값이 사용되었으며 다음 값은 1000이 아님을 나타냅니다. use가 0이면 다음 값은 1000부터 시작합니다.
```

시퀀스의 다음 값이 현재 값보다 작으면 시스템은 응답하지 않습니다.
```
mysql> select tdsql_nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+
```

설정된 다음 값이 현재 값보다 크면 설정 값이 성공적으로 반환됩니다.
```
mysql> select tdsql_setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select tdsql_nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```

강제로 다음 시퀀스 값을 설정합니다(현재 값보다 작은 값을 설정할 수 있음).
```
select tdsql_resetval(test.s2,1000)
```

강제 설정이 성공하면 설정된 값이 반환되고 그 다음 시퀀스 값이 시작됩니다.
```
mysql> select tdsql_resetval(test.s2,14);
+----+
| 14 |
+----+
| 14 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 14 |
+----+
| 14 |
+----+
1 row in set (0.01 sec)
```

일부 Sequence 키워드에는 `TDSQL_` 접두사가 붙습니다.
```
 TDSQL_CYCLE
 TDSQL_INCREMENT
 TDSQL_LASTVAL  
 TDSQL_MINVALUE 
 TDSQL_NEXTVAL  
 TDSQL_NOCACHE  
 TDSQL_NOCYCLE  
 TDSQL_NOMAXVALUE
 TDSQL_NOMINVALUE
 TDSQL_PREVIOUS 
 TDSQL_RESTART  
 TDSQL_REUSE    
 TDSQL_SEQUENCE 
 TDSQL_SETVAL   
```
