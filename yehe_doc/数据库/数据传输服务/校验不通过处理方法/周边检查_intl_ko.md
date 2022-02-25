
## MySQL/TDSQL MySQL/TDSQL-C 확인 사항
- 확인 요건: 원본 데이터베이스의 ‘innodb_stats_on_metadata’ 환경 변수를 ‘OFF’로 설정해야 합니다. 
- 확인 설명:
   - ‘innodb_stats_on_metadata’ 매개변수가 활성화되어 있으면 ‘information_schema’ 메타데이터베이스의 테이블이 쿼리될 때마다 Innodb가 ‘information_schema.statistics’ 테이블을 업데이트하여 액세스 속도가 느려집니다. 이 매개변수를 비활성화하면 schema 테이블에 대한 액세스가 더 빨라질 수 있습니다.
   - MySQL 5.6.6 미만 버전에서는 ‘innodb_stats_on_metadata’ 매개변수의 기본값이 ‘ON’이며 ‘OFF’로 변경해야 합니다. MySQL 5.6.6 이상에서는 기본값이 ‘OFF’이므로 문제가 없습니다.

## 수정 방법
>?데이터베이스를 다시 시작하지 않고 이 매개변수를 수정할 수 있지만 데이터베이스에 대한 모든 비즈니스 연결을 닫아야 합니다. 원본 데이터베이스가 세컨더리인 경우 현재 비즈니스 연결이 수정 전 모드에서 계속 데이터를 쓰는 것을 방지하기 위해 프라이머리/세컨더리 동기화 SQL 스레드도 다시 시작해야 합니다.

1. 원본 데이터베이스에 로그인합니다.
2. ‘innodb_stats_on_metadata’의 값을 ‘OFF’로 변경합니다.
```
set global innodb_stats_on_metadata = OFF 
```
3. 설정이 적용되었는지 확인합니다.
```
show global variables like "%innodb_stats_on_metadata%";
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show globle table status like '%innodb_stats_on_metadata%';
+--------------------------+-------+
| Variable_name            | Value |
+--------------------------+-------+
| innodb_stats_on_metadata | OFF   |
+--------------------------+----- -+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

