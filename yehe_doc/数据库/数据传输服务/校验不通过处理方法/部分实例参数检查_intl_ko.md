
## MySQL/TDSQL MySQL/TDSQL-C/MariaDB/Percona 확인 사항
- 원본 데이터베이스 테이블의 ‘row_format’은 ‘FIXED’일 수 없습니다.
- 원본 및 대상 데이터베이스의 ‘lower_case_table_names’ 변수는 동일해야 합니다.
- 대상 데이터베이스의 ‘max_allowed_packet’ 매개변수는 4MB 이상으로 설정해야 합니다.
- 원본 데이터베이스의 ‘connect_timeout’ 변수는 10을 초과해야 합니다.
- MySQL/TDSQL MySQL/TDSQL-C에서 MySQL로 마이그레이션할 때 시간이 많이 걸리는 SQL 문이 원본 데이터베이스에서 실행 중인 경우 ‘시간이 많이 걸리는 SQL 문이 원본 데이터베이스에서 실행 중이므로 테이블 잠금이 발생할 수 있습니다. 나중에 다시 시도하거나 원본 데이터베이스에서 SQL 문을 처리하십시오’라는 메시지가 보고됩니다. 

## 수정 방법
### 원본 데이터베이스에서 row_format 매개변수 수정
데이터베이스 테이블의 ‘row_format’ 값이 ‘FIXED’인 경우 테이블의 각 행의 저장 길이가 제한을 초과하면 데이터 오버플로가 발생하고 오류가 보고됩니다. 따라서 콘텐츠 길이에 따라 각 행의 저장 길이가 달라지도록 ‘DYNAMIC’과 같은 다른 형식으로 수정해야 합니다. 

유사한 오류가 발생하면 다음과 같이 수정하십시오.
1. 원본 데이터베이스에 로그인합니다.
2. ‘row_format’을 ‘DYNAMIC’으로 설정합니다.  
```
alter table table_name row_format = DYNAMIC
```
3. 설정이 적용되었는지 확인합니다.
```
show table status like '%row_format%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show table status like '%row_format%';
+---------------+----------+
| Variable_name | Value    |
+---------------+----------+
| row_format    | DYNAMIC  |
+---------------+----------+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

### lower_case_table_names를 원본 및 대상 데이터베이스에서 동일한 값으로 만들기
‘lower_case_table_names’는 MySQL에서 대소문자 구분을 설정합니다. 다음과 같은 유효 값이 있습니다.
Windows 및 macOS 환경은 대소문자를 구분하지 않지만 Linux 환경은 대소문자를 구분합니다. 다른 운영 체제 간의 호환성을 보장하려면 동일한 대소문자 구분 규칙을 사용해야 합니다.

- 0: 저장된 테이블의 이름은 지정된 대소문자를 사용하고 비교하는 동안 대소문자를 구분합니다.
- 1: 저장된 테이블의 이름은 디스크에서 소문자이며 비교 시 대소문자를 구분하지 않습니다.
- 2: 저장된 테이블의 이름은 지정된 대소문자를 사용하고 비교하는 동안 소문자입니다.

유사한 오류가 발생하면 다음과 같이 원본 및 대상 데이터베이스의 매개변수를 동일한 값으로 설정합니다.
1. 원본 데이터베이스에 로그인합니다.
2. 원본 및 대상 데이터베이스에서 ‘lower_case_table_names’ 값을 확인합니다.
```
show variables like '%lower_case_table_names%';
```
3. ‘lower_case_table_names’ 매개변수를 수정합니다.
```
alter global lower_case_table_names = 1
```
4. 다음 명령을 실행하여 데이터베이스를 다시 시작합니다.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
5. 설정이 적용되었는지 확인합니다.
```
show variables like '%lower_case_table_names%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show variables like '%lower_case_table_names%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| lower_case_table_names | 1     |
+------------------------+-------+
1 row in set (0.00 sec)
```
6. 확인 작업을 다시 실행합니다.

### 대상 데이터베이스에서 max_allowed_packet 매개변수 수정 
‘max_allowed_packet’은 전송할 수 있는 패킷의 최대 크기입니다. 값이 너무 크면 더 많은 메모리가 사용되어 패킷이 손실되고 큰 예외 이벤트 패킷의 SQL 문을 캡처할 수 없습니다. 값이 너무 작으면 프로그램 오류가 발생하여 백업 실패 및 네트워크 패킷의 빈번한 송수신으로 인해 시스템 성능이 저하됩니다.

유사한 오류가 발생하면 다음과 같이 수정하십시오.
1. 대상 데이터베이스에 로그인합니다.
2. ‘max_allowed_packet’ 매개변수를 수정합니다. 
```
set global max_allowed_packet = 4M
```
3. 설정이 적용되었는지 확인합니다.
```
show global variables like '%max_allowed_packet%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show global variables like '%max_allowed_packet%';
+------------------------+---------+
| Variable_name          | Value   |
+------------------------+---------+
| max_allowed_packet     | 4194304 |
+------------------------+---------+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

### 원본 데이터베이스에서 connect_timeout 변수 수정
‘connect_timeout’은 데이터베이스 연결 시간입니다. ‘connect_timeout’ 경과 후의 연결 요청은 거부됩니다. 이 값이 너무 작으면 데이터베이스 연결이 자주 닫혀 처리 효율성에 영향을 줍니다. 따라서 10보다 큰 값을 설정하는 것이 좋습니다.

유사한 오류가 발생하면 다음과 같이 수정하십시오.
1. 원본 데이터베이스에 로그인합니다.
2. ‘connect_timeout’ 매개변수를 수정합니다.
```
set global connect_timeout = 10
```
3. 매개변수가 성공적으로 수정되었는지 확인합니다.
```
show global variables like '%connect_timeout%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show global variables like '%connect_timeout%';
+------------------------+-------+
| Variable_name          | Value |
+------------------------+-------+
| connect_timeout        | 10    |
+------------------------+-------+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

