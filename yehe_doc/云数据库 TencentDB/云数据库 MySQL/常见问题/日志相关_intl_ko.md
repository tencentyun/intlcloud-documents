### binlog 로그는 어떻게 조회하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 후, [Backup and Restore] > [Log Backup List] 페이지에서 로그를 조회하고 다운로드할 수 있습니다.
![](https://main.qcloudimg.com/raw/b411a99afeae2858ae578696ad9d66af.png)

### 데이터베이스 인스턴스에 왜 binlog 로그가 없나요?
현재 binlog 쓰기 속도가 비교적 느리기 때문일 수 있으며, 한 번도 잘라내지 않아 콘솔에 나타나지 않을 수 있습니다.

MySQL 콘솔에 binlog를 보여주는 로직은 다음과 같습니다.
1. binlog가 256MB가 되면 한 번 잘라냅니다.
2. 잘라낸 binlog 파일을 COS에 업로드합니다.
3. COS에 업로드한 binlog 파일이 콘솔에 나타납니다.
상기 3단계 절차에는 약 3분이 소요됩니다.

데이터베이스에 로그인하여 `flush logs` 명령을 실행하면 약 3분 후 콘솔에서 binlog 로그를 조회할 수 있습니다.

### 최신 binlog 로그를 조회하려면 어떻게 해야 하나요?
데이터베이스에 로그인하여 `flush logs` 명령을 실행하면 약 3분 후 콘솔에서 binlog 로그를 조회할 수 있습니다.

### binlog 로그는 어떻게 백업하나요? 
binlog 로그 시스템은 매일 자동으로 백업되며, 콘솔의 [Backup and Restore] > [Log Backup List] 페이지에서 로그 백업 보관 기간을 설정할 수 있습니다.

