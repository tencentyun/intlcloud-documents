## 기능 소개
빠른 칼럼 추가 기능은 이전 칼럼 추가 작업에서 수행해야 하는 데이터 복사를 피하고 데이터 사전을 수정하기만 하면 큰 테이블의 칼럼을 빠르게 추가할 수 있으므로 칼럼을 추가하는 데 필요한 시간을 크게 줄일 수 있습니다. 또한, 큰 테이블과 시스템에 대한 영향을 축소합니다.

## 지원 버전
- 커널 버전 MySQL 5.7 20190830 이상
- 커널 버전 MySQL 8.0 20200630 이상

## 적용 시나리오
데이터가 많은 테이블에 칼럼을 추가해야 하는 시나리오에 적합합니다.

## 성능 데이터
데이터 볼륨이 5GB인 테이블 테스트 결과, 칼럼 추가 작업이 40초에서 1초 미만으로 감소되었습니다.

## 사용 설명
- Instant Add Column 구문
Alter Table에 algorithm=instant 절이 추가되었으며, 다음 명령으로 칼럼 추가 연산을 수행할 수 있습니다.
```
ALTER TABLE t1 ADD COLUMN c INT, ADD COLUMN d INT DEFAULT 1000, ALGORITHM=INSTANT;
```

- inplace 또는 Instant로 설정할 수 있는 매개변수 innodb_alter_table_default_algorithm이 새로 추가되었습니다.
이 매개변수는 기본적으로 inplace이며 다음과 같이 이 매개변수를 설정하여 Alter Table의 기본 알고리즘을 조정할 수 있습니다. 예시:
```
SET @@global.innodb_alter_table_default_algorithm=instant;
```
이 매개변수로 기본 알고리즘을 지정하면 알고리즘 미지정 시 테이블 변경 작업에 기본 알고리즘이 사용됩니다.
