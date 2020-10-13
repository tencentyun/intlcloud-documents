내부/외부 네트워크를 통해 MySQL 인스턴스에 정상적으로 액세스할 수 없을 경우, 연결 검사 툴을 사용하면 내부/외부 네트워크 연결 문제를 간단히 진단할 수 있습니다.

### 내부 네트워크 연결 검사
CVM을 통해 MySQL 인스턴스에 연결하는 과정에서 액세스 오류 문제가 발생할 경우, MySQL 콘솔에서 제공하는 연결 검사 툴을 사용하면 내부 네트워크 연결 문제를 진단할 수 있어, 간단한 조작만으로 내부 네트워크로 연결할 수 없는 문제를 쉽게 해결할 수 있습니다.
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 진단할 MySQL 인스턴스를 선택하고 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 [Connection check]를 선택합니다.
3. 내부 네트워크 연결 문제를 검사하려면 [Add CVMs that can access this instance]를 클릭해 해당 MySQL 인스턴스에 액세스할 CVM 인스턴스를 추가해야 합니다.
>?CVM 인스턴스 선택 시 같은 리전 내의 CVM만 기본 제공되므로, 리전 간 액세스가 필요하다면 [피어링 연결](https://intl.cloud.tencent.com/document/product/553)을 통해 네트워크를 연결하시기 바랍니다.
>
![](https://main.qcloudimg.com/raw/e233a1cd63718cfdc31347da83153fd8.png)
3. 추가를 완료하면 [Start check]를 클릭합니다. 검사가 완료되면 검사 보고가 생성됩니다.
![](https://main.qcloudimg.com/raw/0788aebb88c5509288e378dc1f541f22.png)
4. 검사 보고의 상태 열에서 [View Report]를 클릭하면 검사 결과를 확인할 수 있습니다.
 - 검사 상태가 [Normal]이면 CVM 인스턴스가 내부 네트워크를 통해 MySQL 인스턴스에 정상적으로 액세스할 수 있음을 의미합니다.
 - 검사 상태가 [Abnormal]이면 CVM 인스턴스가 내부 네트워크를 통해 MySQL 인스턴스에 정상적으로 액세스할 수 없음을 의미합니다. 비정상 항목의 [처리 제안]을 참조하여 설정하시고, 내부 네트워크 액세스에 대한 더 많은 문제는 [인스턴스에 연결할 수 없는 문제](https://intl.cloud.tencent.com/document/product/236/31928)를 참조 바랍니다.
![](https://main.qcloudimg.com/raw/b183b27af9c6b5a28cdb708f8a5c44d8.png)

### 외부 네트워크 연결 검사
외부 네트워크 서버를 통해 MySQL 인스턴스에 연결하는 과정에서 액세스 오류 문제가 발생할 경우, MySQL 콘솔에서 제공하는 연결 검사 툴을 사용하면 외부 네트워크 연결 문제를 진단할 수 있어 간단한 조작만으로 외부 네트워크로 연결할 수 없는 문제를 쉽게 해결할 수 있습니다.

1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 진단할 MySQL 인스턴스를 선택하고 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 [Connection check]>[Public Network Check]를 선택합니다.
3. 외부 네트워크 연결 문제를 검사하려면 [Add an external server to access this instance]를 클릭해 해당 MySQL 인스턴스에 액세스할 외부 네트워크 서버를 추가해야 합니다.
4. 추가를 완료하면 [Start check]를 클릭합니다. 검사가 완료되면 검사 보고가 생성됩니다.
![](https://main.qcloudimg.com/raw/43d9e61c2052797740e7ef6817251f5e.png)
5. 검사 보고의 상태 열에서 [View Report]를 클릭하면 검사 결과를 확인할 수 있습니다.
 - 검사 상태가 [Normal]이면 외부 네트워크 서버가 내부 네트워크를 통해 MySQL 인스턴스에 정상적으로 액세스할 수 있음을 의미합니다.
 - 검사 상태가 [Abnormal]이면 외부 네트워크 서버가 내부 네트워크를 통해 MySQL 인스턴스에 정상적으로 액세스할 수 없음을 의미합니다. 비정상 항목의 [처리 제안]을 참조하여 설정하시고, 외부 네트워크 액세스에 대한 더 많은 문제는 [인스턴스에 연결할 수 없는 문제](https://intl.cloud.tencent.com/document/product/236/31928)를 참조 바랍니다.
![](https://main.qcloudimg.com/raw/01998fb06fe6d8a762dd5a2a9a5eb26c.png)
