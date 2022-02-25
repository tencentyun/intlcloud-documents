
## MySQL/TDSQL MySQL/TDSQL-C 확인 사항
다음 요구 사항에 따라 원본 데이터베이스의 binlog 매개 변수를 설정해야 합니다. 확인에 실패하면 본문의 지침에 따라 수정합니다.
- ‘log_bin’ 변수는 ‘ON’으로 설정해야 합니다.
- ‘binlog_format’ 변수는 ‘ROW’로 설정해야 합니다.
- ‘binlog_row_image’는 ‘FULL’로 설정해야 합니다.
- 원본 데이터베이스가 MySQL 5.6 이상인 경우 ‘gtid_mode’는 ‘ON’ 또는 ‘OFF’로만 설정할 수 있습니다. ‘OFF’로 설정하면 알람이 발생하고 ‘ON_PERMISSIVE’ 또는 ‘OFF_PERMISSIVE’로 설정하면 오류가 보고되므로 ‘ON’으로 설정하는 것이 좋습니다.
- ‘server_id’ 매개변수는 수동으로 설정해야 하며 0이 될 수 없습니다.
- ‘do_db’ 및 ‘ignore_db’를 설정할 수 없습니다.
- 원본 데이터베이스가 세컨더리 데이터베이스인 경우 ‘log_slave_updates’ 변수를 ‘ON’으로 설정해야 합니다.

## 수정 방법
### binlog 활성화 
‘log_bin’은 binlog 스위치를 제어합니다. 모든 데이터베이스 테이블 구조와 데이터 변경 사항을 기록하려면 binlog를 활성화해야 합니다. 

유사한 오류가 발생하면 다음과 같이 수정하십시오.
1. 원본 데이터베이스에 로그인합니다.
2. 원본 데이터베이스의 ‘my.cnf’ 구성 파일을 다음과 같이 수정합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
>
```
log_bin = MYSQL_BIN
binlog_format = ROW
server_id = 2         //1보다 큰 정수로 설정하는 것이 좋습니다. 이 값은 예시입니다.
binlog_row_image = FULL
```
3. 다음 명령을 실행하여 원본 데이터베이스를 다시 시작합니다.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?[\$Mysql_Dir]은 원본 데이터베이스의 설치 경로입니다. 실제 경로로 교체하십시오.
4. binlog 기능이 활성화되어 있는지 확인합니다.
```
show variables like '%log_bin%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show variables like '%log_bin%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| log_bin       | ON    |
+---------------+-------+
1 row in set (0.00 sec)
```
5. 확인 작업을 다시 실행합니다.

### binlog_format 매개변수 수정
‘binlog_format’은 다음 세 가지 binlog 형식 중 하나를 지정합니다.
- ‘STATEMENT’: 데이터를 수정하는 각 SQL 문은 master의 binlog에 기록됩니다. 데이터를 복제할 때 slave는 master에서와 동일한 SQL 문을 실행합니다. 이 형식은 binlog 크기를 줄일 수 있습니다. 그러나 slave는 특정 기능을 제대로 복제하지 못할 수 있습니다.
- ‘ROW’: binlog는 각 데이터 행의 수정 사항을 기록하고 slave는 동일한 데이터를 수정합니다. 이 형식은 올바른 master-slave 복제를 보장하지만 binlog 크기가 증가합니다.
- ‘MIXED’: 상기 두 가지 형식의 조합입니다. MySQL은 자동으로 ‘STATEMENT’ 또는 ‘ROW’ 형식을 선택하여 실행된 각 SQL 문을 기록합니다. 

따라서 올바른 master-slave 복제를 보장하려면 ‘binlog_format’ 매개변수를 ‘ROW’로 설정해야 합니다. 유사한 오류가 발생하면 다음과 같이 수정하십시오.
>?데이터베이스를 다시 시작하지 않고 이 매개변수를 수정할 수 있지만 데이터베이스에 대한 모든 비즈니스 연결을 닫아야 합니다. 원본 데이터베이스가 세컨더리인 경우 현재 비즈니스 연결이 수정 전 모드에서 계속 데이터를 쓰는 것을 방지하기 위해 프라이머리/세컨더리 동기화 SQL 스레드도 다시 시작해야 합니다.

1. 원본 데이터베이스에 로그인합니다.
2. `my.cnf` 구성 파일을 다음과 같이 수정합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
>
```
binlog_format = ROW
```
3. 매개변수 수정이 적용되는지 확인합니다.
```
show variables like "%binlog_format%";
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show variables like '%binlog_format%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| binlog_format | ROW   |
+---------------+-------+
1 row in set (0.00 sec)
```
5. 확인 작업을 다시 실행합니다.

### binlog_row_image 매개변수 수정
‘binlog_row_image’ 매개변수는 데이터 플래시백 및 프라이머리-세컨더리 복제와 같은 기능에 직접적인 영향을 미치는 사전 이미지(수정 전 콘텐츠) 및 사후 이미지(수정 후 콘텐츠)를 binlog에 기록하는 방법을 결정합니다.
‘binlog_row_image’ 매개변수는 ‘binlog_format’이 ‘ROW’로 설정된 경우에만 적용됩니다. 값의 영향은 다음과 같습니다.
- ‘FULL’: ‘ROW’ 형식에서 binlog는 사전 이미지 및 사후 이미지의 모든 열 데이터 정보를 기록합니다.
- ‘MINIMAL’: ‘ROW’ 형식에서 테이블에 기본 키나 고유 키가 없으면 사전 이미지는 모든 열을 기록하고 사후 이미지는 수정된 열을 기록합니다. 기본 키 또는 고유 키가 있는 경우 사전 이미지와 사후 이미지 모두 영향을 받는 열만 기록합니다.

따라서 원본 데이터베이스 binlog가 전체 이미지를 기록하도록 하려면 ‘binlog_row_image’를 ‘FULL’로 설정해야 합니다. 오류가 발생하면 다음과 같이 수정합니다.
>?데이터베이스를 다시 시작하지 않고 이 매개변수를 수정할 수 있지만 데이터베이스에 대한 모든 비즈니스 연결을 닫아야 합니다. 원본 데이터베이스가 세컨더리인 경우 현재 비즈니스 연결이 수정 전 모드에서 계속 데이터를 쓰는 것을 방지하기 위해 프라이머리/세컨더리 동기화 SQL 스레드도 다시 시작해야 합니다.

1. 원본 데이터베이스에 로그인합니다.
2. 원본 데이터베이스의 ‘my.cnf’ 구성 파일을 다음과 같이 수정합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
>
```
binlog_row_image = FULL
```
3. 매개변수 수정이 적용되는지 확인합니다.
```
show variables like "%binlog_row_image%";
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show variables like '%binlog_row_image%';
+------------------+-------+
| Variable_name    | Value |
+------------------+-------+
| binlog_row_image | FULL  |
+------------------+-------+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

### gtid_mode 매개변수 수정
GTID(Global Transaction Identifier)는 binlog에서 트랜잭션을 고유하게 식별합니다. GTID를 사용하면 반복되는 트랜잭션 실행으로 인한 데이터 무질서 또는 프라이머리-세컨더리 불일치를 방지할 수 있습니다.
GTID는 MySQL 5.6의 새로운 기능입니다. 따라서 이 문제는 MySQL 5.6 이상에서만 발생할 수 있습니다. DTS는 ‘gtid_mode’를 ‘ON’ 또는 ‘OFF’로만 설정할 수 있습니다. ‘ON’으로 설정하는 것이 좋습니다. 그렇지 않으면 확인 중에 알람이 트리거됩니다.

알람은 마이그레이션 또는 동기화 작업에 영향을 미치지 않지만 비즈니스에는 영향을 미칩니다. GTID가 설정된 후 증분 데이터 동기화 중에 원본 데이터베이스에서 HA 전환이 발생하면 DTS가 전환되고 다시 시작되어 작업이 거의 감지할 수 없습니다. GTID가 설정되어 있지 않으면 연결이 끊긴 후 작업이 실패하고 복구할 수 없습니다.

다음은 ‘gtid_mode’의 유효한 값입니다. 값을 수정할 때는 지정된 순서대로 단계적으로만 변경할 수 있습니다. 예를 들어 ‘OFF’를 ‘ON’으로 변경하려면 ‘OFF’ <->  ‘OFF_PERMISSIVE’ <-> ‘ON_PERMISSIVE’ <-> ‘ON’ 순서로 ‘gtid_mode’ 값을 수정해야 합니다.
- ‘OFF’: 프라이머리 데이터베이스의 모든 새 트랜잭션과 세컨더리 데이터베이스의 모든 트랜잭션은 익명이어야 합니다.
- ‘OFF_PERMISSIVE’: 프라이머리 데이터베이스의 모든 새 트랜잭션은 익명이어야 합니다. 세컨더리 데이터베이스의 트랜잭션은 익명 또는 GTID 트랜잭션일 수 있지만 GTID 트랜잭션만 될 수는 없습니다.
- ‘ON_PERMISSIVE’: 프라이머리 데이터베이스의 모든 새 트랜잭션은 GTID 트랜잭션이어야 하고 세컨더리 데이터베이스의 트랜잭션은 익명 또는 GTID 트랜잭션일 수 있습니다.
- ‘ON’: 프라이머리 데이터베이스의 모든 새 트랜잭션과 세컨더리 데이터베이스의 모든 트랜잭션은 GTID 트랜잭션이어야 합니다.

유사한 알람이 발생하면 다음과 같이 수정하십시오.
1. 원본 데이터베이스에 로그인합니다.
2. 프라이머리 및 세컨더리 데이터베이스 모두에서 ‘gtid_mode = OFF_PERMISSIVE’를 설정합니다.
```
set global gtid_mode = OFF_PERMISSIVE;
```
3. 프라이머리 및 세컨더리 데이터베이스 모두에서 ‘gtid_mode = ON_PERMISSIVE’를 설정합니다.
```
set global gtid_mode = ON_PERMISSIVE;
```
4. 각 인스턴스 노드에서 다음 명령어를 실행하여 익명 트랜잭션의 소비가 완료되었는지 확인합니다. 매개변수 값이 ‘0’이면 소비가 완료됩니다.
```
show variables like "%ONGOING_ANONYMOUS_TRANSACTION_COUNT%";
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show variables like '%ONGOING_ANONYMOUS_TRANSACTION_COUNT%';
+-------------------------------------+-------+
| Variable_name                       | Value |
+-------------------------------------+-------+
| Ongoing_anonymous_transaction_count | 0     |
+-------------------------------------+-------+
1 row in set (0.00 sec)
```
5. 프라이머리 및 세컨더리 데이터베이스 모두에서 ‘gtid_mode = ON’으로 설정합니다.
```
set global gtid_mode = ON;
```
6. my.cnf 파일에 다음 콘텐츠를 추가합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
>
```
gtid_mode = on
enforce_gtid_consistency = on
```
7. (옵션) 다음 명령을 실행하여 데이터베이스를 다시 시작합니다. MySQL 5.7.6 이하 버전의 데이터베이스는 다시 시작해야 합니다. 5.7.6 이상의 데이터베이스는 다시 시작할 필요가 없지만 모든 비즈니스 연결은 닫아야 합니다.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
8. 확인 작업을 다시 실행합니다. 

### server_id 매개변수 수정
‘server_id’ 매개변수는 수동으로 설정해야 하며 0으로 설정할 수 없습니다. 이 매개변수의 시스템 기본값은 ‘1’이지만 쿼리된 매개변수 값이 ‘1’인 경우에도 구성이 반드시 올바른 것은 아닙니다. 여전히 수동으로 설정해야 합니다.
>?데이터베이스를 다시 시작하지 않고 이 매개변수를 수정할 수 있지만 데이터베이스에 대한 모든 비즈니스 연결을 닫아야 합니다. 원본 데이터베이스가 세컨더리인 경우 현재 비즈니스 연결이 수정 전 모드에서 계속 데이터를 쓰는 것을 방지하기 위해 프라이머리/세컨더리 동기화 SQL 스레드도 다시 시작해야 합니다.

1. 원본 데이터베이스에 로그인합니다.
2. 원본 데이터베이스의 ‘my.cnf’ 구성 파일을 다음과 같이 수정합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
>
```
server_id = 2    //1보다 큰 정수로 설정하는 것이 좋습니다. 이 값은 예시입니다.
```
3. 매개변수 수정이 적용되는지 확인합니다.
```
show global variables like "%server_id%";
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show global variables like '%server_id%';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| server_id     | 2     |
+---------------+-------+
1 row in set (0.00 sec)
```
4. 확인 작업을 다시 실행합니다.

### do_db 및 ignore_db 설정 삭제
binlog는 실행된 모든 DDL 및 DML 문을 데이터베이스에 기록하고 do_db 및 ignore_db는 binlog에 대한 필터 조건을 설정하는 데 사용됩니다.
- ‘binlog_do_db’: 지정된 데이터베이스만 binlog에 기록됩니다(모든 데이터베이스는 기본적으로 기록됨).
- ‘binlog_ignore_db’: 지정된 데이터베이스는 binlog에 기록되지 않습니다.

do_db 및 ignore_db가 설정된 후 일부 데이터베이스 간 작업은 binlog에 기록되지 않으며 프라이머리-세컨더리 복제는 예외적입니다. 따라서 설정하지 않는 것이 좋습니다. 유사한 오류가 발생하면 다음과 같이 수정하십시오.
1. 원본 데이터베이스에 로그인합니다.
2. 원본 데이터베이스에서 ‘my.cnf’ 구성 파일을 수정하여 do_db 및 ignore_db 설정을 삭제합니다.
>?`my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다.
3. 다음 명령을 실행하여 원본 데이터베이스를 다시 시작합니다.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?[\$Mysql_Dir]은 원본 데이터베이스의 설치 경로입니다. 실제 경로로 교체하십시오.
4. 매개변수 수정이 적용되는지 확인합니다.
```
show master status;
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show master status;
+---------------+----------+--------------+------------------+-------------------+
| File          | Position | Binlog_Do_DB | Binlog_Ignore_DB | Executed_Gtid_Set |
+---------------+----------+--------------+------------------+-------------------+
| binlog.000011 | 154      |              |                  |                   |
+---------------+----------+--------------+------------------+-------------------+
```
5. 확인 작업을 다시 실행합니다.

### log_slave_updates 매개변수 수정
프라이머리-세컨더리 재사용 구조에서 세컨더리 데이터베이스에서 ‘log-bin’ 매개변수가 활성화되면 세컨더리 데이터베이스에서 직접 수행된 데이터 작업은 binlog에 기록될 수 있지만 프라이머리 데이터베이스에서 세컨더리 데이터베이스로의 데이터 복제는 기록되지 않습니다. 따라서 세컨더리 데이터베이스를 다른 세컨더리 데이터베이스의 프라이머리 데이터베이스로 사용하려면 ‘log_slave_updates’ 파라미터를 활성화해야 합니다. 
1. 원본 데이터베이스에 로그인합니다.
2. ‘log_slave_updates’를 ‘1’로 설정합니다.
```
set global log_slave_updates = 1;
```
3. 다음 명령을 실행하여 원본 데이터베이스를 다시 시작합니다.
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
>?[\$Mysql_Dir]은 원본 데이터베이스의 설치 경로입니다. 실제 경로로 교체하십시오.
4. 설정이 적용되었는지 확인합니다.
```
show global variables like '%log_slave_updates%';
```
시스템에서 다음과 유사한 결과가 표시되어야 합니다.
```
mysql> show global variables like '%log_slave_updates%';
+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| log_slave_updates | 1     |
+-------------------+-------+
1 row in set (0.00 sec)
```
5. 확인 작업을 다시 실행합니다.
