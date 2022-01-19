## 1. 기본 환경 문제
[](id:b1)
### Web SDK는 어떤 브라우저를 지원합니까?
TRTC Web SDK의 브라우저 지원에 대한 자세한 내용은 [TRTC Web SDK 브라우저 지원](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)을 참고하십시오.
위에 나열되지 않은 시나리오의 경우 현재 브라우저에서 [TRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능이 완벽하게 지원되는지 테스트할 수 있습니다.

[](id:b2)
### 통화 전 오디오/비디오 디바이스 테스트 방법은 무엇입니까?
[통화 전 환경 및 디바이스 점검](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html)을 참고하십시오.

[](id:b3)
### 현재 네트워크 상황을 실시간으로 점검하는 방법은 무엇입니까?
자세한 내용은 [통화 전 네트워크 품질 점검](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)을 참고하십시오.

[](id:b4)
### TRTC Web SDK를 로컬 개발 테스트에 정상적으로 사용할 수 있지만 온라인 배포 시에는 사용할 수 없는 이유는 무엇입니까?

사용자의 안전과 개인 정보 보호를 위해 브라우저는 웹 페이지에서 마이크와 카메라를 안전한 환경(예: `https`, `localhost`, `file://` 및 기타 프로토콜)에서만 수집하도록 제한합니다. HTTP 프로토콜은 안전하지 않으며, 브라우저는 HTTP 프로토콜을 통해 미디어 장치를 수집하는 것을 금지합니다.

로컬에서 개발 테스트를 하면 모든 것이 정상이지만, 페이지가 배포된 후에는 카메라와 마이크를 정상적으로 수집할 수 없는 경우, 웹 페이지가 HTTP 프로토콜에 배포되었는지 확인하십시오. 확인 결과 맞다면, HTTPS를 사용하여 웹 페이지를 배포하고 인증된 HTTPS 보안 인증서가 있는지 확인하십시오.

자세한 내용은 [URL 도메인 및 프로토콜 제한 설명](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html#h2-2)을 참고하십시오.

[](id:b5)
### 혼합 스트림, 릴레이 푸시 스트림, 대/소형 스트림, 뷰티 필터, 워터마크가 지원됩니까?
[혼합 스트림](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode), [릴레이 푸시 스트림](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html), [대/소형 스트림](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html), [뷰티 필터](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html), [워터마크](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-29-advance-water-mark.html) 문서를 참고하여 고급 기능을 구현할 수 있습니다.

[](id:b6)
### WebRTC의 기존 문제는 무엇이 있습니까?
자세한 내용은 [WebRTC 기존 문제 및 솔루션](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html)을 참고하십시오.

## 2. 푸시/풀 스트림 문제
[](id:p1)
### Web SDK 로그에서 보고하는 NotFoundError, NotAllowedError, NotReadableError, OverConstrainedError, AbortError 오류 메시지는 각각 어떤 오류입니까?
| 오류 이름 | 설명 | 해결 방법 |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | 요청에 맞는 매개변수의 미디어 유형(오디오, 비디오, 화면 공유 등)을 찾을 수 없는 경우입니다. 예를 들어, PC에 카메라가 없는데 브라우저에 비디오 스트림을 요청하는 경우, 오류 메세지를 보고합니다. | 통화 전 사용자에게 통화에 필요한 카메라 또는 마이크 등의 디바이스가 있는지 확인을 요청하고, 카메라가 없고 음성 통화만 필요한 경우, [TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)에서 마이크만 사용하는 방법을 확인하십시오. |
| NotAllowedError | 사용자가 현재 브라우저 인스턴스의 오디오, 비디오, 화면 공유 액세스 요청을 거절한 상태입니다.   | 사용자에게 카메라/마이크의 액세스 권한 요청을 거절하면 멀티미디어 통화를 사용할 수 없다고 안내하십시오.       |
| NotReadableError | 사용자가 상응하는 디바이스의 권한을 허용하였으나 운영 체제의 일부 하드웨어, 브라우저 또는 웹 페이지 레이어로 인해 오류가 발생해 디바이스가 액세스할 수 없는 상태입니다. | 브라우저 오류 메시지에 따라 처리하고, 사용자에게 “일시적으로 카메라/마이크에 액세스할 수 없습니다. 현재 다른 애플리케이션에서 카메라/마이크에 액세스 요청을 하지 않았는지 확인한 후 다시 시도해 주십시오.”라고 안내하십시오.|
| OverConstrainedError | cameraId/microphoneId 매개변수 값이 유효하지 않습니다. | cameraId/microphoneId 전송 값이 정확하고 유효한지 확인하십시오. |
| AbortError | 알 수 없는 문제로 인해 디바이스를 사용할 수 없는 상태입니다. | - |

자세한 내용은 [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)를 참고하십시오.

[](id:p2)
### 일부 휴대폰 브라우저에서 TRTC 푸시 스트림을 정상적으로 진행할 수 없습니다.
TRTC Web SDK의 브라우저 지원에 대한 자세한 내용은 [TRTC Web SDK 브라우저 지원](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)을 참고하십시오.
위에 나열되지 않은 시나리오의 경우 현재 브라우저에서 [TRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능이 완벽하게 지원되는지 테스트할 수 있습니다.

[](id:p3)
### Web에서 설정한 푸시 스트림 해상도는 모든 브라우저에서 동일하게 적용됩니까?
디바이스와 브라우저의 제한으로 인해 비디오 해상도가 완전하게 매칭되지 않을 수 있습니다. 이러한 경우 브라우저가 자동으로 Profile에 근접한 해상도로 조정합니다. 자세한 내용은 [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile)을 참고하십시오.

[](id:p4)
### Web 화면 공유 양식 수정은 지원됩니까?
화면 공유 양식은 브라우저가 제어하며, 현재 수정할 수 없습니다.

[](id:p5)
### Web에서의 혼합 스트림이 지원됩니까?
Web에서의 혼합 스트림은 지원됩니다. 자세한 내용은 [혼합 스트림 트랜스 코딩 인터페이스 호출 방법](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)을 참고하십시오.

[](id:p6)
### Web SDK 사용 중 카메라를 제거한 경우, 카메라 리스트 안에 있는 데이터는 어떻게 삭제합니까?
[TRTC.getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras)를 호출하여 신규 디바이스 리스트 획득을 시도해 볼 수 있습니다. 제거한 카메라 정보가 여전히 남아 있다면, 브라우저 기본 레이어에서 해당 리스트를 업데이트하지 않아 Web SDK도 새로운 디바이스 리스트 정보를 얻을 수 없음을 의미합니다.

[](id:p7)
### iOS 버전 WeChat 내장 브라우저에서 푸시 스트림을 정상적으로 진행할 수 없습니다.
[브라우저 지원 현황](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)을 참고하여 iOS 버전 WeChat 내장 브라우저의 푸시/풀 스트림 지원 현황을 확인하시기 바랍니다.

## 3. 재생 문제
[](id:v1)
### 오디오 및 비디오 통신 과정에서 화면은 표시되나 소리가 나오지 않습니다.
- 브라우저의 자동 재생 정책 제한으로 인해, 오디오 재생 시 PLAY_NOT_ALLOWED 예외가 발생합니다. 이 때 서비스 계층에서 오디오 재생 재개를 위해 사용자가 Stream.resume()을 수동으로 조작하도록 안내해야 합니다. 자세한 내용은 [자동 재생 제한 해결 방안](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)을 참고하십시오.
- 모니터링 대시보드를 통해 수발신 양측의 audioLevel & audioEnergy를 쿼리하여 알 수 없는 오류를 확인하십시오.

[](id:v2)
### Web 통화 화면이 표시되지 않습니다.
Web 페이지에서 데이터 획득 여부를 확인합니다. 데이터 송수신이 정상적이라면 `<video>` 요소의 srcObject 속성에 올바른 mediaStream 객체가 할당되었는지 확인합니다. 할당 오류인 경우 화면이 표시되지 않습니다.

[](id:v3)
### Web 통화 중에 에코, 잡음, 소음이 발생하거나 소리가 작습니다.
통화하는 양측의 디바이스가 너무 가까우면 정상적인 현상입니다. 테스트 시 서로 멀리 떨어져 주십시오. 다른 단말에서 Web측 소리에 에코, 잡음, 소음이 들리면, Web에서 3A 처리가 적용되지 않았음을 의미합니다.
사용자 정의 수집에 브라우저의 기본 [getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia) API를 사용하는 경우 3A 매개변수를 수동으로 설정해야 합니다.
- echoCancellation: 에코 제거 스위치
- noiseSuppression: 소음 억제 스위치
- autoGainControl: 자동 게인 제어

[TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream) 인터페이스로 수집하는 경우 3A 매개변수를 수동으로 설정할 필요 없이 SDK가 기본적으로 3A를 활성화합니다.

## 4. 기타
[](id:o0)
### SDK 2.x, 3.x 버전, Chrome 96+ 버전에서 정상적으로 통화가 안됩니다.
최신 버전의 [Chrome 96 Plan-B 폐기](https://www.chromestatus.com/feature/5823036655665152)로 인해 TRTC 구버전(2.x, 3.x) Web SDK 통화 불가가 발생할 수 있습니다. Web SDK를 최신 버전(4.x)으로 업그레이드 하시기 바랍니다. SDK 4.x 버전의 인터페이스는 이전 버전(2.x, 3.x)과 호환되지 않습니다. [빠른 통합(Web)](https://intl.cloud.tencent.com/document/product/647/35096)을 참고하여 SDK 4.x 버전으로 업그레이드하십시오.

[](id:o1)
###  Web SDK 실행 시 "RtcError: no valid ice candidate found" 오류가 발생합니다. 어떻게 해결해야 합니까?
해당 오류는 TRTC 데스크톱 브라우저 SDK가 STUN 홀 펀칭 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC 데스크톱 브라우저 SDK는 다음 포트에 종속되어 데이터를 전송하며, 해당 포트를 방화벽 얼로우리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html)를 통해 설정이 적용되었는지 확인할 수 있습니다.

자세한 내용은 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.

[](id:o2)
###  클라이언트에서 "RtcError: ICE/DTLS Transport connection failed" 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 합니까?
해당 오류는 TRTC 데스크톱 브라우저 SDK가 MediaConnect 터널 구축 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC 데스크톱 브라우저 SDK는 다음 포트에 종속되어 데이터를 전송하므로, 해당 포트를 방화벽 얼로우리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html)를 통해 설정이 적용되었는지 확인할 수 있습니다.

자세한 내용은 [방화벽 제한 대응 관련 질문](https://intl.cloud.tencent.com/document/product/647/35164)을 참고하십시오.


[](id:o3)
### Web SDK에서 현재 볼륨 크기를 획득할 수 있습니까?
현재 볼륨 크기는 [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)을 통해 획득할 수 있습니다. [카메라와 마이크 전환](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)을 참고하십시오.

[](id:o4)
### 어떤 상황에서 Client.on('client-banned')이 트리거 됩니까?

이 이벤트는 사용자가 강제 퇴장될 때 트리거됩니다. 예: 동일한 사용자 이름으로 동시 로그인 또는 [사용자 강제 퇴장](https://intl.cloud.tencent.com/document/product /647/34268) RESTAPI 호출.
>! 동일한 사용자 이름으로 동시 로그인하는 것은 허용되지 않으며, 이는 통화 양측 간에 통화 이상을 유발할 수 있습니다. 서비스 계층은 동일한 사용자 이름으로 동시 로그인하는 것을 피해야 합니다.

자세한 내용은 [CLIENT_BANNED 이벤트](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED)를 참고하십시오.

[](id:o5)
### Web에서 방 퇴장을 원격 수신할 수 있습니까?
방 퇴장 이벤트의 원격 수신을 지원합니다. 클라이언트 이벤트 중 [client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html) 이벤트를 사용하여 원격으로 사용자에게 퇴장을 통지할 것을 권장합니다.

[](id:o6)
### TRTC의 Web, PC 버전은 상호 통신이 됩니까?
네. TRTC는 모든 플랫폼의 통신을 지원합니다.

[](id:o7)
### TRTC Web 스크린샷 기능은 어떻게 구현합니까?
자세한 내용은 [Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#getVideoFrame) 인터페이스를 참고하시기 바랍니다.

[](id:o8)
### Web SDK에서 퓨어 오디오 푸시 스트리밍을 어떻게 녹화합니까? 콘솔에서 자동 릴레이와 자동 녹화를 설정했는데 녹화에 실패했습니다.
[createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)의 pureAudioPushMode 매개변수를 설정해야 합니다.

[](id:o9)
### Client.on(‘error’) 오류는 어떻게 해결합니까?
해당 오류는 SDK에 복구할 수 없는 오류가 발생했음을 나타냅니다. 서비스 계층에서 페이지를 새로고침하거나 Client.leave를 호출하여 퇴장한 뒤 Client.join을 다시 호출하여 재시도해보시기 바랍니다.

[](id:o10)
### 미니프로그램 및 Web에서 사용자 정의 스트림 ID가 지원됩니까?
Web 4.3.8 이상 버전은 사용자 정의 스트림 ID가 지원되므로 SDK를 업데이트하시기 바랍니다. 미니 프로그램은 현재 지원되지 않습니다.

[](id:011)
### Web 화면 공유 시 시스템 오디오를 어떻게 수집합니까?
구체적인 작업 방법은 [화면 공유 시스템 오디오 수집](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html#h2-6)을 참고하십시오.
현재 시스템 오디오 수집은 Chrome M74+만 지원하며, Windows 및 Chrome OS에서는 전체 시스템 오디오를 캡처할 수 있습니다. Linux 및 Mac에서는 탭의 오디오만 캡처할 수 있습니다. 그 외의 Chrome 버전, 기타 시스템 및 브라우저는 지원되지 않습니다.

[](id:012)
### Web에서 카메라와 마이크를 전환하는 방법은 무엇입니까?
먼저 시스템의 카메라 및 마이크 장치를 가져온 다음 [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)를 호출하여 전환할 수 있습니다. 구체적인 작업은 [카메라 및 마이크 전환](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)을 참고하십시오.
