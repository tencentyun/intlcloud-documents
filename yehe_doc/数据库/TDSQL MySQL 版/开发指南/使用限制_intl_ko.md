## 기능 제한
- 사용자 정의 함수, 이벤트 및 테이블 스페이스는 지원되지 않습니다.
- 뷰, 저장 프로시저, 트리거 및 커서는 지원되지 않습니다.
- 외래 키 및 자체 빌드 파티션은 지원되지 않습니다.
- BEGIN END, LOOP 및 UNION과 같은 복합 문은 지원되지 않습니다.
- 프라이머리/세컨더리 동기화와 관련된 SQL 구문은 지원되지 않습니다.

## 작은 구문에 대한 제한
### DDL

- CREATE TABLE ... SELECT는 지원되지 않습니다. 
- CREATE TEMPORARY TABLE은 지원되지 않습니다. 
- CREATE/DROP/ALTER SERVER/LOGFILE GROUP은 지원되지 않습니다.
- ALTER는 shardkey의 이름을 바꾸는 데 지원되지 않지만 유형을 변경하는 데 사용할 수 있습니다.
- RENAME은 지원되지 않습니다.

### DML
- SELECT INTO OUTFILE/INTO DUMPFILE/INTO var_name은 지원되지 않습니다.
- query_expression_options는 지원되지 않습니다. 예시: HIGH_PRIORITY/STRAIGHT_JOIN/SQL_SMALL_RESULT/SQL_BIG_RESULT/SQL_BUFFER_RESULT/SQL_CACHE/SQL_NO_CACHE/SQL_CALC_FOUND_ROWS
- 열 이름이 없는 INSERT/REPLACE는 지원되지 않습니다.
- ORDER BY/LIMIT는 전역 DELETE/UPDATE에 사용할 수 없습니다(>=14.4버전 지원).
- WHERE 조건이 없는 UPDATE/DELETE는 지원되지 않습니다.
- LOAD DATA/XML은 지원되지 않습니다.
- DELAYED 및 LOW_PRIORITY는 SQL 문에서 사용할 수 없습니다.
- INSERT ... SELECT(>14.4버전 지원)는 지원되지 않습니다.
- SET @c=1, @d=@c+1과 같이 SQL의 변수에 대한 참고 및 연산은 지원되지 않습니다. SELECT @c, @d
- index_hint는 지원되지 않습니다.
- HANDLER/DO는 지원되지 않습니다.


### SQL 관리
- ANALYZE/CHECK/CHECKSUM/OPTIMIZE/REPAIR TABLE은 지원되지 않으며, 패스스루 구문으로 수행해야 합니다.
- CACHE INDEX는 지원되지 않습니다.
- FLUSH는 지원되지 않습니다.
- KILL은 지원되지 않습니다.
- LOAD INDEX INTO CACHE는 지원되지 않습니다.
- RESET은 지원되지 않습니다.
- SHUTDOWN은 지원되지 않습니다.
- SHOW BINARY LOGS/BINLOG EVENTS는 지원되지 않습니다.
- SHOW WARNINGS/ERRORS 및 LIMIT/COUNT 조합은 지원되지 않습니다.


### 기타 제한
기본적으로 최대 1000개의 테이블을 생성할 수 있습니다. 더 많은 테이블을 생성해야 하는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 신청할 수 있습니다.
