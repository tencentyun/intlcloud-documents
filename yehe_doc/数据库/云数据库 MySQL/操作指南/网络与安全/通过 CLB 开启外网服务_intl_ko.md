TencentDB for SQL Server는 사설망 및 공중망 주소를 모두 지원하며 전자는 사설망을 통해 인스턴스에 액세스할 수 있도록 기본적으로 활성화되어 있고 후자는 필요에 따라 활성화 또는 비활성화됩니다. 공중망을 통해 Linux 또는 Windows CVM 인스턴스에서 데이터베이스 인스턴스에 액세스하려면 공중망 주소를 활성화할 수 있습니다. CLB를 통해 공중망 액세스를 활성화할 수도 있지만 이 경우 보안 그룹 규칙을 구성해야 합니다.

본문은 CLB를 통해 공중망 액세스를 활성화하고 MySQL workbench를 통해 인스턴스에 연결하는 방법을 설명합니다.

## 전제 조건
백엔드 서비스 기능 사용을 신청 완료해야 합니다.
1. [리전 간 CLB 바인딩 2.0 애플리케이션 페이지](https://cloud.tencent.com/apply/p/y72ehzwbwzk)로 이동합니다.
2. 신청서를 작성하여 제출합니다.
3. 계정에 허용되는 유형을 추가하려면 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=14&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20CLB&level3_id=1068&radio_title=%E9%85%8D%E9%A2%9D/%E7%99%BD%E5%90%8D%E5%8D%95&queue=96&scene_code=41669&step=2)하십시오.
 - CLB 및 MySQL 인스턴스가 동일한 VPC에 있는 경우: CLB_IP_VPCGW 및 CLB_IP_LB 유형을 추가합니다.
 - CLB와 MySQL 인스턴스가 서로 다른 VPC에 있는 경우: CLB_IP_User 유형을 추가합니다.

## 1단계: CLB 인스턴스 구매
>?TencentDB for MySQL과 동일한 리전에 CLB 인스턴스가 이미 있는 경우 이 단계를 건너뜁니다.
>
[CLB 구매 페이지](https://buy.cloud.tencent.com/clb)로 이동하여 구성을 선택하고 **즉시 구매**를 클릭합니다.
>!
>- 리전: TencentDB for MySQL 인스턴스가 있는 리전을 선택해야 합니다.
>- 네트워크: 동일한 VPC를 인스턴스로 선택하거나 다른 VPC를 선택할 수 있습니다.

## 2단계: CLB 인스턴스 구성
다음은 CLB 인스턴스를 데이터베이스 인스턴스와 동일한 VPC와 다른 VPC에 각각 구성하는 방법을 설명합니다.

### 시나리오1: MySQL 인스턴스와 동일한 VPC에 CLB 인스턴스 배포
1. CLB 인스턴스가 다른 사설망 IP에 바인딩될 수 있도록 교차 VPC 액세스를 활성화합니다.
a. [CLB 콘솔](https://console.cloud.tencent.com/cdb/instance)에 로그인하여 리전을 선택하고 인스턴스 목록에서 대상 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
b. **기본 정보** 페이지의 **리얼 서버** 섹션에서 **구성**을 클릭합니다.
c. 팝업 창에서 **제출**을 클릭합니다.

2.  공중망 리스너 포트를 구성합니다.
a. [CLB 콘솔](https://console.cloud.tencent.com/cdb/instance)에 로그인하여 리전을 선택하고 인스턴스 목록에서 대상 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
b. 인스턴스 관리 페이지에서 **리스너 관리** 탭을 선택하고 **TCP/UDP/TCP SSL 리스너** 아래에서 **생성**을 클릭합니다.
c. 팝업 창에서 설정을 완료하고 **제출**을 클릭합니다.

### 시나리오2: CLB 및 MySQL 인스턴스로 다른 VPC에 CLB 인스턴스 배포
1. CLB 인스턴스가 다른 사설망 IP에 바인딩될 수 있도록 교차 VPC 액세스를 활성화합니다.
a. [CLB 콘솔](https://console.cloud.tencent.com/cdb/instance)에 로그인하여 리전을 선택하고 인스턴스 목록에서 대상 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
b. **기본 정보** 페이지의 **리얼 서버** 섹션에서 **구성**을 클릭합니다.
c. 팝업 창에서 **제출**을 클릭합니다.
d. **백엔드 서비스**에서 **SNAT IP 추가**를 클릭합니다.
e. 팝업 창에서 **서브넷**을 선택하고 할당 IP 옆에 있는 **추가**를 클릭한 후 자동을 선택하거나 할당된 IP를 수동으로 입력하고 **저장**을 클릭합니다.
2.  공중망 리스너 포트를 구성합니다.
a. [CLB 콘솔](https://console.cloud.tencent.com/cdb/instance)에 로그인하여 리전을 선택하고 인스턴스 목록에서 대상 인스턴스 ID를 클릭하여 인스턴스 관리 페이지로 이동합니다.
b. 인스턴스 관리 페이지에서 **리스너 관리** 탭을 선택하고 **TCP/UDP/TCP SSL 리스너** 아래에서 **생성**을 클릭합니다.
c. 팝업 창에서 설정을 완료하고 **제출**을 클릭합니다.

## 3단계: MySQL 인스턴스 바인딩
1. 리스너를 생성한 후 **리스너 관리**를 클릭하고 오른쪽의 **바인딩**을 클릭합니다.
2. 팝업 창에서 객체 유형을 **기타 사설망 IP**로 선택하고 MySQL 인스턴스의 IP 주소와 포트를 입력하고 **확인**을 클릭합니다.
>!로그인 계정은 표준 계정(IP별 과금)이어야 합니다. 바인딩에 실패하면 [티켓 제출](https://console.cloud.tencent.com/workorder/category)하여 도움을 받으십시오.
>

## 4단계: MySQL 보안 그룹 구성
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/instance) 로그인 후 리전을 선택하고, 인스턴스 리스트에서 인스턴스 ID 또는 **작업** 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **보안 그룹** 탭을 선택하고 **보안 그룹 구성**을 클릭하여 모든 포트를 열도록 보안 그룹 규칙을 구성한 후, 보안 그룹이 퍼블릭 IP에서 액세스를 허용하는지 확인합니다. 구성에 대한 자세한 내용은 [CDB 보안 그룹 관리](https://intl.cloud.tencent.com/document/product/236/14470)를 참고하십시오.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/I4a8207_37.png)

## 5단계: MySQL Workbench 클라이언트를 통해 인스턴스에 연결
1. [MySQL 커뮤니티 다운로드](https://dev.mysql.com/downloads/)에서 MySQL Workbench를 다운로드하여 설치합니다.
 1. 다운로드 페이지로 이동하여 **MySQL Workbench**를 클릭합니다.
 2. Windows (x86, 64-bit), MSI Installer 다음에 **Downloads**를 클릭합니다.
 3. **No thanks, just start my download**를 클릭합니다.
2. MySQL Workbench가 설치되면 열고 MySQL Connections 뒤의 더하기 기호를 클릭하여 대상 인스턴스의 정보를 추가합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/1bdd5024d708284fd8dc06b2177e0ea6.png)
3. 팝업 창에서 다음 항목을 구성하고 **ok**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ec8f7b944542bc28721446a1e2dbede5.png)
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>Connection name</td>
<td>연결 이름을 지정합니다.</td></tr>
<tr>
<td>Connection Method</td>
<td>Standard(TCP/IP)를 선택합니다.</td></tr>
<tr>
<td>Hostname</td>
<td>CLB 인스턴스의 주소를 입력합니다. CLB 인스턴스 세부 정보 페이지의 기본 정보에서 VIP 정보를 볼 수 있습니다.</td></tr>
<tr>
<td>Port</td>
<td>CLB 인스턴스의 포트를 입력합니다. CLB 인스턴스 세부 정보 페이지의 리스너 관리에서 TCP 포트 번호를 볼 수 있습니다.</td></tr>
<tr>
<td>Username</td>
<td>대상 MySQL 인스턴스의 계정 이름, 즉 인스턴스 관리 페이지 &gt; 데이터베이스 관리 &gt; 계정 관리에서 생성된 계정 이름을 입력합니다.</td></tr>
<tr>
<td>Store in Vault...</td>
<td>비밀번호 필드에 대상 MySQL 인스턴스의 Username 계정 비밀번호를 입력하고 저장합니다.</td></tr>
</tbody></table>
4. MySQL Workbench 홈페이지로 돌아가 방금 구성된 인스턴스를 클릭하여 연결합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/04cb6e563f25bedcaad235be50890aec.png)
5. 연결 완료 후의 UI는 다음과 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ad6c60db6691f5b2f825d36362877fe7.png)
