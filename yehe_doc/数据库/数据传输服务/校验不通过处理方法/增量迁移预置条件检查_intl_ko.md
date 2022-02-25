## 확인 사항
마이그레이션 유형으로 증분 마이그레이션을 선택하는 경우 다음 조건을 확인해야 합니다. 그렇지 않으면 확인이 실패합니다.
- 원본 및 대상 데이터베이스의 주요 버전은 PostgreSQL 10.x 미만이어야 합니다.
- 원본 데이터베이스의 ‘wal_level’은 ‘logical’로 설정되어야 합니다.
- 대상 데이터베이스의 ‘max_replication_slots’ 및 ‘max_wal_senders’ 값은 마이그레이션할 총 데이터베이스 수보다 커야 합니다.
- 대상 데이터베이스의 ‘max_worker_processes’ 값은 ‘max_logical_replication_workers’ 값보다 커야 합니다.
- 마이그레이션할 테이블에는 unlogged table이 포함되어서는 안 됩니다. 그렇지 않으면 마이그레이션할 수 없습니다.

## 수정 방법
버전이 요구 사항을 충족하지 않으면 업그레이드해야 합니다. ‘wal_level’, ‘max_replication_slots’, ‘max_worker_processes’ 및 ‘max_wal_senders’ 값을 다음과 같이 변경할 수 있습니다.

1. 원본 데이터베이스에 로그인합니다.
>?
>- 원본 데이터베이스가 자체 구축된 경우 데이터베이스가 실행되는 서버에 로그인하고 데이터베이스의 기본 데이터 디렉터리(일반적으로 $PGDATA)를 입력해야 합니다.
>- 원본 데이터베이스가 다른 클라우드에 있는 경우 해당 클라우드 공급업체의 요청에 따라 매개변수를 수정합니다.
>- 대상 데이터베이스에서 매개변수를 수정해야 하는 경우 지원을 위해 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하십시오.
2. postgresql.conf 파일을 열고 ‘wal_level’을 수정합니다.
```
wal_level = logical
```
3. 수정이 완료되면 데이터베이스를 다시 시작합니다.
4. 데이터베이스에 로그인하고 다음 명령을 실행하여 매개변수가 올바르게 설정되었는지 확인합니다.
```
postgres=> select name,setting from pg_settings where name='wal_level';
   name    | setting 
-----------+---------
 wal_level | logical
(1 row)
postgres=> select name,setting from pg_settings where name='max_replication_slots';
         name          | setting 
-----------------------+---------
 max_replication_slots | 10
(1 row)
postgres=> select name,setting from pg_settings where name='max_wal_senders';
      name       | setting 
-----------------+---------
 max_wal_senders | 10
(1 row)
```
5. 확인 작업을 다시 실행합니다.

