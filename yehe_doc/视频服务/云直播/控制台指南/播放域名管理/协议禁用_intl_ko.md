현재 도메인 이름의 재생 프로토콜을 제한합니다. 사용 금지 활성화 후 도메인 이름에 속한 해당 재생 프로토콜을 사용할 수 없으며, 사용 금지된 프로토콜에 의해 생성된 재생 주소에 대한 요청이 거부됩니다.

## 전제 조건
- CSS 서비스가 활성화되어 있고 [CSS 콘솔](https://console.cloud.tencent.com/live/livestat)에 로그인되어 있어야 합니다.
- [재생 도메인 이름](https://intl.cloud.tencent.com/document/product/267/35970)을 추가했습니다.


## 프로토콜 사용 금지 설정
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 프로토콜 사용 금지를 설정할 대상 **재생 도메인**을 클릭하거나 오른쪽의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **액세스 제어** > **프로토콜 사용 금지**에서 RTMP, FLV, HLS 및 WebRTC에 대한 프로토콜을 사용 금지를 활성화할 수 있습니다.
3. **편집** 버튼을 클릭하여 프로토콜 사용 금지 구성에서 지정된 프로토콜에 대해 프로토콜 사용 금지를 활성화합니다.
4. **저장**을 클릭하면 설정이 저장됩니다.

![](https://qcloudimg.tencent-cloud.cn/raw/362960a0beaf910fa931fc173b1e8abd.png)

>!
>- 프로토콜 사용 금지를 활성화하는 데 일정 시간이 걸리므로, 프로토콜 사용 금지가 여전히 적용 중인 경우, 다른 프로토콜 사용 금지가 적용된 후 작업하십시오.
>- 현재 재생 중인 스트림은 영향을 받지 않으며 HLS 프로토콜을 제외한 새 스트림만 사용 금지됩니다.



## 프로토콜 사용 금지 비활성화
지정된 프로토콜에 대한 프로토콜 사용 금지 활성화 후, 비활성화하려면 아래 단계를 따르십시오.
1. [도메인 관리](https://console.cloud.tencent.com/live/domainmanage)를 선택하고 프로토콜 사용 금지를 비활성화할 대상 **재생 도메인**을 클릭하거나 오른쪽의 **관리**를 클릭하여 도메인 관리 페이지로 이동합니다.
2. **액세스 제어> 프로토콜 사용 금지**에서 **편집** 버튼을 클릭하여 프로토콜 사용 금지 설정에서 지정된 프로토콜에 대한 프로토콜 사용 금지를 비활성화합니다.
3. **저장**을 클릭하면 설정이 저장됩니다.
![](https://qcloudimg.tencent-cloud.cn/raw/b3f339756306a55b39ed1acf1743c8c6.png)
