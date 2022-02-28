TDSQL은 구문이 mariadb/Oracle과 호환되는 sequence 키워드를 지원합니다. sequence는 전역적으로 증가하고 분산 아키텍처에서 고유해야 합니다. 본문은 sequence를 사용하는 방법을 설명합니다.

시퀀스를 생성하려면 CREATE SEQUENCE 시스템 권한이 필요합니다. 시퀀스를 생성하는 구문은 다음과 같습니다.
```
　　CREATE SEQUENCE 시퀀스 이름
　　[INCREMENT BY n]
　　[START WITH n]
　　[{MAXVALUE/ MINVALUE n| NOMAXVALUE}]
　　[{CYCLE|NOCYCLE}]
　　[{CACHE n| NOCACHE}];
```

>?현재 sequence는 분산 아키텍처에서 전역적으로 고유해야 하므로 상대적으로 성능이 저하되어 동시성이 낮은 시나리오에만 적합합니다.

## 시퀀스 생성
예시는 다음과 같습니다:
```
create sequence test.s1 start with 12 minvalue 10 maxvalue 50000  increment by 5  nocycle 
create sequence test.s2 start with 12 minvalue 10 maxvalue 50000  increment by 1  cycle 
```
매개변수에는 시작 값, 최소값, 최대값, 증분 및 순환 여부가 포함됩니다.

## 시퀀스 삭제
예시는 다음과 같습니다:
```
drop sequence test.s1
```
현재 제약 조건: 모든 매개변수는 양의 정수여야 합니다.

## 시퀀스 보기
예시는 다음과 같습니다:
```
show create sequence test.s1
```

## 시퀀스 사용
#### 테이블 시퀀스 조작
```
select nextval(test.s1)
select next value for test.s1
```

예시:
```
mysql> select nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select nextval(test.s2);
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

nextval은 select 또는 다른 문에서 사용할 수 있습니다.
```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(nextval(test.s2),3);
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

#### 마지막 값 쿼리
nextval이 데이터 쿼리에 사용되지 않은 경우 0이 반환됩니다.
```
select lastval(test.s1)
select previous value for test.s1;
```

예시:
```
mysql> select lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

#### 다음 값 설정
다음 값은 증가해야 하며 그렇지 않으면 0이 반환됩니다.
```
select setval(test.s2,1000,bool use)  //  use는 기본적으로 1이며, 이는 1000 값이 사용되었으며 다음 값은 1000이 아님을 나타냅니다. use가 0이면 다음 값은 1000부터 시작합니다.
```

다음 값이 감소하면 0이 반환됩니다.
```
mysql> select nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+
```

다음 값이 증가하면 방금 설정한 값이 성공적으로 반환됩니다.
```
mysql> select setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```


다음 sequence 키워드에는 TDSQL_ 접두사가 붙습니다.
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
