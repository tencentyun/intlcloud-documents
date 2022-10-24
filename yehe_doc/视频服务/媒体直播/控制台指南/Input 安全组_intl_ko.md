Input 보안 그룹은 필터링 기능이 있는 스테이트풀 가상 방화벽입니다. 주로 푸시형 input의 경우 사용자가 스트림을 푸시할 때 보안 인증을 수행하며, 현재 Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 방법인 IP(세그먼트) 얼로우리스트 방식을 지원합니다.



## 전제 조건
- [StreamLive](https://intl.cloud.tencent.com/products/mdl)가 활성화되어 있어야 합니다. 
- [StreamLive 콘솔](https://console.intl.cloud.tencent.com/mdl/security)에 로그인되어 있어야 합니다.

## Input 보안 그룹 관리
왼쪽 사이드바에서 **Security Group Management**를 클릭하면 생성된 input 보안 그룹 이름, 사용 상태, ID를 볼 수 있으며, 생성, 편집, 삭제할 수 있습니다. 현재 Tencent Cloud StreamLive에는 인도 뭄바이, 태국 방콕, 한국 서울, 일본 도쿄, 독일 프랑크푸르트의 5개 가용존이 있습니다. 여기에서 리전을 선택할 수 있습니다. 다른 가용존에 대한 니즈가 있는 경우 [고객센터](https://intl.cloud.tencent.com/contact-us)로 문의하십시오.

![](https://qcloudimg.tencent-cloud.cn/raw/fc7c32157eccae3591533e14c511fa8f.png)


### Input 보안 그룹 생성
보안 그룹은 입력 소스 IPV4 주소의 합법성을 인증하는 데 사용되며, 보안 그룹 구성을 입력하여 StreamLive 채널의 입력을 보다 안전하게 만들 수 있습니다. input 보안 그룹을 생성해야 하는 경우 페이지 왼쪽 상단의 **Create Security Group** 버튼을 클릭하고 팝업 창에서 구성합니다.
1) **Name**: 보안 그룹의 이름으로, 사용자가 설정할 수 있습니다. 1-32자리의 숫자, 알파벳, 언더바 ‘_’를 지원합니다.
2) **IP Allowlist**: CIDR 형식의 IP 얼로우리스트이며 쉼표 또는 줄 바꿈으로 구분됩니다. 소스 IP를 제한할 필요가 없는 경우 0.0.0.0/0을 입력합니다.
입력 후 **Confirm** 버튼을 클릭하면 생성이 완료됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/4fd4169c10d7b6f968f323822c37301a.png)

### Input 보안 그룹 수정
Input 보안 그룹 수정이 필요한 경우 수정이 필요한 **input security group** 우측의 **Edit**을 클릭하여 팝업창에서 수정 후 **Confirm**을 클릭하여 수정을 완료합니다.

![](https://qcloudimg.tencent-cloud.cn/raw/6fbf87ce94c7c1cc8e9914c5fb9425ef.png)

### Input 보안 그룹 삭제
Input 보안 그룹을 삭제해야 하는 경우 삭제할 **input security group** 우측의 **Delete**를 클릭하고 팝업 창에서 **Confirm**을 클릭하면 삭제가 완료됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/b0f08d28e5b0658c04756a179100dad9.png)

>?
>- 보안 그룹에는 idle과 occupied 두 가지 상태가 있습니다.
>- idle은 현재 보안 그룹이 연결되어 있지 않으며 편집이나 삭제가 가능한 상태임을 나타냅니다.
>- occupied는 현재 보안 그룹이 channel-input과 연결되어 있음을 나타내며, 이 경우 보안 그룹을 편집할 수는 있으나 삭제할 수는 없습니다.
>- 콘솔은 기본적으로 5개의 보안 그룹 생성만 지원하며, 더 많은 보안 그룹이 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder)을 통해 Tencent Cloud 고객 서비스 직원에게 문의하십시오.

