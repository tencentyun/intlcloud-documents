## 작업 시나리오

PostgreSQL은 확장성과 표준 준수에 중점을 둔 오픈 소스 관계형 데이터베이스 관리 시스템입니다. PostgreSQL은 엔터프라이즈 수준의 복잡한 온라인 트랜잭션 처리(OLTP) 시스템에 이상적입니다. NoSQL(JSON/XML/hstore) 및 지리 정보 시스템(GIS, Geographic Information System 또는 Geo－Information system) 데이터 유형을 지원합니다. 강력한 안정성과 데이터 무결성을 특징으로 하는 PostgreSQL은 웹사이트, 위치 애플리케이션 시스템, 복잡한 데이터 객체 처리 및 기타 사용 사례에 적합합니다.

본 문서는 CentOS 7을 실행하는 CVM 인스턴스에서 PostgreSQL 시스템을 구축하는 방법을 설명합니다.

## 소프트웨어
본 문서는 PostgreSQL을 구축하기 위해 다음 소프트웨어를 예로 사용합니다.
- Linux: Linux 운영 체제의 경우, 본 문서는 CentOS 7.6을 예시로 사용합니다.
- PostgreSQL: 관계형 데이터베이스 관리 시스템. 본 문서에서는 PostgreSQL 12을 예시로 사용합니다.


## 전제 조건
- 두 개의 CVM 인스턴스가 생성되어 있어야 합니다. 하나의 CVM 인스턴스는 기본 노드로 작동하고 다른 하나는 보조 노드로 작동합니다.
구체적인 단계는 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.
- 두 CVM 인스턴스에 보안 그룹 규칙(5432 포트 개방)이 설정되어있어야 합니다.
구체적인 단계는 [보안 그룹 규칙 추가](https://intl.cloud.tencent.com/document/product/213/34272)를 참고하십시오.

## 작업 단계

### 프라이머리 노드 설정

1. 프라이머리 노드 인스턴스에 로그인합니다.
2. 다음 명령을 실행하여 모든 패키지, 시스템 버전 및 커널을 업그레이드합니다.
```
yum update -y
```
3. 다음 명령어를 순서대로 실행하여 PostgreSQL을 설치합니다.
본 문서에서는 PostgreSQL 버전 12을 예시로 사용하며 필요에 따라 다른 버전을 선택할 수 있습니다.
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql12-server postgresql12-contrib -y
```
```
/usr/pgsql-12/bin/postgresql12-setup initdb
```
4. 아래의 명령어를 실행하여 서비스를 시작하십시오.
```
systemctl start postgresql-12.service
```
5. 다음 명령을 실행하여 시작 시 서비스가 자동으로 실행되도록 설정합니다.
```
systemctl enable postgresql-12.service 
```
6. 다음 명령을 실행하여 postgres 사용자로 로그인합니다.
```
su - postgres
```
7. 다음 명령을 실행하여 PostgreSQL 인터랙티브 터미널로 이동합니다.
```
psql
```
8. 다음 명령을 실행하여 보안성 향상을 위해 사용자 postgres의 비밀번호를 설정합니다.
```
ALTER USER postgres WITH PASSWORD '사용자 정의 비밀번호';
```
9. 다음 명령어를 실행하여 데이터베이스 계정을 생성하고 비밀번호, 로그인 권한, 백업 권한을 설정합니다.
```
create role 계정 이름 login replication encrypted password '사용자 정의 비밀번호';
```
본 문에서는 데이터베이스 계정 'replica'와 비밀번호 '123456'을 생성하는 것을 예로 들어 다음 명령을 실행합니다.
```
create role replica login replication encrypted password '123456';
```
10. 다음 명령어를 실행하여 계정이 성공적으로 생성되었는지 쿼리합니다.
```
SELECT usename from pg_user;
```
다음 결과가 반환되면 생성이 완료된 것입니다.
```
usename  
----------
postgres
replica
(2 rows)
```
11. 다음 명령어를 실행하여 권한이 성공적으로 생성되었는지 쿼리합니다.
```
SELECT rolname from pg_roles;
```
다음 결과가 반환되면 생성이 완료된 것입니다.
```
rolname      
-------------------
pg_signal_backend
postgres
replica
(3 rows)
```
12. **\q**를 입력하고 **Enter**를 눌러 SQL 터미널을 종료합니다.
13. **exit**를 입력하고 **Enter**를 눌러 PostgreSQL을 종료합니다.
14. 다음 명령을 실행하여 `pg_hba.conf` 구성 파일을 열고 `replica` 사용자 얼로우리스트를 설정합니다.
```
vim /var/lib/pgsql/12/data/pg_hba.conf
```
15. **i**를 눌러 편집 모드로 전환하고 'IPv4 local connections' 섹션에 다음 두 줄의 내용을 추가합니다.
```
host    all             all             <세컨더리 노드의 VPC IPv4 IP 대역>          md5     #VPC IP 대역에서 md5 비밀번호 인증 연결 허용
host    replication     replica         <세컨더리 노드의 VPC IPv4 IP 대역>          md5     #사용자가 replication 데이터베이스에서 데이터 동기화 허용
```
예를 들어 데이터베이스 계정이 'replica'이고 세컨더리 노드의 VPC IPv4 IP 대역이 'xx.xx.xx.xx/16'인 경우 'IPv4 local connections' 섹션에 다음 콘텐츠를 추가합니다.
```
host    all             all             xx.xx.xx.xx/16         md5
host    replication     replica         xx.xx.xx.xx/16         md5
```
16. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
17. 다음 명령어를 실행하여 `postgresql.conf` 파일을 엽니다.
```
vim /var/lib/pgsql/12/data/postgresql.conf
```
18. **i**를 눌러 편집 모드로 이동하고 다음 매개변수를 각각 찾은 다음 매개변수를 다음 콘텐츠로 수정합니다.
```
listen_addresses = '*'   #수신되는 내부 IP 주소
max_connections = 100 #최대 연결 수, 세컨더리 데이터베이스의 max_connections는 프라이머리 데이터베이스의 max_connections보다 커야 함
wal_level = hot_standby  #핫 백업 모드 활성화
synchronous_commit = on  #동기화 복사 활성화
max_wal_senders = 32     #동기화할 최대 프로세스 수
wal_sender_timeout = 60s #스트리밍 복사 호스트가 데이터를 보내는 시간 초과 시간
```
19. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
20. 아래의 명령어를 실행하여 서비스를 재시작합니다.
```
systemctl restart postgresql-12.service
```

### 세컨더리 노드 설정

1. 세컨더리 노드 인스턴스에 로그인합니다.
2. 다음 명령을 실행하여 모든 패키지, 시스템 버전 및 커널을 업그레이드합니다.
```
yum update -y
```
3. 다음 명령어를 순서대로 실행하여 PostgreSQL을 설치합니다.
```
wget --no-check-certificate https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
```
rpm -ivh pgdg-redhat-repo-latest.noarch.rpm
```
```
yum install postgresql12-server postgresql12-contrib -y
```
4. 다음 명령을 실행하여 pg_basebackup 기본 백업 툴을 사용하여 백업 디렉터리를 지정합니다.
```
pg_basebackup -D /var/lib/pgsql/12/data -h <프라이머리 노드 공용 IP> -p 5432 -U replica -X stream -P
```
다음 지시에 따라 데이터베이스 계정에 해당하는 비밀번호를 입력하고 **Enter**를 누릅니다. 다음 결과가 반환되면 백업이 성공한 것입니다.
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
5. 다음 명령을 실행하여 master 설정 파일을 복사합니다.
```
cp /usr/pgsql-12/share/recovery.conf.sample /var/lib/pgsql/12/data/recovery.conf
```
6. 다음 명령어를 실행하여 `recovery.conf` 파일을 엽니다.
```
vim /var/lib/pgsql/12/data/recovery.conf
```
7. **i**를 눌러 편집 모드로 전환하고 각각 다음 매개변수를 찾아 다음 콘텐츠와 같이 수정합니다.
```
standby_mode = on     #이 노드를 세컨더리 데이터베이스로 성명
primary_conninfo = 'host=<프라이머리 노드 공용 IP> port=5432 user=데이터베이스 계정 password=데이터베이스 비밀번호' #해당 프라이머리 데이터베이스의 연결 정보
recovery_target_timeline = 'latest' #스트림 복사를 최신 데이터와 동기화
```
8. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
9. 다음 명령어를 실행하여 `postgresql.conf` 파일을 엽니다.
```
vim /var/lib/pgsql/12/data/postgresql.conf
```
10. **i**를 눌러 편집 모드로 전환하고 다음 매개변수를 각각 찾아 다음과 같이 수정합니다.
```
max_connections = 1000             # 최대 연결 수, 세컨더리 데이터베이스의 max_connections는 프라이머리 데이터베이스보다 커야 함
hot_standby = on                   # 핫 백업 활성화
max_standby_streaming_delay = 30s  # 스트림 백업의 최대 딜레이 시간
wal_receiver_status_interval = 1s  # 세컨더리 노드가 프라이머리 노드에 상태를 보고하는 최대 시간 간격
hot_standby_feedback = on          # 데이터 복사에 오류가 있는 경우 프라이머리에게 피드백
```
11. **Esc**를 누르고 **:wq**를 입력하여 파일을 저장하고 뒤로 돌아갑니다.
12. 다음 명령을 실행하여 데이터 디렉터리의 그룹 및 소유자를 수정합니다.
```
chown -R postgres.postgres /var/lib/pgsql/12/data
```
13. 아래의 명령어를 실행하여 서비스를 시작하십시오.
```
systemctl start postgresql-12.service
```
14. 다음 명령을 실행하여 시작 시 서비스가 자동으로 실행되도록 설정합니다.
```
systemctl enable postgresql-12.service
```

### 배포 인증
다음을 수행하여 배포 성공 여부를 인증할 수 있습니다.
1. 다음 명령어를 실행하여 노드에서 디렉터리를 백업합니다.
```
pg_basebackup -D /var/lib/pgsql/12/data -h <프라이머리 노드 공용 IP> -p 5432 -U replica -X stream -P
```
데이터베이스 비밀번호를 입력하고 **Enter** 키를 눌러 다음 결과가 반환되면 백업이 성공한 것입니다.
```
Password: 
24526/24526 kB (100%), 1/1 tablespace
```
2. 프라이머리 노드에서 다음 명령을 실행하여 sender 프로세스를 조회합니다.
```
ps aux |grep sender
```
![](https://qcloudimg.tencent-cloud.cn/raw/bc610cf837b18158a8d0ddd89d5d87ae.png)
3. 세컨더리 노드에서 다음 명령을 실행하여 receiver 프로세스를 조회합니다.
```
ps aux |grep receiver
```
다음 결과가 반환되면 receiver 프로세스를 성공적으로 조회 가능함을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/13c908ae7d83ff8d5099f2c488b40046.png)
4. 프라이머리 노드에서 다음 명령을 순서대로 실행하여 PostgreSQL 인터랙티브 터미널로 이동하여 프라이머리 데이터베이스에서 세컨더리 데이터베이스 상태를 조회합니다.
```
su - postgres
```
```
psql
```
```
select * from pg_stat_replication;
```
다음 결과가 반환되면 세컨더리 데이터베이스 상태를 성공적으로 조회 가능함을 의미합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c38c6faf64af66188df0e944b335353a.png)

