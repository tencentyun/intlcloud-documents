## 샤딩된 테이블 생성
샤딩된 테이블을 생성할 때 SQL 문 끝에 shardkey 값을 지정해야 합니다. shardkey의 값은 테이블의 필드 이름이며 후속 SQL 라우팅에 사용됩니다.
```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c) ) shardkey=a;
Query OK, 0 rows affected (0.07 sec)
```

TDSQL 인스턴스에서 shardkey는 백엔드 데이터베이스의 파티션 필드에 해당하므로 모든 기본 키 및 고유 인덱스의 일부여야 합니다. 그렇지 않으면 테이블을 생성할 수 없습니다.
Use case: 고유 인덱스가 여러 개인 경우 오류가 발생합니다.
```
mysql> create table test1 ( a int, b int, c char(20),primary key (a,b),unique key u_1(a,c),unique key u_2(b,c) ) shardkey=a;;
```
상기 SQL 문에 따르면 shardkey 필드를 포함하지 않는 고유 인덱스 `u_2`가 있으므로 테이블을 생성할 수 없으며 다음과 같은 오류 메시지가 표시됩니다.
```
ERROR 1105 (HY000): A UNIQUE INDEX must include all columns in the table's partitioning function
```
기본 키 또는 unique key의 인덱스는 전역적으로 고유해야 합니다. 그렇게 하려면 인덱스에 shardkey 필드가 포함되어야 합니다.

상기 제한 사항 외에도 shardkey 필드에는 다음 요구 사항이 있습니다.
- shardkey 필드의 유형은 int, bigint, smallint, char 또는 varchar여야 합니다.
- proxy가 문자 집합을 변환하지 않고 다른 문자 집합이 다른 파티션으로 라우팅될 수 있으므로 shardkey 필드의 값에는 중국어가 포함되어서는 안 됩니다.
- shardkey 필드의 값을 update하지 마십시오.
- shardkey=a는 SQL 문의 끝에 위치해야 합니다.
- 데이터에 접근할 때 SQL 문에 shardkey 값을 지정하는 것이 좋습니다. 이는 필수는 아니지만 shardkey가 없는 SQL 문은 모든 노드로 라우팅되므로 더 많은 리소스를 소비합니다.


## 브로드캐스트 테이블 생성
작은 테이블(브로드캐스트 테이블)을 만들 수 있습니다. 각 set에는 작은 테이블의 모든 데이터가 있으므로 교차 set join을 더 쉽게 수행할 수 있습니다. 또한 분산 트랜잭션은 수정 작업의 원자성을 보장하므로 모든 set의 데이터가 정확히 동일합니다.
```
mysql> create table global_table ( a int, b int key) shardkey=noshardkey_allset;
Query OK, 0 rows affected (0.06 sec)
```

## 비분할 테이블 생성
MySQL과 동일한 구문을 사용하여 분할되지 않은 테이블을 생성할 수 있습니다. 이 유형의 테이블에 있는 모든 데이터는 첫 번째 set에 저장됩니다.
```
mysql> create table noshard_table ( a int, b int key);
Query OK, 0 rows affected (0.02 sec)
```
