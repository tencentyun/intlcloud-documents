StreamLive는 HLS 파일을 Tencent Cloud COS로 출력하여 보관하도록 지원합니다. 이를 위해 우선 COS에 버킷을 생성하고 StreamLive에 버킷 액세스 권한을 부여해야 합니다.

1. COS 서비스 활성화 및 COS 버킷 생성

COS 아카이브로 출력하기 전에 [Tencent Cloud COS 서비스](https://console.cloud.tencent.com/cos5)를 활성화해야 합니다. COS 서비스 활성화 후 [COS 버킷 콘솔](https://console.cloud.tencent.com/cos5)에서 [버킷 리스트]를 선택하고 [버킷 생성]을 클릭하여 가장 가까운 리전에 COS 버킷을 생성합니다.

![img](https://main.qcloudimg.com/raw/258a128f8e010886f7bea5b6dac83c72.png)

2. 출력 유형을 HLS_ARCHIVE로 선택합니다. StreamLive 콘솔로 돌아와서 출력 설정 시, 출력 유형을 HLS_ARCHIVE로 선택합니다.

![img](https://main.qcloudimg.com/raw/5e782e85e27d4f860d9921cc86f1165f.png)

3. StreamLive에 COS 버킷 액세스 권한을 부여합니다. StreamLive에 COS 버킷 액세스 권한을 부여하지 않았기 때문에 COS 타깃 필드가 회색으로 설정되어 있고 입력이 제한되어 있습니다. [click here]을 클릭하면 권한 부여 알림창이 나타납니다. [Authorize Now]를 클릭하여 권한 추가 인터페이스로 이동합니다. [Grant]를 클릭하여 권한 부여를 완료합니다.

![img](https://main.qcloudimg.com/raw/5327f143f1fc7482c68225e8abad3c82.png))![img](https://main.qcloudimg.com/raw/3b3a91b1e9053f9ac0b6c9bc2955e12c.png)

권한 부여 완료 후 StreamLive 인터페이스로 돌아와 [Authorization completed]를 선택하면 COS Destination 필드를 입력할 수 있습니다.

![img](https://main.qcloudimg.com/raw/ee8f5a51ec6fb2642e570a9c67f91865.png))![img](https://main.qcloudimg.com/raw/41fc5c9c4a18d04b54f6585241231688.png)

4. COS 아카이브 주소를 입력합니다. 생성한 COS 버킷을 바탕으로 COS 아카이브 주소를 http://.cos..myqcloud.com/path 형식으로 입력합니다.

5. 설정을 저장하고 제출합니다. [StreamLive 채널 관리](https://intl.cloud.tencent.com/document/product/1048/45214)의 나머지 channel 설정을 완료하고 저장합니다.




