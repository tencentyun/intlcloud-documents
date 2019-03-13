## 시나리오
보안 그룹은 하나 이상의 클라우드 데이터베이스에 대한 네트워크 액세스 제어를 설정하기 위한 필터링 기능이 있는 상태 기반 가상 방화벽이고 Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 도구입니다. 보안 그룹은 논리적인 그룹입니다. 동일한 지역에서 동일한 네트워크 보안 격리 요구가 있는 클라우드 데이터베이스 인스턴스를 동일한 보안 그룹에 추가할 수 있습니다. 클라우드 데이터베이스는 CVM과 보안 그룹 목록을 공유합니다. 매칭은 보안 그룹의 규칙을 기반으로 수행됩니다. 특정 규칙 및 제한 사항에 대한 자세한 내용은 보안 그룹 설명을 참조하십시오.

>!
> 1. TencentDB 보안 그룹은 현재 **VPC 사설망 액세스의 네트워크 관리만 지원하고 기본 네트워크의 네트워크 관리는 지원하지 않습니다.**
> 2. **TencentDB에 액티브 아웃바운드 트래픽이 없기 때문에, 해당 아웃바운드 규칙은 TencentDB에 무효합니다.**
> 3. TencentDB for MongoDB 보안 그룹은 마스터 인스턴스, 읽기 전용 인스턴스와 재해 복구 인스턴스를 지원합니다.
> 4. 보안 그룹이 기본적인 탬플릿에 대해 다음 사항을 주의하십시오.
>  - Linux에 22 포트 개방: SSH 로그인을 위한 TCP 포트 22만 궁중망에 노출하며 모든 사설망 포트는 개방합니다. **TencentDB에서는 이 템플릿을 사용할 수 없습니다.**
>  - Windows에 3389 포트 개방: MSTSC 로그인을 위한 TCP 포트 3389만 궁중망에 노출하며 모든 사설망 포트는 개방합니다. **TencentDB에서는 이 템플릿을 사용할 수 없습니다.**
>  - 전체 포트 개방: TencentDB에 모든 IP의 접근을 허용합니다. 어느 정도의 보안 위험이 있습니다.
> 5. 보안 그룹 기능은 현재 화이트리스트에 의해 관리합니다. 필요할 경우, [티켓 제출](https://console.cloud.tencent.com/workorder/category)을 하여 신청하십시오.

## 작업 절차

### 보안 그룹 생성

1. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)에 로그인 후, [클라우드 제품] > [CVM]을 선택하여 CVM 관리 페이지로 들어가십시오.
2. 좌측 탐색 모음에서 [보안 그룹]을 클릭하여 보안 그룹 관리 페이지로 들어가십시오.
   ![](https://main.qcloudimg.com/raw/9c154ef45b104ffebef99a3de249b50c.png)
3. [생성]을 클릭하여, [탬플릿] 또는 [사용자 지정] 생성을 선택하고 보안 그룹의 [이름] (예: my-security-group)을 입력합니다. [속한 프로젝트]를 선택하고, [비고]를 선택적으로 입력한 후, 확인하고 [확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/cc9a780ddd091f68c5476ee8463e1294.png)

### TencentDB for MongoDB에 보안 그룹 구성
[보안 그룹](https://cloud.tencent.com/doc/product/213/500)은 Tencent Cloud가 제공하는 인스턴스 수준의 방화벽이고 TencentDB에 인바운드/아웃바운드 트래픽을 관리합니다. 인스턴스 구매 시, 보안 그룹을 바인딩할 수 있으며, 인스턴스를 구매한 후, 콘솔에서 보안 그룹을 바인딩할 수도 있습니다.

> ! 현재 TencentDB for MongoDB 보안 그룹은 **VPC 클라우드 데이터베이스** 구성만 지원합니다.

1. [MongoDB 콘솔](https://console.cloud.tencent.com/mongodb)에 로그인하고, 인스턴스 리스트에서 구성할 보안 그룹 인스턴스를 선택합니다. [작업] 열에서 [관리] > [보안 그룹]을 선택합니다.
![](https://main.qcloudimg.com/raw/22337a8d71bb79228790c3253d4fd3e2.png)
2. 바인딩할 보안 그룹을 선택하고 [확인]을 클릭하면 보안 그룹이 TencentDB for MongoDB와 바인딩됩니다.
![](https://main.qcloudimg.com/raw/b63568e07e679628d17d61b75fb453f5.png)

### 보안 그룹 삭제
1. [보안 그룹 페이지](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인하고 보안 그룹 리스트의 [작업] 열에서 [추가] > [삭제]를 선택합니다.
![](https://main.qcloudimg.com/raw/794d76f9f7969fe66f250b63e7a99415.png)
2. 팝업된 보안 그룹 삭제 페이지에서 [확인]을 선택합니다. 현재 보안 그룹이 연결한 CVM이 있다면, 먼저 보안 그룹을 해제하고 삭제할 수 있습니다.

### 보안 그룹 클론
1. [보안 그룹 페이지](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인하고 보안 그룹 리스트의 [작업] 열에서 [추가] > [클론]을 선택합니다.
   ![](https://main.qcloudimg.com/raw/28810c1f2b863caac6d4598d3b4c5c07.png)
2. 팝업된 클론 보안 그룹 페이지에서 대상 지역, 대상 프로젝트를 선택하고 [확인]을 클릭합니다. 새 보안 그룹을 CVM에 연결해야 할 경우, 보안 그룹 안의 CVM 관리 작업을 다시 진행하십시오.

### 보안 그룹에 규칙 추가
1. [보안 그룹 페이지](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인하고 업데이트할 보안 그룹을 선택하고 보안 그룹 ID를 클릭하여 세부 정보 페이지에 들어갑니다. 세부 정보 페이지는 해당 보안 그룹의 세부 정보 및 인바운드/아웃바운드 규칙이 포함되어 있습니다.
2. 인/아웃바운드 규칙 탭에서 [규칙 추가]를 클릭하십시오.
  ![](https://main.qcloudimg.com/raw/c2c4533dc6ff96e4f2af2fb8ee0fea30.png)
3. 탭에서 인/아웃바운드 규칙이 필요한 옵션을 선택한 후, 필요한 정보를 입력합니다. 예를 들어, 오리진/대상을 10.0.0.0/0으로 지정하고 프로토콜 포트를 TCP:3306으로 지정하고 또는 전략을 허용으로 설정합니다. [완료]를 클릭하고 [새 줄 추가]를 클릭하면 동시에 다중 규칙을 설정할 수 있습니다.
  ![](https://main.qcloudimg.com/raw/2f48931b61d45ab8275e12cf0cf70945.png)

### 보안 그룹 가져오기/내보내기 규칙
1. [보안 그룹 페이지](https://console.cloud.tencent.com/cvm/securitygroup)에 로그인하고 업데이트할 보안 그룹을 선택하고 보안 그룹 ID를 클릭하여 세부 정보 페이지에 들어갑니다.
2. 인/아웃바운드 규칙 탭에서 [규칙 가져오기]를 클릭하십시오.
![](https://main.qcloudimg.com/raw/ab01ffb53084acf3e88219df7aca7b25.png)
3. 기존 규칙이 있으면 먼저 기존 규칙을 내보내는 것을 권장합니다. 규칙을 가져오면 기존의 규칙을 덮어쓰게 되기 때문입니다. 규칙이 비어 있다면 먼저 탬플릿을 내보내고 탬플릿 파일을 편집한 후, 다시 [파일 선택]을 클릭하여 탬플릿 파일을 선택하고 [가져오기]를 클릭하면 됩니다.
![](https://main.qcloudimg.com/raw/fda954cd9eaa9058a1fea6ca52d12f50.png)
