## 작업 시나리오
>?스토리지 용량을 절약하기 위해 TencentDB for MySQL의 물리 백업과 로직 백업 파일은 먼저 qpress 압축을 거친 다음 xbstream(Percona의 패킹/언패킹 툴)으로 압축 및 패킹(Packing)합니다.
>
오픈 소스 소프트웨어 Percona Xtrabackup은 데이터베이스의 백업 복구 시에 사용됩니다. 본 문서는 XtraBackup 툴로 MySQL 로직 백업 파일을 다른 호스트에 있는 자체 구축 데이터베이스에 복구하는 방법에 관해 소개합니다.
- XtraBackup은 Linux 플랫폼에서만 지원되며, Windows 플랫폼은 지원하지 않습니다.
- Windows 플랫폼의 데이터 복구는 [TCCLI로 데이터 마이그레이션](https://intl.cloud.tencent.com/document/product/236/8464)을 참조 바랍니다.

## 전제 조건
- XtraBackup 툴을 다운로드 및 설치합니다.
  다운로드 주소는 [Percona XtraBackup 공식 홈페이지](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)를 이용 바라며, Percona XtraBackup 2.4.6 및 그 이상의 버전을 선택하시기 바랍니다. 설치에 대한 자세한 내용은 [Percona XtraBackup 2.4](https://www.percona.com/doc/percona-xtrabackup/2.4/installation.html?spm=a2c4g.11186623.2.14.4d8653a6QmHkgI)를 참조 바랍니다.
- 지원하는 인스턴스 버전: MySQL 고가용성 버전과 파이낸스 버전.

## 작업 순서
### 1단계: 백업 파일 다운로드
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 명칭 혹은 'Operation' 열의 [Manage]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. 인스턴스 관리 웹페이지에서 [Backup and Restore]>[Data Backup List] 페이지를 선택하고, 다운로드하려는 백업을 선택하여 'Operation' 열의 [Download]를 클릭합니다.
3. 팝업된 대화 상자에서 권장한 대로 다운로드 주소를 복제하고, [CDB가 속한 VPC의 CVM(Linux 시스템)에 로그인](https://intl.cloud.tencent.com/zh/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)하여 wget 명령어로 내부 네트워크 고속 다운로드를 사용하면 더욱더 효율적입니다.
>?
>- 또한 [로컬 다운로드]를 선택하여 직접 다운로드할 수 있지만, 다소 긴 시간이 소요될 수 있습니다.
>- wget 명령어 형식: wget -c '백업 파일 다운로드 주소' -O 사용자 정의 파일 이름.xb
>
예시는 다음과 같습니다.
```
wget -c 'https://mysql-database-backup-bj-118.cos.ap-beijing.myqcloud.com/12427%2Fmysql%2F42d-11ea-b887-6c0b82b%2Fdata%2Fautomatic-delete%2F2019-11-28%2Fautomatic%2Fxtrabackup%2Fbk_204_10385%2Fcdb-1pe7bexs_backup_20191128044644.xb?sign=q-sign-algorithm%3Dsha1%26q-ak%3D1%26q-sign-time%3D1574269%3B1575417469%26q-key-time%3D1575374269%3B1517469%26q-header-list%3D%26q-url-param-list%3D%26q-signature%3Dfb8fad13c4ed&response-content-disposition=attachment%3Bfilename%3D%2141731_backup_20191128044644.xb%22&response-content-type=application%2Foctet-stream' -O test0.xb
```

### 2단계: 백업 파일 언패킹
xbstream을 사용해 백업 파일을 언패킹합니다.
```
xbstream -x < test0.xb
```
>?`test0.xb`를 백업 파일로 변경합니다.
>
언패킹(Unpacking) 결과는 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/61b53f4f54ffd2fbe7c0d1b3423255b0.png)

### 3단계: 백업 파일 압축 해제
1. 다음 명령어를 사용해 qpress 툴을 다운로드합니다.
```
wget http://www.quicklz.com/qpress-11-linux-x64.tar
```
>?wget 다운로드 시 오류 알림이 뜬다면 [quicklz](http://www.quicklz.com/)에서 qpress 툴을 로컬에 다운로드한 후 qpress 툴을 다시 Linux CVM에 업로드하시기 바랍니다. 자세한 내용은 [SCP로 파일을 Linux CVM에 업로드](https://intl.cloud.tencent.com/document/product/213/2133)를 참조 바랍니다.
2. 다음 명령어를 사용해 qpress를 이진법 파일로 압축 해제합니다.
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. qpress로 백업 파일을 압축 해제합니다.
```
qpress -d cdb-jp0zua5k_backup_20191202182218.sql.qp .
```
>?압축 해제 시간을 참고하여 확장자가 `.sql.qp`인 백업 파일을 찾은 다음, `cdb-jp0zua5k_backup_20191202182218`을 해당하는 파일 이름으로 변경합니다.
>
압축 해제 결과는 아래 이미지와 같습니다.
![](https://main.qcloudimg.com/raw/355557bc949fd86af8346d8a44dc4551.png)

### 4단계: 백업을 타깃 데이터베이스로 가져오기
다음 명령어를 실행하여 sql 파일을 타깃 데이터베이스로 가져옵니다.
```
mysql -uroot -P3306 -h127.0.0.1 -p < cdb-jp0zua5k_backup_20191202182218.sql
```
>?
>- 본 문서는 MySQL의 로컬 3306 포트 가져오기를 예로 들며, 실제 상황에 따라 변경하실 수 있습니다.
>- `cdb-jp0zua5k_backup_20191202182218.sql`을 qpress를 통해 압축 해제한 실제 sql 파일로 변경합니다.
