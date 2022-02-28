

TDSQL for MySQL은 현재 Range 및 List 형식에서 레벨2 샤딩을 지원하며, 여기서 특정 테이블 생성 구문은 MySQL의 샤딩 구문과 유사합니다.

## 레벨2 샤딩 구문
레벨1의 Hash와 레벨2의 List를 사용하여 분할된 테이블을 만드는 구문은 다음과 같습니다.
```
MySQL [test]> CREATE TABLE customers_1 (
  first_name VARCHAR(25) key,
  last_name VARCHAR(25),
  street_1 VARCHAR(30),
  street_2 VARCHAR(30),
  city VARCHAR(15),
  renewal DATE
) shardkey=first_name

PARTITION BY LIST (city) (
  PARTITION pRegion_1 VALUES IN('Beijing', 'Tianjin', 'Shanghai'),
  PARTITION pRegion_2 VALUES IN('Chongqing', 'Wulumuqi', 'Dalian'),
  PARTITION pRegion_3 VALUES IN('Suzhou', 'Hangzhou', 'Xiamen'),
  PARTITION pRegion_4 VALUES IN('Shenzhen', 'Guangzhou', 'Chengdu')
);
```
   
레벨1의 Range와 레벨2의 List를 사용하여 분할된 테이블을 만드는 구문은 다음과 같습니다.
```
MySQL [test]> CREATE TABLE tb_sub_r_l (
   id int(11) NOT NULL,
   order_id bigint NOT NULL,
   PRIMARY KEY (id,order_id)) 
   PARTITION BY list(order_id)
   (PARTITION p0 VALUES in (2121122),
   PARTITION p1 VALUES in (38937383))
   TDSQL_DISTRIBUTED BY RANGE(id) (s1 values less than (100),s2 values less than (1000));
Query OK, 0 rows affected, 1 warning (0.35 sec)
```

#### 지원되는 Range 유형
- DATE, DATETIME, TIMESTAMP.
- year, month, day 기능이 지원됩니다. 함수가 비어 있으면 기본적으로 day 함수로 설정됩니다.
- TINYINT, SMALLINT, MEDIUMINT, INT, BIGINT.
- year, month, day 기능이 지원됩니다. 입력한 값을 년월일로 변환하여 샤딩된 테이블 정보와 비교한다.

#### 지원되는 List 유형
- DATE, DATETIME, TIMESTAMP.
- 년월일 기능이 지원됩니다.
- TINYINT, SMALLINT, MEDIUMINT, INT , BIGINT.

<dx-alert infotype="alarm" title="알람">
<li>TIMESTAMP 유형을 샤드키로 사용하지 마십시오. TIMESTAMP의 영향을 받아 시간대가 적용되고 2038년 이전의 시간 값만 지정할 수 있기 때문입니다.</li>
<li>shardkey가 char 또는 varchar 유형인 경우 길이는 255 미만인 것이 좋습니다.</li>
</dx-alert>

## 사용 사례 및 제안
기업용으로 가능한 한 레벨1의 샤딩된 테이블을 사용합니다.
- 사용하기 전에 장기적으로 비즈니스 시나리오에 따라 테이블 구조를 합리적으로 설계하십시오. 레벨2 샤딩은 테이블 구조가 생성된 후 오랜 시간 동안 DDL 변경이 필요하지 않은 시나리오와 로그 트랜잭션 테이블과 같이 샤딩된 데이터를 정기적으로 정리하고 다듬어야 하는 시나리오에 적합합니다.
- 레벨2 샤딩의 세분성을 합리적으로 설계합니다. 너무 세분화된 레벨2 분할을 사용하지 않는 것이 좋습니다. 그렇지 않으면 너무 많은 서브 테이블이 생성됩니다. 예를 들어, 트랜잭션 테이블을 일 또는 시간이 아닌 월별로 분할하여 파일 시스템에 너무 많은 데이터 파일이 없도록 해야 합니다.
- 레벨2 샤딩 테이블에 대해 SQL 쿼리를 수행할 때 쿼리 조건에 레벨1 샤딩과 레벨2 샤딩의 키 값을 최대한 포함하여 쿼리 실행 중 검색을 위해 많은 데이터 파일을 열 필요가 없도록 합니다.
- 레벨2 샤딩된 테이블에 대해 join 쿼리를 수행할 때 쿼리 조건에 레벨1 및 레벨2 샤딩의 키 값이 포함되지 않으면 연산 성능이 낮아져 권장하지 않습니다.
- 테이블의 기본 키 또는 고유 인덱스에는 샤드 키가 포함되어야 합니다. 그렇지 않으면 데이터 고유성을 보장할 수 없습니다.
