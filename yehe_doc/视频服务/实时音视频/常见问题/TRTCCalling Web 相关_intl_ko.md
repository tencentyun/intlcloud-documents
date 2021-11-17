[](id:base)
## 기본 문제

[](id:b1)
### TRTCCalling은 무엇입니까?
TRTCCalling은 TRTC와 TIM을 기반으로 개발된 오디오 및 비디오 솔루션으로 빠른 통합이 가능합니다. 1v1 및 다자간 영상/음성 통화를 지원합니다.
![](https://main.qcloudimg.com/raw/db70b140c138ba8c4aff32f679332ac3.png)      

[](id:b2)
### TRTCCalling roomID는 string일 수 있습니까?
roomID는 string일 수 있지만 숫자 문자열만 가능합니다.


[](id:environment)
## 환경 문제

[](id:e1)
### Web SDK는 어떤 브라우저를 지원합니까?
TRTC Web SDK의 브라우저 지원에 대한 자세한 내용은 [TRTC Web SDK 브라우저 지원](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)을 참고하십시오.
위에 나열되지 않은 시나리오의 경우 현재 브라우저에서 [TRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능이 완벽하게 지원되는지 테스트할 수 있습니다.

[](id:e2)
### 현재 네트워크 상황을 실시간으로 점검하는 방법은 무엇입니까?
구체적인 작업은 [통화 전 네트워크 품질 점검](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)을 참고하십시오.

[](id:e3)
### IM H5 Demo 프로젝트 로컬 실행 기능은 정상인데 서버 IP 액세스 후 영상/음성 통화를 정상적으로 사용할 수 없습니다.

- **배경**: IM H5 Demo 로컬 실행 후, localhost를 사용하면 일반적으로 메시지 전송, 영상/음성 통화 기능을 구현할 수 있습니다. 프로젝트를 서버에 올리고 IP로 접속한 후, 텍스트 메시지 수발신, 콘솔 요청 반환은 정상 작동되고 콘솔은 이상이 없으나, 음성/영상 통화가 정상적으로 실행되지 않고 영상 이미지를 가져올 수 없습니다.
- **원인**: IM에서 음성/통화 영상은 TRTCCalling SDK를 사용하고, 사용자가 IP를 사용하여 액세스할 때는 HTTP 프로토콜을 사용하였기 때문입니다.
- **솔루션**: TRTCCalling SDK는 HTTPS 또는 localhost 환경에서 실행되어야 합니다.


[](id:integrated)
## 통합 문제

[](id:i1)
### calling 온라인 Demo NO_RESP으로 진입할 수 없습니다.
- **원인**: NO_RESP 이벤트 트리거 조건: 1-초대자 시간 초과, 2-초대 수신자 오프라인 상태.
- **솔루션**: 트리거 조건에 따라 이벤트 처리를 진행하시기 바랍니다.

[](id:i2)
### iPhone에서 WeChat 브라우저를 통해 calling을 열면 상대방의 목소리가 들리지 않습니다.
- 원인: 자동 재생이 제한되었습니다.
- 솔루션: calling 1.0.0 버전에서 해결되었습니다. calling 버전을 1.0.0 이상으로 업그레이드할 것을 권장합니다.

[](id:i3)
### TRTCCalling handup() "uncaught (in promise) TypeError: cannot read property 'stop' of null" 오류가 보고됩니다.
- **원인**: 사용자가 모니터링 이벤트 중에 handup()을 여러 번 호출하여, 완료되지 않은 상태로 hangup이 다시 트리거되었습니다.
- **솔루션**: 이벤트의 후속 작업 수신은 handup()을 한 번만 실행하면 됩니다. TRTCCalling 내부적으로 이미 해결되었습니다. 더 이상 hangup() 메소드를 실행할 필요가 없습니다.

[](id:i3)
### Chrome 90 최신 버전 브라우저 trtccalling.js에서 "지원되지 않습니다. TRTCClinet. 귀하의 브라우저는 이 애플리케이션과 호환되지 않습니다."가 표시됩니다.
- **원인**: IM 버전이 너무 낮고 점검 메커니즘이 없습니다.
- **솔루션**: IM 버전 업그레이드를 권장합니다.

[](id:4)
### 연결 중 "TypeError: Cannot read property 'getVideoTracks' of null"가 표시됩니다.

- **원인**: 사용자 수락 시, 사용자의 비디오 및 마이크 사용 권한을 받지 못했기 때문입니다.
- **솔루션**: startRemoteView, startLocalView 등 작업 디바이스 메소드 사용 시, 비동기화 메소드를 사용하거나 TRTCCaling 버전을 1.0.0으로 업그레이드할 것을 권장합니다.

[](id:i5)
### script를 사용하여 sdkAppid를 가져올 때, "TSignaling._onMessageReceived unknown bussinessID=undefined"가 표시됩니다.
- **상세 내용**: 동일 sdkAppid가 script로 도입되었고, script로 도입된 경우 통신 가능하나, npm 또는 Android/iOS로 도입된 경우는 통신되지 않으며, `TSignaling._onMessageReceived unknown bussinessID=undefined` 경고 메시지가 반환됩니다.
- **원인**: `bussinessId=undefined`는 해당 버전의 tsignaling 버전이 구 버전이며, 구 버전 신호에 문제가 있음을 의미합니다.
- **솔루션**: tsignaling 버전을 업그레이드하고, 도입 과정에서 **새 버전 tsignaling의 파일명은 `tsignaling-js`**임을 주의해야 합니다.


[](id:i6)
### 알림: "Uncaught ( in promise ) Error: createCustomMessage 인터페이스는 SDK ready 상태일 때 호출 가능합니다."

- **원인**: 초기화가 제대로 진행되지 않았습니다.
- **솔루션**: TRTCCalling 버전을 1.0.0으로 업그레이드하고, SDK_READY 이벤트를 수신하여 후속 작업을 진행합니다.


[](id:i7)
### 알림: "Uncaught ( in promise ) RTCError: duplicated play() call observed, please stop() firstly &lt;INVALID_OPERATION 0x1001&gt;"
- **원인**: 음성 전달 과정에서 startRemoteView 인터페이스를 호출하였기 때문입니다.
- **솔루션**: 음성 통화 과정에서 startRemoteView 작업을 취소합니다.

[](id:i8)
### 알림: "Uncaught ( in promise ) Error: inviteID is invalid or invitation has been processed"
- **상세 내용**: Web trtcccalling은 native와 통신됩니다. web에서 native를 호출하면 native 수신 후 web 카메라가 아직 활성화되지 않은 상태에서 로컬 미리보기 화면이 나오기 전 끊기고, native는 통화 페이지에 머무릅니다. `Uncaught ( in promise ) Error: inviteID is invalid or invitation has been processed` 오류 메시지가 반환됩니다.
- **원인**: 사용자 디바이스를 가져올 때 음성/영상 디바이스를 인증하지 않으면, 멀티미디어 통화 방에 입장할 수는 있지만, 끊을 때는 native가 종료 신호를 받을 수 없습니다.
- **솔루션**: calling의 1.0.0 버전에서 사전 획득 진행 및 획득 실패한 경우, 사용자는 통화에 접속할 수 없습니다. calling을 1.0.0 및 이후 버전으로 업그레이드할 것을 권장합니다.

[](id:i9)
### 발신자가 성공적으로 호출한 후 수신자가 로그를 출력했지만(호출을 받았어야 함) handleNewInvitationReceived 콜백이 없습니다.

- **원인**: TRTCCalling <= 0.6.0 및 Tsignaling <= 0.3.0 버전이 너무 낮습니다.
- **솔루션**: TRTCCalling 및 Tsignaling을 최신 버전으로 업그레이드합니다.
