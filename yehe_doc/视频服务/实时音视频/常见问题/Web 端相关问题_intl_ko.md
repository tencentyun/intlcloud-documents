[](id:que1)
###  Web SDK를 지원하는 브라우저는 무엇입니까? 
현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android 플랫폼 브라우저)에서의 지원은 완전하지 못할 수 있습니다. 자세한 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/41664)을 참고하십시오.
브라우저에서 [WEBRTC 기능 테스트](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능을 완벽하게 지원하는지 테스트할 수 있습니다.

[](id:que2)
###  Web, 미니프로그램, PC TRTC는 서로 통신할 수 있습니까?
네. TRTC는 모든 플랫폼의 통신을 지원합니다.

[](id:que3)
###  TRTC Native SDK에는 클라우드 혼합 스트림 API가 있지만 Web, 미니프로그램용 TRTC SDK로 클라우드 혼합 스트림 기능을 구현하려면 어떻게 해야 합니까?
Web에는 현재 클라이언트 인터페이스가 없습니다. 직접 CSS의 [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997) 인터페이스를 호출하여 혼합 스트리밍을 사용할 수 있습니다.

[](id:que4)
### Web SDK 실행 시 “RtcError: no valid ice candidate found” 오류가 발생합니다. 어떻게 처리해야 합니까?

해당 오류는 TRTC Web SDK가 STUN 홀 펀칭 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC Web SDK는 다음 포트에 종속되어 데이터를 전송하며, 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [공식 Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html)에서 설정이 적용되었는지 확인할 수 있습니다.
 - TCP 포트: 8687
 - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
 - 도메인: qcloud.rtc.qq.com

[](id:que5)
### 클라이언트에서 "RtcError: ICE/DTLS Transport connection failed" 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 합니까?
해당 오류는 TRTC Web SDK의 MediaConnect 터널 구축 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC Web SDK는 다음 포트에 종속되어 데이터를 전송하므로, 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [공식 Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html)에서 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
 - TCP 포트: 8687
 - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
 - 도메인: qcloud.rtc.qq.com


[](id:que6)
###  TRTC Web 버전에서 화면 캡처 기능을 구현하는 방법은 무엇입니까?
[Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#getVideoFrame)인터페이스를 참고하시기 바랍니다.

[](id:que7)
### Web SDK 로그에서 보고하는 NotFoundError, NotAllowedError, NotReadableError, OverConstrainedError, AbortError 오류 메시지는 각각 어떤 오류입니까?


| 오류 이름 | 설명 | 해결 방법 |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | 요청에 맞는 매개변수의 미디어 유형(오디오, 비디오, 화면 공유 등)을 찾을 수 없는 경우입니다.<br>예를 들어, PC에 카메라가 없는데 브라우저에 비디오 스트림을 요청하는 경우, 오류 메세지를 보고합니다. | 통화 전 사용자에게 통화에 필요한 카메라 또는 마이크 등의 디바이스가 있는지 확인을 요청하고, 카메라가 없고 음성 통화만 필요한 경우, [TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)에서 마이크만 사용하는 방법을 확인하십시오. |
| NotAllowedError | 사용자가 현재 브라우저 인스턴스의 오디오, 비디오, 화면 공유 액세스 요청을 거절한 상태입니다. | 사용자에게 카메라/마이크의 액세스 권한 요청을 거절하면 멀티미디어 통화를 사용할 수 없다고 안내하십시오. |
| NotReadableError     | 사용자가 상응하는 디바이스의 권한을 허용하였으나 운영 체제의 일부 하드웨어, 브라우저 또는 웹 페이지 레이어로 인해 오류가 발생해 디바이스가 액세스할 수 없는 상태입니다.                        | 브라우저 오류 메시지에 따라 처리하고, 사용자에게 "일시적으로 카메라/마이크에 액세스할 수 없습니다. 현재 다른 애플리케이션에서 카메라/마이크에 액세스 요청을 하지 않았는지 확인한 후 다시 시도해 주십시오."라고 안내하십시오.                                                                                                                                                                   |
| OverConstrainedError | cameraId/microphoneId 매개변수 값이 유효하지 않습니다. | cameraId/microphoneId 전송 값이 정확하고 유효한지 확인하십시오. |
| AbortError | 알 수 없는 문제로 인해 디바이스를 사용할 수 없는 상태입니다. | - |


자세한 내용은 [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)를 참고하십시오.


[](id:que8)
### Web SDK는 enableSmallVideoStream과 유사한 크고 작은 화면 듀얼 채널 인코딩 모드를 지원합니까? 
현재는 지원하지 않습니다.

[](id:que9)
### Web SDK 사용 중 카메라를 제거한 경우, 카메라 리스트 안에 있는 데이터는 어떻게 삭제합니까?
[getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras)를 호출하여 신규 디바이스 리스트 획득을 시도해 볼 수 있습니다. 제거한 카메라 정보가 여전히 남아 있다면, 브라우저 기본 레이어에서 해당 리스트를 업데이트하지 않아 Web SDK도 새로운 디바이스 리스트 정보를 얻을 수 없음을 의미합니다.

[](id:que10)
### Web SDK에서 퓨어 오디오 푸시 스트리밍을 어떻게 녹화합니까? 콘솔에서 자동 릴레이와 자동 녹화를 설정했는데 녹화에 실패했습니다. 
[createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)의 pureAudioPushMode 매개변수를 설정해야 합니다.

[](id:que11)
### Web SDK에서 현재 볼륨 크기를 획득할 수 있습니까?
[getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)을 통해 현재 볼륨 크기를 획득할 수 있습니다.

[](id:que12)
###  TRTC Web SDK에서 화면 공유 팝업 창의 스타일을 변경할 수 있습니까?  
Web 화면 공유 팝업창의 디자인은 브라우저에서 관리하기 때문에 Web 페이지에서 변경할 수 없습니다.

[](id:que13)
### Web에서 설정한 푸시 스트리밍의 해상도는 모든 브라우저에서 동일하게 적용됩니까?
디바이스와 브라우저의 제한으로 인해 비디오 해상도는 완전하게 매칭되지 않을 수 있습니다. 이러한 경우 브라우저가 자동으로 Profile에 근접한 해상도로 조정합니다. 자세한 내용은 [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile)을 참고하십시오.

[](id:que14)
### Web SDK가 정상적으로 디바이스(카메라/마이크) 리스트를 획득했는지 어떻게 알 수 있습니까?
1. 브라우저가 정상적으로 디바이스를 사용할 수 있는지 확인합니다.
페이지에서 직접 콘솔을 열어 `navigator.mediaDevices.enumerateDevices()`를 입력해 디바이스 리스트를 획득할 수 있는지 확인합니다.
 - 정상적으로 디바이스를 획득한 경우 Promise가 리턴되며, 안에 MediaDeviceInfo 객체 디지털 그룹이 나타납니다. 디지털 그룹 안의 모든 객체는 각각 사용 가능한 미디어 디바이스가 있습니다.
 - 열거에 실패한 경우 Promise가 rejected를 리턴하며, 이는 브라우저가 식별할 수 있는 디바이스가 없음을 의미하므로 브라우저 또는 디바이스를 점검해야 합니다.
2. 디바이스 리스트를 획득한 경우 `navigator.mediaDevices.getUserMedia({ audio: true, video: true })`를 입력하여 MediaStream 객체가 정상적으로 리턴되는지 확인합니다. 정상적으로 리턴되지 않으면 브라우저가 데이터를 획득할 수 없는 상태이므로 브라우저 설정을 점검해야 합니다.

[](id:que15)
###  TRTC Web SDK의 에코 또는 노이즈는 어떻게 해결합니까?
다른 단말에서 Web 소리에 에코, 소음, 잡음 등이 들리는 경우, Web의 3A 프로세싱이 적용되지 않다는 의미입니다.

- 사용자 정의 수집에 브라우저의 기본 [getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia) API를 사용하는 경우 3A 매개변수를 수동으로 설정해야 합니다.
	- echoCancellation：에코 제거 스위치
	- noiseSuppression：소음 억제 스위치
	- autoGainControl：자동 이득 제어 스위치
>? 자세한 내용은 [미디어 추적 제한](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)을 참고하십시오.
- TRTC.createStream 인터페이스를 사용하여 수집하는 경우 3A 매개변수를 수동으로 설정할 필요가 없으며 SDK는 기본적으로 3A를 활성화합니다.


[](id:que16)
### Web에서 방 퇴장을 원격 수신할 수 있습니까?
방 퇴장 이벤트의 원격 수신을 지원합니다. 클라이언트 이벤트 중 [client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html) 이벤트를 사용하여 원격으로 사용자에게 퇴장을 통지할 것을 권장합니다.
