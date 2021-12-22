## 기능 소개
많은 사용자는 인덱스를 삭제 가능 여부를 확인하기 위해 인덱스 숨기기 기능이 필요합니다. Invisible Index를 통해 사용자는 인덱스 삭제를 최종 결정하기 전에 응용 프로그램 또는 데이터베이스 사용자가 실제로 사용하는지(오류 발생/보고 여부) 확인할 수 있으며 이 기능은 8.0에서 5.7 버전으로 이식되었습니다.

## 지원 버전
커널 버전 MySQL 5.7 20180918 이상

## 적용 시나리오
인덱스 삭제 전, 인덱스를 invisible로 설정하여 인덱스가 유용한지 확인하고 인덱스를 안전하게 삭제할 수 있습니다.

## 사용 설명
다음 명령을 사용하여 invisible 인덱스를 생성하거나, 기존 인덱스를 invisible로 변경할 수 있습니다.
```sql
CREATE TABLE t1 (
  i INT,
  j INT,
  k INT,
  INDEX i_idx (i) INVISIBLE
) ENGINE = InnoDB;
CREATE INDEX j_idx ON t1 (j) INVISIBLE;
ALTER TABLE t1 ADD INDEX k_idx (k) INVISIBLE;
```

다음 명령을 사용하여 visible 인덱스로 변경할 수 있습니다.
```sql
ALTER TABLE t1 ALTER INDEX i_idx INVISIBLE;
ALTER TABLE t1 ALTER INDEX i_idx VISIBLE
```
