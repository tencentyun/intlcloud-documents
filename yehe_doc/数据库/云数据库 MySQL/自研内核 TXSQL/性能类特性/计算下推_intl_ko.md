## 기능 소개
이 함수는 단일 테이블 쿼리의 LIMIT/OFFSET 또는 SUM 작업을 InnoDB로 푸시하여 쿼리 딜레이 시간을 효과적으로 줄입니다.
- LIMIT/OFFSET이 2단계 인덱스로 푸시 다운되면, 이 기능은 ‘테이블로 돌아가기’ 작업을 피하고 스캐닝 비용을 효과적으로 절감합니다.
- SUM 작업이 InnoDB로 푸시 다운되면 InnoDB 계층에서 계산이 수행되어 ‘최종’ 결과를 반환하므로 Server 계층과 InnoDB 엔진 계층에서 ‘각 행’ 레코드를 여러 번 스프린트하는 비용을 절약할 수 있습니다.

## 지원 버전
- LIMIT/OFFSET 최적화에 해당하는 커널 버전 MySQL 5.7 20180530
- SUM 작업 푸시 다운에 해당하는 커널 버전 MySQL 5.7 20180918

## 적용 시나리오
- 이 기능은 `Select *from tbl Limit 10”, “Select* from tbl Limit 10,2`, `Select sum(c1) from tbl` 등의 명령과 같이 단일 테이블 쿼리에 LIMIT/OFFSET 또는 SUM이 있는 시나리오에 주로 사용됩니다.
- 최적화 불가 시나리오:
  - 쿼리 명령에 distinct, group by, having이 있는 경우.
  - 중첩 서브 쿼리가 있는 경우.
  - FULLTEXT 인덱스를 사용하는 경우.
  - order by가 있고 옵티마이저는 index를 사용하여 order by를 구현할 수 없는 경우.
  - 다중 범위 MRR을 사용하는 경우.
  - SQL_CALC_FOUND_ROWS가 있는 경우.

## 성능 데이터
sysbench가 백만 개의 데이터 행을 가져오기한 후:
- `select * from sbtest1 limit 1000000,1;` 실행 시간이 6.3초에서 2.8초로 감소했습니다.
- `select sum(k) from sbtest1;` 실행 시간이 5.4초에서 1.5초로 감소했습니다.

## 사용 설명
SQL 실행 중 해당 기능 제어 매개변수의 활성화/비활성화 상황에 따라, 쿼리 옵티마이저는 자동으로 쿼리 플랜을 다시 작성하여 계산 푸시다운의 최적화를 완료합니다.
매개변수는 다음과 같습니다.

| 매개변수 이름                     | 동적 | 유형 | 기본값 | 매개변수 값 범위 | 설명                             |
| -------------------------- | ---- | ---- | ---- | ---------- | -------------------------------- |
| cdb_enable_offset_pushdown | Yes  | bool | ON   | {ON,OFF}   | LIMIT/OFFSET 푸시 다운 제어, 기본 활성화 |
| cdb_enable_sumagg_pushdown | Yes  | bool | OFF  | {ON,OFF}   | SUM 푸시 다운 제어, 기본 비활성화          |

