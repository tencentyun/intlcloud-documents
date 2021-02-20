내/외부 네트워크로 MySQL 인스턴스에 정상적으로 액세스할 수 없는 경우, 연결 진단 툴로 내/외부 네트워크의 액세스 문제를 간편하게 진단할 수 있습니다.

### 내부 네트워크 연결 진단
CVM으로 MySQL 인스턴스 액세스 시 오류가 발생한 경우, MySQL 콘솔이 제공하는 연결 진단 툴로 내부 네트워크의 연결 관련 문제를 진단할 수 있습니다. 간단한 방법으로 내부 네트워크의 연결 장애 문제를 해결할 수 있습니다.
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 진단이 필요한 MySQL 인스턴스를 선택하고, 인스턴스 이름을 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. 인스턴스 관리 페이지에서 [Connection Check] 페이지를 선택합니다.
3. 내부 네트워크 연결 문제를 진단하는 경우, [Add CVMs that can Access this instance]를 클릭하여 MySQL 인스턴스를 액세스하는 CVM 인스턴스를 추가합니다.
>?CVM 인스턴스 선택 시, 동일 리전 내 CVM에 한해 디폴트로 설정됩니다. 리전 간 액세스하는 경우, [피어링 연결](https://intl.cloud.tencent.com/document/product/553)로 네트워크를 연결합니다.
>
![](https://main.qcloudimg.com/raw/e233a1cd63718cfdc31347da83153fd8.png)
3. 추가한 뒤 [Start Check]을 클릭합니다. 진단이 종료되면 진단 보고서가 생성됩니다.
![](https://main.qcloudimg.com/raw/0788aebb88c5509288e378dc1f541f22.png)
4. 진단 보고서의 상태열에서 [View Report]를 클릭하면 진단 결과를 조회할 수 있습니다.
 - 진단 상태가 [정상]인 경우, CVM 인스턴스가 내부 네트워크로 해당 MySQL 인스턴스에 정상 액세스하는 것을 허용했다는 뜻입니다.
 - 진단 상태가 [오류]인 경우, CVM 인스턴스가 내부 네트워크로 해당 MySQL 인스턴스에 정상 액세스하는 것을 거부했다는 뜻입니다. 오류 진단 항목의 [처리 권장 사항]을 참조하여 설정하십시오. 이외의 내부 네트워크 액세스 관련 문제는 [인스턴스 연결 장애](https://intl.cloud.tencent.com/document/product/236/31928)를 참조하십시오.
![](https://main.qcloudimg.com/raw/b183b27af9c6b5a28cdb708f8a5c44d8.png)

### 외부 네트워크 연결 진단
외부 네트워크 서버로 MySQL 인스턴스 액세스 시 오류가 발생한 경우, MySQL 콘솔이 제공하는 연결 진단 툴로 외부 네트워크의 연결 관련 문제를 진단할 수 있습니다. 간단한 방법으로 외부 네트워크의 연결 장애 문제를 해결할 수 있습니다.

1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 진단이 필요한 MySQL 인스턴스를 선택하고, 인스턴스 이름을 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. 인스턴스 관리 페이지에서 [Connection check]>[Public Network Check]를 선택합니다.
3. 외부 네트워크 연결 문제를 검사하려면 [Add an external server to access this instance]를 클릭해 해당 MySQL 인스턴스에 액세스할 외부 네트워크 서버를 추가해야 합니다.
4. 추가를 완료하면 [Start check]를 클릭합니다. 검사가 완료되면 검사 보고가 생성됩니다.
![](https://main.qcloudimg.com/raw/43d9e61c2052797740e7ef6817251f5e.png)
5. 검사 보고의 상태 열에서 [View Report]를 클릭하면 검사 결과를 확인할 수 있습니다.
 - 진단 상태가 [정상]인 경우, 외부 네트워크 서버가 외부 네트워크로 해당 MySQL 인스턴스에 정상 액세스하는 것을 허용했다는 뜻입니다.
 - 진단 상태가 [오류]인 경우, 외부 네트워크 서버가 외부 네트워크로 해당 MySQL 인스턴스에 정상 액세스하는 것을 거부했다는 뜻입니다. 오류 진단 항목의 [처리 권장 사항]을 참조하여 설정하십시오. 이외의 외부 네트워크 액세스 관련 문제는 [인스턴스 연결 장애](https://intl.cloud.tencent.com/document/product/236/31928)를 참조하십시오.
![](https://main.qcloudimg.com/raw/01998fb06fe6d8a762dd5a2a9a5eb26c.png)
