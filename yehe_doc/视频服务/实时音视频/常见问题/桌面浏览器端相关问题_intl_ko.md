<span id="que1"></span>
### 데스크톱 브라우저 SDK는 어떤 브라우저를 지원합니까?	
현재 데스크톱 Chrome 브라우저, 데스크톱 Edge 브라우저, 데스크톱 Firefox 브라우저, 데스크톱 Safari 브라우저, 모바일 Safari 브라우저에서 비교적 완벽하게 지원되며, 기타 플랫폼(예: Android 플랫폼 브라우저)에서의 지원은 완전하지 못할 수 있습니다. 자세한 내용은 [지원 플랫폼](https://intl.cloud.tencent.com/document/product/647/35143)을 참조하십시오.
브라우저에서 [WEBRTC 능력 테스트](https:///web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)를 열어 WebRTC 기능을 완벽하게 지원하는지 테스트할 수 있습니다.

<span id="que2"></span>
### TRTC의 데스크톱 브라우저와 PC는 동기화됩니까?
동기화됩니다. TRTC는 모든 플랫폼의 통신을 지원합니다.

<span id="que3"></span>
### TRTC Native SDK에는 클라우드 혼합 스트리밍 인터페이스가 있는데, 데스크톱 브라우저에서는 클라우드 혼합 스트리밍을 어떻게 사용할 수 있습니까?
데스크톱 브라우저에는 현재 클라이언트 인터페이스가 없습니다. 직접 LVB의 [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997) 인터페이스를 호출하여 혼합 스트리밍을 사용할 수 있습니다.

<span id="que4"></span>
### 데스크톱 브라우저 SDK 실행 시 “RtcError: no valid ice candidate found” 오류가 발생합니다. 어떻게 처리해야 합니까?

해당 오류는 TRTC 데스크톱 브라우저 SDK가 STUN 홀 펀칭 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC 데스크톱 브라우저 SDK는 다음 포트에 종속되어 데이터를 전송하며, 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
 - TCP 포트: 8687
 - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
 - 도메인: qcloud.rtc.qq.com

<span id="que5"></span>
### 클라이언트에서 "RtcError: ICE/DTLS Transport connection failed" 또는 “RtcError: DTLS Transport connection timeout” 오류가 발생합니다. 어떻게 처리해야 합니까?
해당 오류는 TRTC 데스크톱 브라우저 SDK가 MediaConnect 터널 구축 실패 시 발생합니다. 방화벽 설정을 확인해 주십시오. TRTC 데스크톱 브라우저 SDK는 다음 포트에 종속되어 데이터를 전송하므로, 해당 포트를 방화벽 화이트리스트에 추가하고 설정을 완료하십시오. [홈페이지 Demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html)에 액세스하여 설정이 적용되었는지 확인할 수 있습니다.
 - TCP 포트: 8687
 - UDP 포트: 8000, 8080, 8800, 843, 443, 16285
 - 도메인: qcloud.rtc.qq.com


<span id="que6"></span>
### TRTC 데스크톱 브라우저에서 화면 캡처 기능은 어떻게 사용합니까?
화면 캡처 기능은 인스턴스 HTMLVideoElement의 HTMLVideoElement.takeSnapshot에서 사용할 수 있습니다.
``` 
/*
 * params:
 *   DeviceObject device
 * return:
 *   null
 */
    var video = document.getElementById(""video"")
    video.takeSnapshot(function(data){
        var img = document.createElement('img');
        img.src = data;
        $(""#some_div_id"").append( img );
    });
```

<span id="que7"></span>
### 데스크톱 브라우저 SDK 로그에서 보고하는 NotFoundError, NotAllowedError, NotReadableError, OverConstrainedError, AbortError 오류 메시지는 각각 어떤 오류입니까?


 | 오류명               | 설명                                                                                                                        | 권장 처리사항                                                                                                                                                                                                                                                                                 |
 | -------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
 | NotFoundError        | 요청에 부합하는 매개변수의 미디어 유형(오디오, 비디오, 화면 공유 등)을 찾을 수 없는 경우입니다.<br>예: PC에 카메라가 없는데 브라우저에 비디오 스트리밍을 요청하는 경우 | 통화 전 사용자에게 통화에 필요한 카메라 또는 마이크 등의 디바이스가 있는지 확인을 요청하며, 카메라가 없고 음성 통화만 필요한 경우 [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream)에서 마이크만 사용하는 방법을 확인하십시오. |
 | NotAllowedError      | 사용자가 현재 브라우저 인스턴스의 오디오, 비디오, 화면 공유 액세스 요청을 거절한 상태입니다.                                                                  | 사용자에게 카메라/마이크의 액세스 권한 요청을 거절하면 멀티미디어 통화를 사용할 수 없다고 안내하십시오.                                                                                                                                                                                                                                    |
 | NotReadableError     | 사용자가 상응하는 디바이스의 권한을 허용하였으나 운영 체제의 일부 하드웨어, 브라우저 또는 웹 페이지 레이어로 인해 오류가 발생해 디바이스가 액세스할 수 없는 상태입니다.                        | 브라우저 오류 메시지에 따라 처리하고, 사용자에게 "일시적으로 카메라/마이크에 액세스할 수 없습니다. 현재 다른 애플리케이션에서 카메라/마이크에 액세스 요청을 하지 않았는지 확인한 후 다시 시도해 주십시오."라고 안내하십시오.                                                                                                                                                                   |
 | OverConstrainedError | cameraId/microphoneId 매개변수 값이 유효하지 않습니다.                                                                                        | cameraId/microphoneId 전송 값이 정확하고 유효한지 확인하십시오.                                                                                                                                                                                                                                            |
 | AbortError           | 알 수 없는 문제로 인해 디바이스를 사용할 수 없는 상태입니다.                                                                                        | -                                                                                                                                                                                                                                                                                        |


자세한 내용은 [initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize)를 참조하십시오.


<span id="que8"></span>
### 데스크톱 브라우저 SDK는 enableSmallVideoStream과 유사한 크기의 듀얼 채널 인코딩 모드를 지원합니까?	
현재는 지원하지 않습니다.

<span id="que9"></span>
### 데스크톱 브라우저 SDK 사용 중 카메라를 제거한 경우, 카메라 리스트 안에 있는 데이터는 어떻게 삭제합니까?
[getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.48566118.1562552652.1542703643#.getCameras)를 호출하여 신규 디바이스 리스트 획득을 시도해 볼 수 있습니다. 제거한 카메라 정보가 여전히 남아 있다면, 브라우저 기본 레이어에서 해당 리스트를 업데이트하지 않아 데스크톱 브라우저 SDK도 새로운 디바이스 리스트 정보를 얻을 수 없음을 의미합니다.

<span id="que10"></span>
### 데스크톱 브라우저 SDK에서 순수 오디오 푸시 스트리밍을 어떻게 녹화합니까? 콘솔에서 자동 릴레이와 자동 녹화를 설정했는데 녹화에 실패했습니다.	
[createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.212323796.1562552652.1542703643#.createClient)의 pureAudioPushMode 매개변수를 설정해야 합니다.

<span id="que11"></span>
### 데스크톱 브라우저 SDK에서 현재 음량 크기를 획득할 수 있습니까?
[getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?_ga=1.215278807.1562552652.1542703643#getAudioLevel)을 통해 현재 음량 크기를 획득할 수 있습니다.

<span id="que12"></span>
### 데스크톱 브라우저 화면 공유 팝업창 디자인을 변경할 수 있습니까?	
데스크톱 브라우저 화면 공유 팝업창의 디자인은 브라우저에서 관리하기 때문에 Web 페이지에서 변경할 수 없습니다.

<span id="que13"></span>
### 데스크톱 브라우저에서 설정한 푸시 스트리밍의 해상도는 모든 브라우저에서 동일하게 적용됩니까?
디바이스와 브라우저의 제한으로 인해 비디오 해상도는 완전하게 매칭되지 않을 수 있습니다. 이러한 경우 브라우저가 자동으로 Profile에 근접한 해상도로 조정합니다. 자세한 내용은 [setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#setVideoProfile)을 참조하십시오.

<span id="que14"></span>
### 데스크톱 브라우저 SDK가 정상적으로 디바이스(카메라/마이크) 리스트를 획득했는지 어떻게 알 수 있습니까?
1. 브라우저가 정상적으로 디바이스를 사용할 수 있는지 확인합니다.
페이지에서 직접 콘솔을 열어 `navigator.mediaDevices.enumerateDevices()`를 입력해 디바이스 리스트를 획득할 수 있는지 확인합니다.
 - 정상적으로 디바이스를 획득한 경우 Promise가 리턴되며, 안에 MediaDeviceInfo 객체 디지털 그룹이 나타납니다. 디지털 그룹 안의 모든 객체는 각각 사용 가능한 미디어 디바이스가 있습니다.
 - 열거에 실패한 경우 Promise가 rejected를 리턴하며, 이는 브라우저가 식별할 수 있는 디바이스가 없음을 의미하므로 브라우저 또는 디바이스를 점검해야 합니다.
2. 디바이스 리스트를 획득한 경우 `navigator.mediaDevices.getUserMedia({ audio: true, video: true })`를 입력하여 MediaStream 객체가 정상적으로 리턴되는지 확인합니다. 정상적으로 리턴되지 않으면 브라우저가 데이터를 획득할 수 없는 상태이므로 브라우저 설정을 점검해야 합니다.

<span id="que15"></span>
### 데스크톱 브라우저에서 에코와 잡음이 발생합니다. 어떻게 처리해야 합니까?
다른 곳에서 데스크톱 브라우저 소리에 에코, 잡음 등이 들리는 경우, 데스크톱 브라우저의 3A 처리가 유효하지 않다는 의미입니다.
WebRTC 표준에서 3A 알고리즘을 제공합니다. 지정된 audio의 MediaTrackConstrains 상의 AEC, ANS, AGC 스위치를 이용해 3A 처리를 제어할 수 있습니다. 에코, 잡음, 작은 음량 등의 문제가 발생하는 경우 데스크톱 브라우저의 localstream에서 creatStream 시 echoCancellation, noiseSuppression, autoGainControl의 세 가지 Attribute를 제어하여 에코 제거, 잡음 억제, 음량 확대를 진행할 수 있습니다.
다음 상황이 발생하면 브라우저와 하드웨어 디바이스가 호환되지 않는 것입니다. 디바이스 교체 또는 점검을 권장합니다.
- echoCancellation이 true로 설정되어 있으나 여전히 에코 문제가 존재하는 경우
- noiseSuppression이 true로 설정되어 있으나 여전히 배경에 잡음이 존재하는 경우
- autoGainControl이 true로 설정되어 있으나 여전히 음량이 너무 작은 경우

자세한 내용은 [미디어 추적 제한](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)을 참조하십시오.






<span id="que17"></span>
### Windows에서 공유된 애플리케이션의 재생 소리를 어떻게 캡처합니까?
[startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35131) 인터페이스를 호출하여 시스템 음성 수집을 활성화할 수 있습니다.

<span id="que18"></span>
### Windows 회의 모드에서 호스트가 관중에게 멀티미디어 연결 기능을 시작하려면 어떻게 해야 합니까?
다른 클라우드 서비스와 연결이 필요한 경우 [인스턴트 메시징 IM](https://intl.cloud.tencent.com/document/product/1047/33996)에서 연결을 요청해야 합니다.

로컬 비디오 데이터를 차단하여 호출의 대략적인 로직은 다음과 같습니다. A가 B에게 사용자 정의 정보 X를 발송하고 호출 페이지 알람을 설정하면, X 출력 효과를 자체적으로 처리하고 B가 X를 받은 후 호출된 페이지를 호출합니다. B가 [enterRoom](https://intl.cloud.tencent.com/document/product/647/35131)을 클릭해 방 안으로 들어가면 사용자 정의 정보 X1을 A에 발송하고 A가 X1(출력 여부 자체 결정)을 받음과 동시에 enterRoom을 호출해 방으로 들어갑니다. IM을 사용하여 사용자 정의 정보를 발송합니다.

<span id="que19"></span>
### 관중들이 어떻게 방 안에 있는 연결 화면을 볼 수 있나요?
관중이 라이브 방송 모드를 사용하는 경우, 관중이 방 안으로 들어가 TRTCCloudDelegate 상의 [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) 콜백을 통해 호스트의 userid(마이크 연결한 사람도 [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)으로 방에 들어갈 수 있으며, 관중에게는 해당 사용자가 호스트가 됨)를 알 수 있습니다. 그리고 관중이 [startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33a6e3765d6ca52d572224bc6e25dbcb) 호출해 호스트의 비디오 화면을 볼 수 있습니다.
자세한 조작 방법은 [라이브 방송 모드 실행(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)을 참조하십시오.

<span id="que20"></span>
### Web에서 리스너를 원격으로 퇴장시킬 수 있나요?
리스너 원격 퇴장 이벤트를 지원합니다. 클라이언트 이벤트 상의 [client.on('peer-leave')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html) 이벤트를 사용하여 원격으로 사용자에게 퇴장을 통지하는 것을 권장합니다.
