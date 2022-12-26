본 문서는 Tencent Cloud TRTC Web SDK Demo를 빠르게 실행하는 방법을 소개합니다.
## 준비 작업
TRTC Web SDK Demo 실행 전에 알아두어야 할 사항들이 있습니다.

### 지원 플랫폼
TRTC Web SDK는 WebRTC를 기반으로 구현되었으며 현재 데스크톱 및 모바일에서 주요 브라우저를 지원합니다. 지원 관련 자세한 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/41664)을 참고하십시오.
귀하의 시나리오가 지원되는 테이블에 없는 경우 [TRTC Web SDK 기능 테스트 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)에서 현재 환경이 WebView 환경 등 WebRTC의 모든 기능을 지원하는지 확인할 수 있습니다.

응용 시나리오가 주로 교육 시나리오의 경우, 교사측의 [Electron](https://intl.cloud.tencent.com/document/product/647/35097) 솔루션 사용을 권장합니다. 크고 작은 듀얼 채널 화면을 지원하여 더 효율적으로 화면을 공유할 수 있으며 네트워크 신호가 약한 경우 복구 능력이 더욱 뛰어납니다. 

### URL 도메인 프로토콜 제한
브라우저 보안 정책의 제한으로 인해 WebRTC 기능을 사용하려면 페이지의 액세스 프로토콜에 대한 엄격한 요구 사항이 있으므로 다음 테이블을 참고하여 애플리케이션을 개발하고 배포하십시오.

| 응용 시나리오     | 프로토콜             | 수신(재생) | 발송(마이크 켜짐) | 화면 공유 | 비고     |
|----------|:-----------------|:---------|----------|--------|----------|
| 프로덕션 환경     | HTTPS 프로토콜         | 지원      | 지원      | 지원               | **권장** |
| 프로덕션 환경     | HTTP 프로토콜         | 지원         | 미지원       | 미지원   |    -      |
| 로컬 개발 환경 | http://localhost | 지원         | 지원         | 지원     | **권장** |
| 로컬 개발 환경 | http://127.0.0.1 | 지원         | 지원         | 지원     |      -    |
| 로컬 개발 환경 | http://[로컬 IP]  | 지원         | 미지원       | 미지원   |    -      |
| 로컬 개발 환경 | file:///         | 지원         | 지원         | 지원     |     -     |

### 방화벽 구성
TRTC Web SDK 사용 시 방화벽 제한으로 인해 음성 및 영상 통화가 안될 수 있으니 [방화벽 제한](https://www.tencentcloud.com/document/product/647/35164)을 참고하여 해당 포트 및 도메인 이름을 방화벽 얼로우리스트에 추가하시기 바랍니다.


## 전제 조건
[Tencent Cloud 가입](https://intl.cloud.tencent.com/document/product/378/17985) 계정이 있어야 합니다.

## 작업 단계

### 1단계: 애플리케이션 생성

1. TRTC 콘솔에 로그인하고 왼쪽 사이드바에서 [[애플리케이션 관리](https://console.tencentcloud.com/trtc/app)]를 선택합니다.

2. [애플리케이션 생성]을 클릭하고 'APIExample'과 같은 애플리케이션 이름을 입력합니다. 이미 애플리케이션이 있는 경우 [기존 애플리케이션 선택]을 선택하고 [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/6704c9f7eb9e18e422c513cb9a2a3926.png)


### 2단계: 샘플 코드 다운로드

1. UI 없음을 선택하고 Github로 이동하여 플랫폼에 대한 샘플 코드를 다운로드합니다.
2. [다음]을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d28964ad85dddd85833a28310a62d514.png)


### 3단계: 프로젝트 구성
1. 데모 프로젝트를 실행 중인 경우 [테스트]를 선택합니다. SDKAppID와 Secret key를 기록해 둡니다.
![](https://qcloudimg.tencent-cloud.cn/raw/82a45972f2d12763a6dc80eee6c952c0.png)
2. 이전에 다운로드한 파일을 엽니다. 콘솔의 지시에 따라 SDKAppID와 Secret key를 수정하고 [다음]을 클릭합니다.

>?
>- 본문에서 설명하는 UserSig를 생성하는 방법은 클라이언트 코드에서 SECRETKEY를 구성하는 것입니다. 이 방법에서 SECRETKEY는 쉽게 디컴파일되고 역전될 수 있으며, 키가 공개되면 공격자가 Tencent Cloud 트래픽을 도용할 수 있습니다. 따라서 **이 방법은 TRTC-API-Example의 로컬 실행 및 디버깅에만 적합합니다**.
>- UserSig의 계산 코드를 서버에 통합하고 App 지향 API를 제공하는 것이 가장 좋습니다. UserSig가 필요할 때 App은 동적 UserSig에 대한 요청을 서버에 보낼 수 있습니다. [서버에서 UserSig 생성](https://www.tencentcloud.com/document/product/647/35166)을 참고하십시오.


## FAQ

### 1. 클라이언트에서 “RtcError: no valid ice candidate found” 오류가 발생합니다. 어떻게 처리해야 합니까?
STUN 홀 펀칭이 실패했음을 나타냅니다. 방화벽 설정을 확인하려면 [방화벽 제한](https://www.tencentcloud.com/document/product/647/35164)을 참고하십시오.

### 2. 클라이언트에서 "RtcError: ICE/DTLS Transport connection failed" 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 합니까?
TRTC Web SDK가 미디어 전송 연결을 설정하지 못했음을 나타냅니다. [방화벽 제한](https://www.tencentcloud.com/document/product/647/35164)에서 방화벽 구성을 확인하십시오.

### 3. 10006 error가 발생합니다. 어떻게 처리해야 합니까?
‘Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it’ 오류가 발생하는 경우 TRTC 애플리케이션의 서버 상태가 정상인지 확인합니다.
[TRTC 콘솔](https://console.cloud.tencent.com/rav)에 로그인하여 생성한 애플리케이션을 클릭한 후 **애플리케이션 정보**를 클릭하면 서비스 상태를 확인할 수 있습니다.
![](https://main.qcloudimg.com/raw/e3b928c20ed3379679e5e73e210fd63e.png)

>? 기타 FAQ는 [Web 관련](https://intl.cloud.tencent.com/document/product/647/37340)을 참고하십시오.
