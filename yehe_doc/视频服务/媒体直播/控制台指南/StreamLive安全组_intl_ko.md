보안 그룹은 필터 기능이 있는 스테이트풀 가상 방화벽으로 주로 입력 소스의 보안 인증을 관리하며 Tencent Cloud에서 제공하는 중요한 네트워크 보안 격리 방법입니다.

### 보안 그룹 리전 선택

현재 Tencent Cloud StreamLive에는 인도 뭄바이, 태국 방콕, 한국 서울, 일본 도쿄의 4개 가용존이 있습니다. 여기에서 리전을 선택할 수 있습니다. 기타 다른 가용존에 대한 배포를 요청하려면 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하시기 바랍니다.
![](https://qcloudimg.tencent-cloud.cn/raw/c099c3984d22fca6227e14123d9e2c17.jpg)

### 보안 그룹 생성

보안 그룹은 입력 소스 IPV4 주소의 유효성을 확인하는 용도로 사용되며, 보안 그룹 설정을 통해 StreamLive 채널을 보다 안전하게 입력할 수 있습니다.

[Security Group Management] 메뉴를 선택하고 [Create Security Group]을 클릭하여 보안 그룹을 생성합니다. Name을 입력한 뒤, CIDR 포맷의 문자열을 새로운 입력 보안 그룹에 추가하고 쉼표 또는 줄 바꿈 부호로 구분해 줍니다. 입력 후 [Confirm]을 클릭해 생성을 완료합니다.

![img](https://main.qcloudimg.com/raw/e5c7365ba3724802b2013b3c25cdc07b.png)

>?
> - 보안 그룹에는 idle과 occupied 두 가지 상태가 있습니다.
> - idle은 현재 보안 그룹이 연결되어 있지 않으며 편집이나 삭제가 가능한 상태임을 나타냅니다.
> - occupied는 현재 보안 그룹이 channel-input과 연결되어 있음을 나타내며, 이 경우 보안 그룹을 편집할 수는 있으나 삭제할 수는 없습니다.
> - 콘솔은 기본적으로 5개의 보안 그룹 생성만 지원하며, 더 많은 보안 그룹이 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder)을 통해 Tencent Cloud 고객 서비스 직원에게 문의하십시오.
