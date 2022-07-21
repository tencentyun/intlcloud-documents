## 시나리오의 문제점 및 솔루션
화면 공유 등 응용 시나리오에서는 시스템 오디오를 상대방에게 공유해야 하는 상황이 종종 발생하지만, Mac 컴퓨터의 사운드 카드는 애플리케이션이 Electron에 의해 패키징될 때 시스템 오디오 캡처를 허용하지 않아 Mac 컴퓨터에서 시스템 오디오를 공유할 수 없습니다. 이 문제를 해결하기 위해 TRTC는 Mac 컴퓨터에서 시스템 오디오를 녹음하는 기능을 도입했습니다. 구체적인 활성화 방법은 다음과 같습니다.

[](id:step1)
### 1단계: 시스템 오디오 수집 시작

[startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) API를 호출하여 시스템 오디오 캡처를 시작하고 오디오를 업스트림 오디오 스트림에 믹싱합니다. 결과는 [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError)를 통해 다시 호출됩니다.
```javascript
import TRTCCloud, { TRTCAudioQuality } from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
function onSystemAudioLoopbackError(errCode) {
  if (errCode === 0) {
    console.log('실행 성공');
  }
  if (errCode === -1330) {
    console.log('시스템 사운드 녹음 활성화 실패, 예: 오디오 드라이버 플러그 인 사용 불가');
  }
  if (errCode === -1331) {
    console.log('오디오 드라이버 플러그 인 설치 권한 없음');
  }
  if (errCode === -1332) {
    console.log('오디오 드라이버 플러그 인 설치 실패');
  }
}

trtcCloud.on('onSystemAudioLoopbackError', onSystemAudioLoopbackError);
trtcCloud.startLocalAudio(TRTCAudioQuality.TRTCAudioQualityDefault);
trtcCloud.startSystemAudioLoopback();


```

>! 처음 startSystemAudioLoopback을 호출하면 SDK는 아래와 같이 root 액세스를 요청합니다. **예**를 클릭하면 버추얼 사운드 카드 플러그 인을 컴퓨터에 자동으로 설치하기 시작합니다.  

[](id:step2)

### 2단계: 시스템 오디오 수집 중지 
[stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback) API를 호출하여 시스템 오디오 캡처를 중지합니다.
```javascript
trtcCloud.stopSystemAudioLoopback();
```

[](id:step3)
### 3단계: 시스템 사운드 수집 음량 설정
[setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/en-us/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume) API를 호출하여 시스템 오디오 캡처 볼륨을 설정합니다.

```javascript
trtcCloud.setSystemAudioLoopbackVolume(60);
```

## 결론
TRTC는 Mac에서 버츄얼 사운드 카드 플러그 인 `TRTCAudioPlugin.driver`를 통해 시스템 오디오를 녹음합니다. 이 버츄얼 사운드 카드 플러그 인은 시스템 디렉터리 `/Library/Audio/Plug-Ins/HAL`에 복사하여 오디오 서비스를 재시작하면 적용됩니다. `실행`의 `기타` 폴더에 있는 `오디오 MIDI 설정` 애플리케이션으로 버츄얼 사운드 카드 플러그 인이 정상적으로 설치되었는지 확인할 수 있으며, 해당 애플리케이션의 디바이스 리스트에 'TRTC Audio Device'가 있으면 TRTC 버츄얼 사운드 카드 플러그 인이 정상적으로 설치된 것입니다.  
