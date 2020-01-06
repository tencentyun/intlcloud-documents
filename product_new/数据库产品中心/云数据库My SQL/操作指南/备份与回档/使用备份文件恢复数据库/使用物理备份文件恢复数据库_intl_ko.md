## 작업 시나리오
 이 파일은 로컬에 다운로드한 물리 백업 파일을 기타 호스트에서 데이터베이스를 복구하는 방법을 소개드립니다. 

## 조작 프로세스
### 백업 파일 다운로드
상세 프로세스는 [백업 다운로드](https://intl.cloud.tencent.com/document/product/236/7274)를 참조하십시오.

### 백업 파일 압축 해제
1. 백업 파일은 우선 qpress를 압축하고나서 xbstream을 통해 패킹합니다(xbstream은 Percona의 패킹/압축 해제 툴입니다). 관련하여 백업 파일을 다운로드하면 우선 xbstream으로 압축 해제해야 합니다. xbstream툴은 Percona XtraBackup 홈페이지에서 다운로드하거나 직접 이진법 패킷을 다운로드할 수 있습니다.
 - [Percona XtraBackup 홈페이지 다운로드/설치](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)
 Percona XtraBackup 2.4.6 및 이상 버전을 선택하십시오. 설치 설명은 [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)를 참조하십시오.
 -이진법 패킷 설치
[XtraBackup-download](https://www.percona.com/downloads/Percona-XtraBackup-2.4/Percona-XtraBackup-2.4.13/binary/tarball/percona-xtrabackup-2.4.13-Linux-x86_64.libgcrypt145.tar.gz)을 통해 대응하는 조작시스템 버전의 XtraBackup 이진법 패킷을 다운로드합니다.
>기존 Windows 조작시스템은 XtraBackup툴을 지원하지 않습니다. 오직 Linux 조작시스템만 XtraBackup툴을 지원합니다.
2. XtraBackup을 설치 완료하면 xbstream 커맨드를 적용하여 백업 파일을 목표 디렉터리에 압축 해제합니다. 
```
xbstream -x -C /data < ~/test.xb
```
패킷 압축 해제 결과는 하기 스샷을 참조하십시오.
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

### 백업 파일 압축 해제
백업 파일은 quicklz 알고리즘을 통해 압축되었으므로, 압축을 해제해야 합니다. [qpress 툴 다운로드](http://www.quicklz.com/)해야 하며, 다운로드를 완료하면 다음 커맨드를 적용하여 qpress 이진법 파일을 압축 해제해야 합니다.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
qpress 커맨드를 적용하여 목표 디렉터리의 전체 `.qp` 앤딩 파일을 압축 해제합니다.
```
xtrabackup --decompress --target-dir=/data
```
>
>- `xtrabackup --decompress`는 qpress 툴을 호출합니다. `--decompress` 파라미터를 사용하기 전에 qpress를 설치해야 합니다.
>- Percona Xtrabackup는 2.4.6 및 이상 버전에서만 `--remove-original` 옵션을 지원합니다.
>- ‘trabackup’는 기본적으로 압축 해제 시에 오리지널 압축 파일을 삭제하지 않습니다. 혹 압축 해제 완료후에 오리지널 압축 파일을 삭제하려면, 위 커맨드에 `--remove-original` 파라미터를 추가할 수 있습니다.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

### 백업 파일 Prepare
백업을 압축 해제하면, 다음 커맨드를 실행하여 apply log를 조작해야 합니다.
```
xtrabackup --prepare  --target-dir=/data
```
실행 시 출력 결과에 다음 사항을 포함하면 prepare 성공함을 뜻합니다.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	

### 설정 파일 수정
버전상 문제로 압축 해제 파일 backup-my.cnf에서 다음 파라미터를 노트(note)하십시오.
- innodb_checksum_algorithm
- innodb_log_checksum_algorithm
- innodb_fast_checksum
- innodb_page_size 
- innodb_log_block_size
- redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 파일 옵션 수정
파일 옵션을 수정 및 파일은 mysql 사용자 소유인지 체크합니다.
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### mysqld 스레드 기동 및 로그인 검증
1. mysqld 스레드를 작동합니다.
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. 클라이언트에 로그인하여 mysql 검증합니다.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

>
>- 복구 완료 시, mysql.user 테이블은 TencentDB에 생성한 사용자를 포함하지 않으며, 새롭게 구축해야 합니다.
>- 신규 사용자를 생성하기 전에 다음 SQL를 실행하십시오.
```
delete from mysql.db where user<>'root' and char_length(user)>0;
delete from mysql.tables_priv where user<>'root' and char_length(user)>0;
flush privileges;
```
