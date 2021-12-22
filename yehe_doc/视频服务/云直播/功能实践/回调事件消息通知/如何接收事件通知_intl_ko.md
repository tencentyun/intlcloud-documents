라이브 방송 중 도메인 연결 템플릿 이벤트가 트리거된 경우 Tencent Cloud가 클라이언트 서버에 응답 요청을 보내며, 클라이언트 서버가 요청에 응답하게 됩니다. 인증 후 라이브 방송 이벤트 콜백 정보를 포함한 JSON 데이터 패킷을 수동으로 얻을 수 있습니다.

현재 메시지 알림을 트리거하는 라이브 방송 이벤트는 라이브 방송 푸시 스트리밍, 라이브 방송 스트리밍 중단, 라이브 방송 녹화, 라이브 방송 화면 캡처, 라이브 방송 음란물 감지입니다.

## 전체 프로세스

<img src="https://main.qcloudimg.com/raw/252b7e06b322350c8520283e7826d5a3.png" data-nonescope="true">

**프로세스 설명:**
1. 콘솔 또는 클라우드 API 직접 호출을 통해 호스트가 이벤트 메시지 알림 URL과 녹화, 화면 캡처 등 관련 기능을 설정합니다.
2. 호스트가 라이브 방송 스트리밍을 푸시하거나 중단합니다.
3. 서비스에서 내부 이벤트가 발생하면 이벤트 메시지 알림 서비스를 통해 시청자에게 메시지가 전송됩니다.


[](id:protocol)
## 이벤트 메시지 알림 프로토콜

### 네트워크 프로토콜
- 요청: HTTP POST 요청, 패킷 콘텐츠는 JSON이며 각 메시지의 세부 패킷 콘텐츠는 아래 내용을 참조하십시오.
- 응답: HTTP STATUS CODE = 200, 서버는 응답 패킷의 특정 내용을 무시합니다. 더 정확한 연결을 위해 응답에 JSON: {"code":0}를 추가하는 것이 좋습니다.

### 알림 신뢰성
이벤트 알림 서비스에는 재시도 메커니즘이 있습니다. 재시도 간격은 2분으로, 총 5번 수행됩니다. 또한, 라이브 방송 푸시 스트리밍, 라이브 방송 스트리밍 중단, 라이브 방송 녹화, 라이브 방송 음란물 감지 이벤트 알림 재시도 간격은 1분으로, 총 12번 수행됩니다.
이러한 재시도가 서버 및 네트워크 대역폭에 미치는 영향을 방지하려면, 응답 패킷이 정상적인지 확인하시기 바랍니다. 재시도 트리거 조건은 다음과 같습니다.
- 장시간(20초) 패킷 응답이 없는 경우
- 응답 HTTP STATUS가 200이 아닌 경우

[](id:configuration)
## 콜백 이벤트 설정 방법
콜백 설정은 두 가지 방식으로 할 수 있습니다. 첫 번째 방법은 [CSS 콘솔](#c_callback)을 통해서 할 수 있습니다. 두 번째 방법은 [서버 API](#api_callback) 호출을 통해서 할 수 있습니다.
>?라이브 방송 콜백 메시지 알림 URL은 푸시 스트리밍, 스트리밍 중단, 녹화, 화면 캡처, 음란물 감지 이벤트의 단독 콜백 URL 설정을 지원합니다.



[](id:c_callback)
### CSS 콘솔
1. CSS 콘솔의 **이벤트 센터>[라이브 방송 콜백](https://console.cloud.tencent.com/live/config/callback)**으로 이동하여 콜백 템플릿을 생성합니다. 자세한 내용은 [콜백 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31074)을 참조하십시오.
2. [ **도메인 관리** ](https://console.cloud.tencent.com/live/domainmanage)를 선택하고, 도메인 이름을 찾은 후에, **관리>템플릿 설정**을 클릭하여 콜백 템플릿과 연결합니다. 자세한 방법은 [콜백 설정](https://intl.cloud.tencent.com/document/product/267/31065)을 참조하십시오.

[](id:api_callback)
### 서버 API
1. [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)을 호출하여 콜백 템플릿 인터페이스를 생성하고 필요한 콜백 매개변수 정보를 설정합니다.
2. [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)을 호출하여 콜백 규칙을 생성하고 매개변수 푸시 도메인 이름 DomainName과 TemplateId(1단계로 돌아가기)를 설정합니다. 푸시 스트리밍과 재생 주소 중 일치하는 AppName을 작성하여 특정 라이브 방송 스트리밍 콜백을 활성화할 수 있습니다.

## 콜백 정보 매개변수 설명
콜백 템플릿과 도메인 연결 성공 후. 라이브 방송 중 템플릿 이벤트가 트리거되면 Tencent Cloud는 자동으로 콜백 정보를 포함한 JSON 패킷을 고객 서버에 보냅니다. 콜백 정보의 세부 매개변수 설명은 아래와 같습니다.
- [스트림 푸시 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38081)
- [스트림 중단 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38081)
- [녹화 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38082)
- [화면 캡처 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38083)
- [음란물 감지 이벤트 알림](https://intl.cloud.tencent.com/document/product/267/38084)






