
## 작업 시나리오
>?스토리지 용량을 절약하기 위해 TencentDB for MySQL의 물리 백업과 로직 백업 파일은 먼저 qpress 압축을 거친 다음 xbstream(Percona의 패킹/언패킹 툴)으로 압축 및 패킹(Packing)합니다.
>
오픈 소스 소프트웨어 Percona Xtrabackup은 데이터베이스 백업 복구 시 사용합니다. 본 문서는 XtraBackup 툴을 이용해 MySQL 물리 백업 파일을 다른 호스트에 있는 자체구축 데이터베이스에 복구하는 방법을 소개합니다.
- XtraBackup은 Linux 플랫폼만 지원하며, Windows 플랫폼은 지원하지 않습니다.
- Windows 플랫폼의 데이터 복구는 [TCCLI로 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/236/8464)을 참조하십시오.


## 전제 조건
- XtraBackup 툴을 다운로드 및 설치합니다.
다운로드는 [Percona XtraBackup 공식 홈페이지](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)에서 가능하며, Percona XtraBackup 2.4.6 이상의 버전을 선택하여 다운로드하십시오. 설치에 대한 자세한 내용은 [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)를 참조하십시오.
- 지원하는 인스턴스 버전: MySQL 이중 노드, 3중 노드
- 데이터 암호화 기능을 활성화한 인스턴스는 물리 백업으로 데이터베이스를 복구할 수 없습니다.

## 작업 순서
>?본 문서는 CentOS 운영 체제의 CVM과 MySQL 5.7 버전을 예로 들어 소개합니다.
>
### 1단계: 백업 파일 다운로드
콘솔에서 TencentDB for MySQL의 데이터 백업 및 로그 백업을 다운로드할 수 있습니다.
>?한 IP당 링크는 기본 10개로 제한되어 있으며, 각 링크의 다운로드 속도는 20Mpbs~30Mpbs입니다.
>
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, 인스턴스 리스트에서 인스턴스 이름 또는 '작업' 열의 [관리]를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 [백업 복구]>[데이터 백업 리스트]로 이동한 후, 다운로드하려는 백업을 선택하고 '작업' 열의 [다운로드]를 클릭합니다.
3. 팝업된 대화 상자에서 권장한 다운로드 주소를 복사하고 [CDB가 속한 VPC의 CVM(Linux 시스템)](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)에 로그인한 후, wget 명령어로 내부 네트워크 고속 다운로드를 사용하면 보다 효율적입니다.
>?
>- [로컬 다운로드]를 선택하여 직접 다운로드할 수도 있으나 다소 긴 시간이 소요될 수 있습니다.
>- wget 명령어 포맷: wget -c '백업 파일 다운로드 주소' -O 사용자 정의 파일명.xb 
>
예시는 다음과 같습니다.
```
wget -c 'https://mysql-database-backup-sh-1218.cos.ap-nanjing.myqcloud.com/12427%2Fmysql%2F0674-ffba-11e9-b592-70bd%2Fdata%2Fautomatic-delete%2F2019-12-03%2Fautomatic%2Fxtrabackup%2Fbk_61_156758150%2Fcdb-293fl9ya_backup_20191203000202.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3DAKzxfbLJ1%26q-sign-time%3D1575374119%3B1575417319%26q-key-time%3D1575374119%3B1575417319%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dba959757&response-content-disposition=attachment%3Bfilename%3D%22yuan177685_backup_20191203000202.xb%22&response-content-type=application%2Foctet-stream' -O ~/test.xb
```

### 2단계: 데이터 복구
#### 2.1 백업 파일 언패킹
xbstream 명령어를 사용해 백업 파일을 타깃 디렉터리에 언패킹합니다.
```
xbstream -x -C /data < ~/test.xb
```
>?
>- 본 문서의 타깃 디렉터리는 `/data`이며, 실제 상황에 따라 경로를 선택할 수 있습니다.
>- `~/test.xb`를 백업 파일로 변경합니다.
>
언패킹(Unpacking) 결과는 아래 이미지와 같습니다.
![extract.png](https://main.qcloudimg.com/raw/ed2ffc8b81df11040559ceda59427a3e.png)

#### 2.2 백업 파일 압축 해제
1. 다음 명령어를 사용해 qpress 툴을 다운로드합니다.
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?wget 다운로드 시 오류 알림이 뜬다면 [quicklz](http://www.quicklz.com/)에서 qpress 툴을 로컬에 다운로드한 후 다시 Linux CVM에 업로드하시기 바랍니다. 자세한 내용은 [SCP로 Linux CVM에 파일 업로드하기](https://intl.cloud.tencent.com/zh/document/product/213/2133)를 참조하십시오.
2. 다음 명령어를 사용해 qpress 바이너리 파일을 압축 해제합니다.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. 다음 명령어를 사용해 타깃 디렉터리에서 `.qp`로 끝나는 모든 파일을 압축 해제합니다.
```
xtrabackup --decompress --target-dir=/data
```
>?
>- `/data`는 이전에 저장한 백업 파일의 타깃 디렉터리로, 실제 상황에 따라 경로를 선택할 수 있습니다.
>- Percona Xtrabackup은 2.4.6 이상 버전에서만 `--remove-original` 옵션을 지원합니다.
>- `xtrabackup`은 압축 해제 시 원본 압축 파일을 삭제하지 않도록 기본 설정되어 있습니다. 압축 해제 후에 원본 압축 파일을 삭제하려면, 위 명령어에 `--remove-original` 매개변수를 추가하십시오.
>
![decompress.png](https://main.qcloudimg.com/raw/886e5463ffff0656ffe06d73ffbeb211.png)

#### 2.3 Prepare 백업 파일
백업을 압축 해제한 후 다음 명령어를 실행하여 apply log 작업을 하십시오.
```
xtrabackup --prepare  --target-dir=/data
```
실행 후 출력 결과에 다음 사항이 포함되어 있다면 prepare 성공을 뜻합니다.
![prepare.png](https://main.qcloudimg.com/raw/13c768fd980f99d7f5824e8f28100950.png)
	
	
#### 2.4 구성 파일 수정
1. 다음 명령어를 실행하여 `backup-my.cnf` 파일을 엽니다.
```
vi /data/backup-my.cnf
```
>?본 문서는 타깃 디렉터리 `/data`를 예로 들며, 실제 상황에 따라 경로를 변경할 수 있습니다.
>
2. 버전 관련 문제가 있으므로 압축 해제 파일 `backup-my.cnf`에서 다음 매개변수에 주석을 추가합니다.
 - innodb_checksum_algorithm
 - innodb_log_checksum_algorithm
 - innodb_fast_checksum
 - innodb_page_size 
 - innodb_log_block_size
 - redo_log_version 

![](https://mc.qcloudimg.com/static/img/10113311b33e398ce0df96ca419f7f45/3.png)

### 2.5 파일 속성 수정
파일 속성을 수정하고 mysql 사용자 소속 여부를 확인합니다.
```
chown -R mysql:mysql /data
```
![](https://mc.qcloudimg.com/static/img/efbdeb20e1b699295c6a4321943908b2/4.png)

### 3단계: mysqld 프로세스 실행 및 로그인 인증
1. mysqld 프로세스를 실행합니다.
```
mysqld_safe --defaults-file=/data/backup-my.cnf --user=mysql --datadir=/data &
```
2. 클라이언트에 로그인하여 mysql 인증을 진행합니다.
```
mysql  -uroot
```
![](https://main.qcloudimg.com/raw/c95419569318a928c0f71978fbb8c6ad.png)

## 백업 관련 문제
[백업 FAQ](https://intl.cloud.tencent.com/document/product/236/9036) 및 [백업 실패 원인](https://intl.cloud.tencent.com/document/product/236/34394)을 참조하십시오.


