라이브 방송 중 도메인 연결 템플릿 이벤트가 트리거된 경우 Tencent Cloud는 자동으로 클라이언트 서버에 응답 요청을 보내며, 클라이언트 서버가 요청에 응답하게 됩니다. 인증 후 라이브 방송 이벤트 콜백 정보를 포함한 JSON 데이터 패키지를 수동으로 얻을 수 있습니다.

현재 메시지 공지를 트리거하는 라이브 방송 이벤트는 라이브 방송 푸시 스트리밍, 라이브 방송 스트리밍 중단, 라이브 방송 녹화, 라이브 방송 화면 캡처, 라이브 방송 음란물 감지입니다.

## 전체 프로세스

<img src="https://main.qcloudimg.com/raw/ea1b7cd9ac91b2d561ef045c2f6f2159.svg" data-nonescope="true">

**프로세스 설명**
1. 콘솔 또는 클라우드 API 직접 호출을 통해 호스트가 이벤트 메시지 공지 URL과 녹화, 화면 캡처 등 관련 기능을 설정합니다.
2. 호스트가 라이브 방송 스트리밍을 푸시하거나 중단합니다.
3. 라이브 방송 서비스 내부에서 이벤트가 발생할 경우 이벤트 공지 서비스를 통해 시청자에게 메시지가 통합 콜백됩니다.
<span id="protocol"></span>
## 이벤트 메시지 공지 프로토콜

### 네트워크 프로토콜
- 요청: HTTP POST 요청, 패킷 콘텐츠는 JSON이며 각 메시지의 세부 패킷 콘텐츠는 아래 내용을 참조하십시오.
- 응답: HTTP STATUS CODE = 200, 서버가 응답 패키지의 세부 콘텐츠를 무시합니다. 원활한 프로토콜 연결을 위해 클라이언트 응답 콘텐츠에 JSON: `{"code":0}` 추가를 권장합니다.

### 공지 신뢰성

이벤트 공지 서비스는 재시도 기능이 있으며 재시도 간격은 60초로 총 3번 반복됩니다. 재시도로 인한 서버와 네트워크 대역폭 충돌을 피하기 위해 정상 패킷 반환을 유지해주십시오. 재시도가 트리거되는 조건은 아래와 같습니다.

- 장시간(20초) 패킷 응답이 없는 경우
- 응답 HTTP STATUS가 200이 아닌 경우

<span id="configuration"></span>
## 콜백 이벤트 설정 방법
콜백 설정은 두 가지 방식으로 할 수 있습니다. 첫 번째 방법은 [CSS 콘솔](#c_callback)을 통해서 할 수 있습니다. 두 번째 방법은 [서버 API](#api_callback) 호출을 통해서 할 수 있습니다.
>?라이브 방송 콜백 메시지 공지 URL은 푸시 스트리밍, 스트리밍 중단, 녹화, 화면 캡처, 음란물 감지 이벤트의 단독 콜백 URL 설정을 지원합니다.



<span id="c_callback"></span>
### CSS 콘솔
1. CSS 콘솔의 [기능 템플릿]>[콜백 설정](https://console.cloud.tencent.com/live/config/callback)에 들어가 콜백 템플릿을 생성합니다. 자세한 내용은 [콜백 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/31074)을 참조하십시오.
![](https://main.qcloudimg.com/raw/e487fbb21c3e7018c97f82f7055b8f8a.png)
2. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)에서 작업에 필요한 푸시 스트리밍 도메인을 찾고 [Manage]>[Template Configuration]을 클릭하여 도메인과 트랜스 코딩 템플릿을 연결합니다. 자세한 내용은 [콜백 설정](https://cloud.tencent.com/document/product/267/35254)을 참조하십시오.
<span id="api_callback"></span>
### 서버 API
1. [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)을 호출하여 콜백 템플릿 인터페이스를 생성하고 필요한 콜백 매개변수 정보를 설정합니다.
2. [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)을 호출하여 콜백 규칙을 생성하고 매개변수 푸시 스트리밍 도메인 이름 DomainName과 TemplateId(1단계에서 반환)를 설정합니다. 푸시 스트리밍과 재생 주소 중 일치하는 AppName을 작성하여 특정 라이브 방송 스트리밍 콜백을 활성화할 수 있습니다.

## 콜백 정보 매개변수 설명
콜백 템플릿을 도메인에 성공적으로 연결한 후 라이브 방송 중 템플릿 이벤트가 트리거되면 Tencent Cloud는 자동으로 콜백 정보를 포함한 JSON 패킷을 고객 서버에 보냅니다. 콜백 정보의 세부 매개변수 설명은 아래와 같습니다.
- [푸시 스트리밍 이벤트 메시지 공지](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [스트리밍 중단 이벤트 메시지 공지](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [녹화 이벤트 메시지 공지](https://intl.cloud.tencent.com/zh/document/product/267/38082)
- [화면 캡처 이벤트 메시지 공지](https://intl.cloud.tencent.com/zh/document/product/267/38083)
- [음란물 감지 이벤트 메시지 공지](https://intl.cloud.tencent.com/zh/document/product/267/38084)






