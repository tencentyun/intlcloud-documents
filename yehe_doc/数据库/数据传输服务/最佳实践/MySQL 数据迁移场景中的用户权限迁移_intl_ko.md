
## 작업 시나리오
NewDTS는 MySQL 데이터 마이그레이션 동안 데이터 콘텐츠 자체에 더 중점을 둡니다. 기본 테이블과 뷰만 마이그레이션하지만 사용자 권한 정보는 마이그레이션하지 않습니다. 본문은 사용자 권한을 마이그레이션하는 방법을 설명합니다. 

본문에서 pt-show-grants는 원본 데이터베이스에서 사용자 권한을 내보내고 대상 데이터베이스로 가져오는 데 사용됩니다.

## 준비 작업
- [pt-show-grants](https://www.percona.com/doc/percona-toolkit/LATEST/pt-show-grants.html)를 설치하고 기본 작업을 배웁니다. 본문은 pt-show-grants 3.2.0을 예로 사용합니다.
- 원본 데이터베이스에서 마이그레이션 계정을 승인합니다. 다음은 ‘dts’ 사용자를 예로 사용합니다.
```
CREATE USER 'dts'@'%' IDENTIFIED BY '마이그레이션 비밀번호'; 
GRANT SELECT ON `mysql`.* TO 'dts'@'%';
```
- 대상 데이터베이스에서 마이그레이션 계정에 권한을 부여합니다. 다음은 ‘dts’ 사용자를 예로 사용합니다. 
```
CREATE USER 'dts'@'%' IDENTIFIED BY '마이그레이션 비밀번호';
GRANT SELECT,CREATE USER,LOCK TABLES,SHOW VIEW,TRIGGER,ALTER,ALTER ROUTINE,CREATE,CREATE ROUTINE,CREATE TABLESPACE,CREATE TEMPORARY TABLES,CREATE VIEW,DELETE,DROP,EVENT,EXECUTE, INDEX,INSERT,PROCESS,REFERENCES,RELOAD,UPDATE,SHOW DATABASES on *.* to 'dts'@'%';
FLUSH PRIVILEGES;
```
- 마이그레이션 중에는 마이그레이션 세션 이외의 세션을 대상 데이터베이스에 쓰지 않는 것이 좋습니다. 대상 데이터베이스에 액세스해야 하는 경우 읽기 전용 권한이 있는 계정을 만드는 것이 좋습니다. 이는 데이터 충돌 및 작업 실패를 유발할 수 있는 이중 쓰기의 위험을 피하는 데 도움이 됩니다. 다음은 ‘read_only’ 사용자를 예로 사용합니다.
```
CREATE USER 'read_only'@'%' IDENTIFIED BY '마이그레이션 비밀번호';
GRANT SELECT, SHOW DATABASES, SHOW VIEW on *.* to 'read_only'@'%';
FLUSH PRIVILEGES;
```

## 주의 사항
- 대상 데이터베이스가 TencentDB for MySQL인 경우 다음 일반 권한만 가져올 수 있지만 상위 수준 권한은 가져올 수 없습니다. 이 제한은 주로 높은 권한을 가진 사용자의 오작동으로 인한 비즈니스 위험을 피하기 위해 사용됩니다.
SELECT, CREATE USER, LOCK TABLES, SHOW VIEW, TRIGGER, ALTER, ALTER ROUTINE, CREATE,CREATE ROUTINE, CREATE TABLESPACE, CREATE TEMPORARY TABLES, CREATE VIEW,DELETE,DROP,EVENT,EXECUTE, INDEX, INSERT, PROCESS, REFERENCES, RELOAD, UPDATE, SHOW DATABASES, REPLICATION CLIENT, REPLICATION SLAVE 권한 계정.
- 원본 데이터베이스에 대해 pt-show-grants에 의해 생성된 SQL 문은 원본 MySQL 버전에 따라 다릅니다. 5.7.6 미만 버전에서 생성된 명령문은 5.7.6 이상의 대상 데이터베이스로 가져올 수 없습니다.

## 작업 단계
1. 원본 데이터베이스에서 다음 명령을 실행하여 사용자 계정 정보를 내보냅니다.
‘--ignore’를 지정하여 MySQL에서 가져올 수 없는 높은 권한의 계정을 필터링할 수 있습니다.
```
pt-show-grants --user=root --host=<src host or ip> --port=<src port> --user=<user> --password=<password> --ignore 'mysql.sys'@'localhost','mysql.session'@'localhost','mysql.infoschema'@'localhost','root','root'@'localhost' > account.sql
```
2. 사용자 계정 정보를 대상 데이터베이스로 가져옵니다.
```
mysql -u<user> -p<password> -h<dst ip or host> -P<dst port> -e "source account.sql"
```
다음은 MySQL 5.7.6 이상에서 내보낸 샘플 SQL 문입니다.
```
-- Grants dumped by pt-show-grants
-- Dumped from server xxxx via TCP/IP, MySQL 8.0.22-txsql at 2021-09-01 11:28:21
-- Grants for 'dts'@'%'
CREATE USER IF NOT EXISTS 'dts'@'%';
ALTER USER 'dts'@'%' IDENTIFIED WITH 'mysql_native_password' AS '*F2XFE7135318FD1F12CDF7B027506096F223DDD46' REQUIRE NONE PASSWORD EXPIRE DEFAULT ACCOUNT UNLOCK PASSWORD HISTORY DEFAULT PASSWORD REUSE INTERVAL DEFAULT PASSWORD REQUIRE CURRENT DEFAULT;
GRANT LOCK TABLES, PROCESS, RELOAD, REPLICATION CLIENT, REPLICATION SLAVE, SELECT, SHOW DATABASES, SHOW VIEW ON *.* TO `dts`@`%`;
GRANT SELECT ON `mysql`.* TO `dts`@`%`;
```
다음은 v5.7.6 미만의 MySQL에서 내보낸 샘플 SQL 문입니다.
```
-- Grants dumped by pt-show-grants
-- Dumped from server xxxx via TCP/IP, MySQL 5.6.16-log at 2021-09-01 11:33:53
-- Grants for 'dts'@'%'
GRANT LOCK TABLES, PROCESS, RELOAD, REPLICATION CLIENT, REPLICATION SLAVE, SELECT, SHOW VIEW ON *.* TO 'dts'@'%' IDENTIFIED BY PASSWORD '*47D7DB84D97A8D7EFD5B3CFA20A7A2433A9E86A4';
GRANT ALL PRIVILEGES ON `__tencentdb__`.* TO 'dts'@'%';
GRANT SELECT ON `mysql`.* TO 'dts'@'%';
```

