>!다음 FAQ는 3.x.x 버전의 TRTC Web SDK에 적용됩니다.

### 현재 브라우저가 WebRTC를 지원하는지 어떻게 확인합니까?
WebRTCAPI.fn.detectRTC를 사용하여 확인할 수 있습니다. 피드백이 false일 경우 비즈니스에서 오류 알림 페이지를 제공하여 사용자가 지원하는 환경에서 사용할 수 있도록 해야 합니다. 특별한 상황일 경우 다음 방법을 통해 처리할 수 있습니다.
- [능력 점검 페이지](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html)를 열어 점검합니다.
-[티켓 제출](https://console.cloud.tencent.com/workorder/category)을 통해 도움을 요청합니다.

### 하울링(Squeak 또는 중복음)이 발생했습니다. 어떻게 처리해야 합니까?
Demo(Web)에 로컬 video/audio에 대해 muted Attribute가 설정되어 있습니다. 즉, 로컬 비디오 스트리밍의 음소거 재생이 설정된 상태입니다. 별도의 설정을 거치지 않을 경우 로컬 비디오 스트리밍의 사운드가 오디오 입력 소스가 되어 “하울링” 또는 “중복음” 문제를 야기합니다.

```html
	<video muted autoplay playsinline></video>

	<audio muted autoplay playsinline></audio>
```

>?2개의 모바일(Android 또는 iOS)을 사용하여 근거리 테스트를 실시할 경우 “하울링” 또는 “중복음” 문제가 발생할 수 있습니다. 둘 중 하나에서 캡처 및 재생을 음소거하면 됩니다.

### 오디오를 한참 후에 들을 수 있습니다. 어떻게 해야 합니까?
퓨어 오디오를 사용하고 있을 경우 video가 아니라 audio 태그를 사용하여 오디오 스트리밍을 로딩합니다.

### Android WeChat/모바일 QQ를 정상적으로 사용할 수 없습니다. 어떻게 해야 합니까?
[점검 툴](http://debugx5.qq.com/)을 사용하여 TBS 설치/업데이트 성공 여부를 확인합니다. 실패한 경우 TBS를 다시 설치합니다.

### on set remote sdp failed(아래 이미지)가 나타나는 이유는 무엇입니까?
![](https://main.qcloudimg.com/raw/45f5395173438ebb5894d45197828ac5.png)
webrtcapi 인스턴스화 방법에서 매개변수 closeLocalMedia는 자동 푸시 스트리밍 차단 여부를 나타냅니다. 해당 매개변수가 false(기본 false)일 경우 startWebRTC를 호출하면 이런 문제가 발생하게 됩니다.

### 휴대폰의 배터리 사용량이 유난히 많습니다. 어떻게 해결해야 합니까?
비디오는 코딩/디코딩이 필요하며, 코딩/디코딩 작업 자체가 배터리 소모가 많습니다. 페이지에서 푸시 스트리밍/시청을 하지 않았는데도 배터리 소모가 많을 경우 차단 스트리밍 콜백에서 video의 srcObject를 초기화하지 않았는지 확인합니다.

```javascript
    videoElement.srcObject = null
```

### SecurityError[보안 오류]가 발생했습니다. 어떻게 처리해야 합니까?
해당 오류는 멀티미디어를 정확하게 획득할 수 없을 때 나타납니다.
WebRTC는 반드시 HTTPS 또는 localhost 페이지에서 열려야 합니다. 그렇지 않을 경우 멀티미디어 디바이스를 획득할 수 없습니다.

### NotAllowedError[불허 오류]가 발생했습니다. 무슨 의미입니까?
해당 오류는 사용자가 멀티미디어 디바이스 획득 요청을 거절할 경우 나타납니다.

### OverConstrainedError[조건 충족 불가 오류]가 발생했습니다. 어떻게 처리해야 합니까?
해당 오류는 지정된 조건을 디바이스가 만족하지 못함을 의미합니다. `OverconstrainedError` 유형의 객체이며 constraint Attribute를 가지고 있는데 이 Attribute에는 현재 부합하지 않는 constraint가 포함되어 있습니다. 여러 개의 Tab 페이지를 열어 동시에 푸시 스트리밍할 경우 해상도 캡처가 일치해야 합니다.

###  NotFoundError[찾지 못함 오류]가 발생했습니다. 무슨 의미입니까?
해당 오류는 요청 매개변수에 부합하는 미디어 유형을 찾지 못했을 때 나타납니다.

###  사용자에게 라이선스를 할당했는데 NotReadableError[판독 불가 오류]가 발생한 이유는 무엇입니까?
사용자가 해당 디바이스 라이선스를 보유하고 있으나 운영 체제의 하드웨어, 브라우저 또는 웹에서 오류가 발생하여 디바이스에 접근할 수 없을 때 나타납니다.

### AbortError[중지 오류]가 발생하는 이유는 무엇입니까?
사용자와 운영 체제 모두 디바이스 하드웨어에 접근할 권한이 있으며 `NotReadableError`와 같은 하드웨어로 인한 문제가 발생하지 않았다면, 어떠한 특정 문제로 인해 디바이스를 사용할 수 없어 AbortError[중지 오류]가 나타나게 된 것입니다.

### TypeError[유형 오류]가 발생하는 이유는 무엇입니까?
constraints 객체를 설정하지 않았거나 false로 설정되었을 때 나타납니다.

### 소리가 들리지 않습니다. 어떻게 해결해야 합니까?
브라우저에는 기본적으로 음성 출력 디바이스가 사용되고 있습니다. 음성 출력 디바이스를 조정하고 전력 증폭기가 아닌 다른 디바이스 사용을 잠시 중단하여 정상 여부를 확인합니다.

### Electron 개발 시 비디오 통화를 진행할 수 없습니다. 어떻게 해결해야 합니까?
Electron을 사용하고 있으며 Mac App Store에 제출한 후 비디오 통화를 진행할 수 없다면 entitlements.plist 파일에 `com.apple.securite.network.server`를 추가하십시오.

### dom tree 다시 그리기(Repaint)로 인한 블랙 스크린 현상을 어떻게 해야 막을 수 있습니까?
react/vue/angular를 사용하고 있다면 video와 stream의 관계는 js를 통해 제어됩니다. 데이터 변경으로 인해 페이지가 변할 경우 video와 stream의 관계를 다시 바인딩해야 하며 그렇지 않을 경우 블랙 스크린 현상이 나타납니다.

### iOS에서 블랙 스크린 현상이 나타나는 이유는 무엇입니까?
- react/vue/angular를 사용하고 있다면 동적으로 생성된 video는 브라우저에서 자동으로 재생할 수 없습니다.
- 관객 모드를 사용하면서 푸시 스트리밍을 진행하지 않으면 iOS에서 음성이 있는 비디오의 자동 재생을 허용하지 않습니다. 또한 원격 비디오 스트리밍도 자동으로 재생할 수 없습니다. onRemoteStreamUpdate 이벤트 프로세스 함수에서 원격 스트리밍을 video 태그에 바인딩한 후 video.play()를 추가해야 합니다.


### 마이크 종료/음소거 후에도 데이터 패키지가 있는 이유는 무엇입니까?
마이크 종료 또는 음소거 후에도 음소거 패키지가 있습니다.

### 카메라 종료 후에도 데이터 패키지가 있는 이유는 무엇입니까?
카메라 종료 후에도 블랙 스크린 패키지가 있습니다.

