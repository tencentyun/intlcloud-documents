## 작업 시나리오
데이터 마이그레이션, 동기화 또는 구독 작업의 원본 데이터베이스가 자체 구축한 MySQL/TDSQL MySQL/TDSQL-C MySQL 데이터베이스인 경우, 확인하는 동안 원본 데이터베이스의 요구 사항을 충족하도록 자체 구축 데이터베이스의 Binlog를 설정해야 합니다.

## 작업 영향
이 작업을 수행하려면 데이터베이스를 다시 시작해야 하며 이는 비즈니스에 영향을 줍니다. 사용량이 적은 시간에 수행하는 것이 좋습니다. 

## 작업 단계
1. 원본 데이터베이스에 로그인합니다.
2. `my.cnf` 구성 파일을 다음과 같이 수정합니다. 
> ?
> - `my.cnf` 구성 파일의 기본 경로는 `/etc/my.cnf`입니다. 실제 조건에 따라 입력합니다. 
> - 최소 3일 동안 원본의 Binlog를 보관하는 것이 좋습니다. 그렇지 않으면 체크포인트에서 작업을 재개할 수 없으며 실패합니다.
>    - `my.cnf` 구성 파일의 수정 사항은 영구적으로 적용됩니다. 사용자가 일시적으로만 적용하려면 `set global expire_logs_days=3` 명령을 실행하여 수정하십시오.
>    - MySQL 8.0 이상에서는 `binlog_expire_logs_seconds`를 사용하여 Binlog 보관 시간을 수정할 수도 있습니다. 이 매개변수는 초 단위까지 정확합니다.
>
```
log_bin = MYSQL_BIN
binlog_format = ROW
server_id = 2    //1보다 큰 정수로 설정하는 것이 좋습니다. 이 값은 예시입니다.
binlog_row_image = FULL
expire_logs_days=3  //binlog의 보관 시간 수정, 3일 이상을 권장
```
3. MySQL 프로세스를 다시 시작합니다. 
```
[\$Mysql_Dir]/bin/mysqladmin -u root -p shutdown
[\$Mysql_Dir]/bin/safe_mysqld &
```
> ?[$Mysql_Dir]은 원본 데이터베이스의 설치 경로입니다. 실제 경로로 교체하십시오. 

