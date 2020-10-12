### binlog 로그는 어떻게 조회하나요?
[MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, [Backup and Restore]>[Log Backup List] 페이지에서 로그를 다운로드 및 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/80e006c2d5165ecfa9ce9395d59d01f8.png)

### 데이터베이스 인스턴스에 binlog 로그가 없는 이유는 무엇인가요?
현재 binlog의 쓰기 속도가 느려 로테이션이 되지 않고 있어, 콘솔에서 표시되지 않는 것일 수 있습니다.

MySQL 콘솔에서 표시되는 binlog 로직은 아래와 같습니다.
1. binlog 쓰기가 256MB를 모두 사용하면 한 번 로테이션됩니다.
2. 로테이션 된 binlog 파일을 COS에 업로드합니다.
3. COS에 업로드한 binlog 파일이 콘솔에서 표시됩니다.
위 세 가지 단계를 완료하기까지 약 3분 정도 소요됩니다.

데이터베이스에 로그인하고 `flush logs` 명령어를 실행하면 약 3분 후에는 콘솔에서 binlog 로그를 조회할 수 있습니다.

### 최신 binlog 로그는 어떻게 조회하나요?
데이터베이스에 로그인하고 `flush logs` 명령어를 실행하면 약 3분 후에는 콘솔에서 binlog 로그를 조회할 수 있습니다.

### binlog 로그는 어떻게 백업하나요? 
binlog 로그 시스템은 매일 자동으로 백업되며, 콘솔의 [Backup and Restore]>[Log Backup List] 페이지에서 로그 백업의 보관 시간을 설정할 수 있습니다.

