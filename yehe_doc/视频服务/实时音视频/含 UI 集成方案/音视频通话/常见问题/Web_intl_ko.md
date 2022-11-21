## 1. 기본 환경 문제

### TRTC Web SDK는 어떤 브라우저를 지원합니까?

브라우저 지원에 대한 자세한 내용은 [지원되는 브라우저](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)를 참고하십시오. 사용 중인 브라우저가 문서에 없는 경우 브라우저에서 [TRTC 호환성 확인 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC를 완벽하게 지원하는지 테스트할 수 있습니다.

### 현재 네트워크 품질을 테스트하려면 어떻게 해야 합니까?

자세한 내용은 [통화 전 네트워크 품질 확인](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html)을 참고하십시오.

### SDK는 로컬에서 테스트했을 때 제대로 작동했지만 온라인으로 배포한 후에는 음성/영상 통화가 되지 않는 이유가 무엇입니까?

데이터 보안을 보장하고 사용자의 개인 정보를 보호하기 위해 브라우저는 예를 들어 `https`, `localhost` 또는 `file://`이 액세스에 사용되는 경우와 같이 안전한 환경에서만 마이크와 카메라에 대한 액세스를 허용합니다. HTTP는 안전하지 않기 때문에 브라우저는 HTTP가 사용될 때 미디어 장치에 대한 액세스를 차단합니다.

SDK를 로컬 개발 환경에서 사용할 수 있지만 웹에 배포한 후 카메라나 마이크에서 데이터를 캡처할 수 없는 경우 웹 페이지가 HTTP를 사용하여 배포되었는지 확인하십시오. 그렇다면 대신 HTTPS를 사용하고 유효한 HTTPS 인증서가 있는지 확인하십시오.

자세한 내용은 [도메인 이름 및 프로토콜 지원](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html#h2-2)을 참고하십시오.

### ‘is not included in the current tim&#39;s package’ 오류가 발생하면 어떻게 해야 하나요?

**원인**

TIM 종속성 버전이 너무 오래되었습니다.

버전 문제가 아닌 경우 SDKAppID에 TRTC 패키지를 구입하지 않았거나 구입한 패키지가 해당 기능을 지원하지 않기 때문일 수 있습니다.

**해결 방법**:

TIM 종속성을 v2.21.2 이상으로 업데이트하십시오.

TRTC 패키지를 구매하십시오.


## 2. 통합

### tuiCallEngine.handup()을 호출할 때: ‘uncaught (in promise) TypeError: cannot read property 'stop' of null’ 오류가 발생하면 어떻게 해야 하나요?

**원인**: handup()이 콜백에서 여러 번 호출되어 API가 실행되기 전에 다시 트리거됩니다.

**해결 방법**: handup()은 한 번만 호출하면 됩니다. 후속 작업은 컴포넌트 내에서 수행됩니다. 비즈니스와 관련된 작업에만 주의를 기울이면됩니다.

### 호출할 때 ‘TypeError: Cannot read property 'getVideoTracks' of null’ 오류가 발생하면 어떻게 해야 합니까?

**원인**: 수신자가 전화를 받기 전에 카메라/마이크 액세스 권한을 부여하지 않으면 오류가 발생합니다.

**해결 방법**: 기기 관련 API(예: startRemoteView 및 startLocalView)를 비동기식으로 호출하거나 컴포넌트를 최신 버전으로 업데이트합니다.

### script를 통해 컴포넌트를 가져올 때 sdkAppid에서 ‘TSignaling._onMessageReceived unknown bussinessID=undefined’ 오류가 발생하면 어떻게 해야 하나요?

**상세 내용**: 동일한 응용 프로그램(sdkAppid)이 두 클라이언트의 script를 통해 컴포넌트를 모두 가져오는 경우 두 클라이언트는 서로 통신할 수 있습니다. 그러나 한 클라이언트에서는 script를 통해 컴포넌트를 가져오고 다른 클라이언트에서는 npm을 사용하여 컴포넌트를 가져오거나 다른 클라이언트의 애플리케이션에서 TRTC Android/iOS SDK를 가져오는 경우 두 클라이언트는 서로 통신할 수 없으며 `TSignaling._onMessageReceived unknown bussinessID=undefined` 오류가 발생합니다.

**원인**: `bussinessId=undefined`는 tsignaling 버전이 너무 오래되었음을 나타냅니다. tsignaling 이전 버전의 신호 기능에 결함이 있습니다.

**해결 방법**: tsignaling 버전을 을 업데이트하고 가져오기 중에 **파일 이름이 `tsignaling-js`인지 확인합니다.**

### 알림: ‘Uncaught ( in promise ) RTCError: duplicated play() call observed, please stop() firstly <INVALID_OPERATION 0x1001>’ 오류가 발생하면 어떻게 해야 하나요?

**원인**: 음성 통화 중에 startRemoteView API를 호출하면 이 오류가 발생합니다.

**해결 방법**: 음성 통화 중에 startRemoteView를 호출하지 마십시오.

### Error: tuiCallEngine.call - ‘사용자의 기기에 접근하지 못했습니다’ 오류가 발생하면 어떻게 해야 하나요?

**원인**: 컴포넌트에 카메라/마이크 권한이 부여되지 않았거나 카메라/마이크가 존재하지 않습니다.

**해결 방법**:

[TRTC 지원 레벨 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 실행합니다.

**Chrome 설정**(chrome://settings/content)에서 Chrome이 컴포넌트를 사용하여 웹사이트에 카메라/마이크 권한을 부여했는지 확인하십시오.

### TUICallEngine web 컴포넌트는 오프라인 메시지 수신을 지원합니까?

아니요, 오프라인 메시지 수신을 지원하지 않습니다.

그러나 오프라인 메시지 푸시를 지원합니다. 푸시할 메시지는 call / groupCall의 [offlinePushInfo](https://intl.cloud.tencent.com/document/product/647/41653) 매개변수를 사용하여 설정할 수 있습니다.

### Error: TRTCClient.getMediaDevicesAuth - failed to get user video steam - NotReadableError: Could not start video source？

**원인**: 시스템이 브라우저 카메라 권한을 부여하지 않았습니다.

**해결 방법**: 시스템 설정에서 브라우저 카메라 권한을 부여합니다.