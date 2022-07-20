## 개요

사용자는 통화 중 장치 문제를 감지하기 어렵기 때문에 브라우저를 점검하고 카메라, 마이크 등의 장치를 테스트한 후 영상 통화를 시작하는 것을 권장합니다.

## 브라우저 점검

SDK의 통신 기능을 호출하기 전에 {@link TRTC.checkSystemRequirements checkSystemRequirements()} API를 사용하여 SDK가 사용자의 브라우저를 지원하는지 점검하는 것이 좋습니다. 브라우저가 지원되지 않는 경우 사용자의 장치 유형에 따라 지원되는 브라우저를 사용하도록 권장하십시오.

```javascript
TRTC.checkSystemRequirements().then(checkResult => {
  if (checkResult.result) {
    // 방 입장 지원 여부 점검
    if (checkResult.isH264DecodeSupported) {
    	// 풀 스트림 지원 여부 점검
    }
    if (checkResult.isH264EncodeSupported) {
    	// 스트림 푸시가 지원 여부 점검
    }
  }
})
```

⚠️ 사용자의 현재 브라우저가 SDK에서 지원되지만 `TRTC.checkSystemRequirements`에서 반환된 점검 결과가 false인 경우 다음 이유 중 하나 때문일 수 있습니다.

사례1: 링크가 다음 3가지 조건 중 하나를 충족하는 경우
- localhost 도메인( Firefox는 localhost 및 로컬 ip에 대한 액세스 지원 )
- HTTPS가 활성화된 도메인
- file:/// 프로토콜을 통해 열린 로컬 파일

사례2: Firefox 브라우저가 설치된 후 H264 코덱을 동적으로 로드해야 합니다. 따라서 검사 결과는 일시적으로 false가 됩니다. 잠시 기다렸다가 다시 시도하거나 다른 권장 브라우저를 사용하여 링크를 여십시오.


### 다른 브라우저에 대한 알려진 사용 제한

**Firefox**
- Firefox는 30 fps의 프레임 레이트만 지원합니다. 프레임 레이트를 설정해야 하는 경우 SDK에서 지원하는 다른 브라우저를 사용하십시오.

**QQ 브라우저**
- 일반 카메라와 마이크가 있는 특정 Windows 장치의 localhost 환경에서 localStream.initialize()를 호출하면 NotFoundError 오류가 발생할 수 있습니다.


## 멀티미디어 장치 테스트

사용자가 TRTC SDK로 좋은 사용자 경험을 할 수 있도록 사용자가 TRTC 방에 입장하기 전에 사용자의 장치 및 네트워크 상태를 점검하고 문제 해결 제안을 제공하는 것이 좋습니다.

다음 메소드를 참고하여 장치 및 네트워크 점검 기능을 통합할 수 있습니다.

- [rtc-detect의 JS 라이브러리](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-4)
- [장치 점검용 React 컴포넌트](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-5)
- [TRTC 기능 점검 페이지](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-6)

## rtc-detect 라이브러리

[rtc-detect](https://www.npmjs.com/package/rtc-detect)에서 TRTC SDK에 대한 현재 환경의 지원을 점검하고 현재 환경의 세부 정보를 볼 수 있습니다.

### 설치

```shell
npm install rtc-detect
```

### 사용 방법

```javascript
import RTCDetect from 'rtc-detect';
// 감지 모듈 초기화
const detect = new RTCDetect();
// 현재 환경의 감지 결과를 가져옴
const result = await detect.getReportAsync();
// result에는 현재 환경 시스템 정보, API 지원, 코덱 지원, 장치 정보가 포함됨
console.log('result is: ' + result);
```

### API

#### (async) isTRTCSupported()

이 API는 현재 환경이 TRTC를 지원하는지 점검하는 데 사용됩니다.

```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  console.log('current browser supports TRTC.')
} else {
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```

#### getSystem()

이 API는 현재 시스템 환경 매개변수를 가져오는 데 사용됩니다.

| Item                   | Type   | Description                     |
| ---------------------- | ------ | ------------------------------- |
| UA                     | string | 브라우저 ua                     |
| OS                     | string | 현재 장치의 운영 체제              |
| browser                | object | { name, version } 형식의 현재 브라우저 정보 |
| displayResolution      | object | { width, height } 형식의 현재 해상도    |
| getHardwareConcurrency | number | 현재 장치의 CPU 코어 수             |

```javascript
const detect = new RTCDetect();
const result = detect.getSystem();
```

#### getAPISupported()

이 API는 현재 환경의 API 지원을 얻는 데 사용됩니다.

| Item                              | Type    | Description                                           |
| --------------------------------- | ------- | ----------------------------------------------------- |
| isUserMediaSupported              | boolean | 사용자 미디어 데이터 스트림 획득 가능 여부                            |
| isWebRTCSupported                 | boolean | WebRTC 지원 여부                                       |
| isWebSocketSupported              | boolean | WebSocket 지원 여부                                    |
| isWebAudioSupported               | boolean | WebAudio 지원 여부                                     |
| isScreenCaptureAPISupported       | boolean | 화면 스트림 획득 가능 여부                                  |
| isCanvasCapturingSupported        | boolean | canvas에서 데이터 스트림 획득 가능 여부                          |
| isVideoCapturingSupported         | boolean | video에서 데이터 스트림 획득 가능 여부                           |
| isRTPSenderReplaceTracksSupported | boolean | track이 대체될 때 peerConnection과의 재협상을 생략할 수 있는지 여부     |
| isApplyConstraintsSupported       | boolean | 다시 getUserMedia를 호출하지 않고 카메라 해상도를 변경할 수 있는지 여부 |

```javascript
const detect = new RTCDetect();
const result = detect.getAPISupported();
```

#### (async) getDevicesAsync()

이 API는 현재 환경에서 사용 가능한 장치를 가져오는 데 사용됩니다.

| Item                    | Type                | Description                                        |
|-------------------------|---------------------|----------------------------------------------------|
| hasWebCamPermissions    | boolean             | 사용자 카메라 데이터 획득 가능 여부                                      |
| hasMicrophonePermission | boolean             | 사용자 마이크 데이터 획득 가능 여부                                      |
| cameras                 | array<CameraItem>   | 비디오 스트림에 대해 지원되는 해상도, 최대 너비, 최대 높이 및 최대 프레임 레이트(특정 브라우저만 해당)를 포함한 사용자 카메라 목록 |
| microphones             | array<DeviceItem>   | 사용자 마이크 목록                                         |
| speakers                | array<DeviceItem>   | 사용자 스피커 목록                                         |

**CameraItem**

| Item       | Type    | Description                                                          |
|------------|---------|----------------------------------------------------------------------|
| deviceId   | string  | 장치 ID, 일반적으로 고유하며 장치를 식별하는 데 사용할 수 있음                                              |
| groupId    | string  | 그룹 ID, 두 장치가 동일한 물리적 장치에 속하는 경우 동일한 그룹 ID를 갖음                                     |
| kind       | string  | 카메라 장치 유형: 'videoinput'                                                 |
| label      | string  | 장치를 설명하는 태그                                                             |
| resolution | object  | 카메라가 지원하는 최대 해상도 너비, 높이 및 프레임 레이트 {maxWidth: 1280, maxHeight: 720, maxFrameRate: 30} |

**DeviceItem**

| Item     | Type     | Description                          |
|----------|----------|--------------------------------------|
| deviceId | string   | 장치 ID, 일반적으로 고유하며 장치를 식별하는 데 사용할 수 있음             |
| groupId  | string   | 그룹 ID, 두 장치가 동일한 물리적 장치에 속하는 경우 동일한 그룹 ID를 갖음     |
| kind     | string   | 장치 유형, 예시: 'audioinput', 'audiooutput' |
| label    | string   | 장치를 설명하는 태그                             |

```javascript
const detect = new RTCDetect();
const result = await detect.getDevicesAsync();
```

#### (async) getCodecAsync()

이 API는 현재 환경의 코덱 지원을 얻는 데 사용됩니다.

| Item                  | Type    | Description        |
| --------------------- | ------- | ------------------ |
| isH264EncodeSupported | boolean | h264 인코딩 지원 여부 |
| isH264DecodeSupported | boolean | h264 디코딩 지원 여부 |
| isVp8EncodeSupported  | boolean | vp8 인코딩 지원 여부  |
| isVp8DecodeSupported  | boolean | vp8 디코딩 지원 여부  |
인코딩이 지원되는 경우 오디오/비디오를 게시할 수 있습니다. 디코딩이 지원되는 경우 재생을 위해 오디오/비디오를 가져올 수 있음

```javascript
const detect = new RTCDetect();
const result = await detect.getCodecAsync();
```

#### (async) getReportAsync()

이 API는 현재 환경의 탐지 보고서를 가져오는 데 사용됩니다.

| Item            | Type   | Description                       |
| --------------- | ------ | --------------------------------- |
| system          | object | getSystem()의 반환 값과 동일       |
| APISupported    | object | getAPISupported()의 반환 값과 동일 |
| codecsSupported | object | getCodecAsync()의 반환 값과 동일   |
| devices         | object | getDevicesAsync()의 반환 값과 동일 |

```javascript
const detect = new RTCDetect();
const result = await detect.getReportAsync();
```

#### (async) isHardWareAccelerationEnabled()

이 API는 Chrome 브라우저에서 하드웨어 가속이 활성화되어 있는지 점검하는 데 사용됩니다.

> !
> - 이 API의 구현은 기본 WebRTC API에 따라 다릅니다. isTRTCSupported를 호출한 후 점검을 위해 이 API를 호출하는 것이 좋습니다. 아래 테스트에 따라 점검하는 데 최대 30s가 소요될 수 있습니다.
>   1. 하드웨어 가속이 활성화된 경우 이 API는 Windows에서 약 2s, Mac에서 약 10s가 걸립니다.
>   2. 하드웨어 가속이 비활성화된 경우 이 API는 Windows 및 Mac 모두에서 약 30s가 걸립니다.


```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  const result = await detect.isHardWareAccelerationEnabled();
  console.log(`is hardware acceleration enabled: ${result}`);
} else {
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```


## 장치 점검을 위한 React 컴포넌트

### 장치 점검 UI 컴포넌트 기능

1. 장치 연결 및 로직 처리 점검

2. 네트워크 점검 로직 처리

3. 네트워크 점검 tab(옵션)

4. 중국어 및 영어 지원

### 장치 점검 UI 컴포넌트 링크

컴포넌트의 npm 패키지를 사용하는 방법에 대한 자세한 내용 참고: [rtc-device-detector-react](https://www.npmjs.com/package/rtc-device-detector-react)

컴포넌트의 소스 코드를 디버깅 방법에 대한 자세한 내용 참고: [github/rtc-device-detector](https://github.com/FTTC/rtc-device-detector)

컴포넌트를 가져오는 방법에 대한 자세한 내용 참고: [WebRTC API Example](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/index.html)

### 장치 점검 UI 컴포넌트 페이지

<img src="https://qcloudimg.tencent-cloud.cn/raw/d4868199e58d757c56a6e69fd58f93a9.png" alt="img" style="zoom:52%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/a7f8aab8091da5b8147d68c493271521.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/e87cc19b7f8bf90bc23a9dce9e00d5dc.png" alt="img" style="zoom:87%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ff35e633d69acffac15ebe27cb6c9cc.png" alt="img" style="zoom:77%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/d4227a2d69cf209a57f395918831873b.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ca749ec2d4fc52728c2a478a6067d83.png" alt="img" style="zoom:87%;" />

### 장치 및 네트워크 점검 로직

#### 1) 장치 연결

 장치 연결의 목적은 사용자의 장치에 카메라, 마이크, 스피커가 있고 네트워크에 연결되어 있는지 점검하는 것입니다. 카메라와 마이크가 있는 경우 시스템은 오디오/비디오 스트림을 가져오려고 시도하고 사용자에게 카메라와 마이크에 대한 액세스 권한을 부여하라는 메시지를 표시합니다.

+ 기기에 카메라, 마이크, 스피커가 있는지 점검

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  const cameraList = await TRTC.getCameras();
  const micList = await TRTC.getMicrophones();
  const speakerList = await TRTC.getSpeakers();
  const hasCameraDevice = cameraList.length > 0;
  const hasMicrophoneDevice = micList.length > 0;
  const hasSpeakerDevice = speakerList.length > 0;
  ```

+ 카메라 및 마이크 액세스 권한 획득

  ```javascript
  navigator.mediaDevices
    .getUserMedia({ video: hasCameraDevice, audio: hasMicrophoneDevice })
    .then((stream) => {
    	// 오디오/비디오 스트림 가져오기 성공
      // ...
    	// 카메라와 마이크 릴리스
     	stream.getTracks().forEach(track => track.stop());
    })
    .catch((error) => {
      // 오디오/비디오 스트림 가져오기 실패
    });
  ```

+ 장치가 네트워크에 연결되어 있는지 점검

  ```javascript
  export function isOnline() {
    const url = 'https://web.sdk.qcloud.com/trtc/webrtc/assets/trtc-logo.png';
    return new Promise((resolve) => {
      try {
        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
          resolve(true);
        };
        xhr.onerror = function () {
          resolve(false);
        };
        xhr.open('GET', url, true);
        xhr.send();
      } catch (err) {
        // console.log(err);
      }
    });
  }
  const isOnline = await isOnline();
  ```



#### 2) 카메라 점검

카메라 점검은 선택된 카메라가 캡쳐한 영상 스트림을 사용자가 카메라를 정상적으로 사용할 수 있는지 판단할 수 있도록 렌더링하는 것입니다.

+ 카메라 목록을 가져옵니다. 기본적으로 목록의 첫 번째 장치가 기본적으로 사용됨

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let cameraList = await TRTC.getCameras();
  let cameraId = cameraList[0].deviceId;
  ```

+ 비디오 스트림을 초기화하고 ID가 camera-video인 dom 요소에서 재생

  ```javascript
  const localStream = TRTC.createStream({
    video: true,
    audio: false,
    cameraId,
  });
  await localStream.initialize();
  localStream.play('camera-video');
  ```

+ 사용자가 카메라를 전환한 후 스트림 업데이트

  ```javascript
  localStream.switchDevice('video', cameraId);
  ```

+ 장치 연결/분리 시 수신

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    cameraList = await TRTC.getCameras();
      cameraId = cameraList[0].deviceId; 
    localStream.switchDevice('video', cameraId);
  })
  ```

+ 점검 완료 후 카메라 해제

  ```javascript
  localStream.close();
  ```



#### 3) 마이크 점검

마이크 점검은 선택한 마이크가 캡처한 오디오 스트림의 볼륨을 렌더링하여 사용자가 마이크를 정상적으로 사용할 수 있는지 판단하는 데 도움이 됩니다.

+ 마이크 목록을 가져옵니다. 기본적으로 목록의 첫 번째 장치가 사용됨

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let microphoneList = await TRTC.getMicrophones();
  let microphoneId = microphoneList[0].deviceId;
  ```

+ 오디오 스트림을 초기화하고 ID가 audio-container인 dom 요소에서 재생

  ```javascript
  const localStream = TRTC.createStream({
    video: false,
    audio: true,
    microphoneId,
  });
  await localStream.initialize();
  localStream.play('audio-container');
  timer = setInterval(() => {
    const volume = localStream.getAudioLevel();
  }, 100);
  ```

+ 사용자가 마이크를 전환한 후 스트림 업데이트

  ```javascript
  // 사용자가 선택한 새로운 microphoneId 가져오기
  localStream.switchDevice('audio', microphoneId);
  ```

+ 장치 연결/분리 시 수신

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    microphoneList = await TRTC.getMicrophones();
      microphoneId = microphoneList[0].deviceId;
    localStream.switchDevice('audio', microphoneId);
  })
  ```

+ 점검 완료 후 마이크에서 손을 떼고 볼륨으로 수신 중지

  ```javascript
  localStream.close();
  clearInterval(timer);
  ```



#### 4) 스피커 점검

스피커 점검은 사용자가 오디오를 재생하여 선택한 스피커를 정상적으로 사용할 수 있는지 점검할 수 있는 오디오 플레이어를 제공합니다.

+ mp3 플레이어를 제공하고 사용자에게 장치 재생 볼륨을 높이고 mp3 파일을 재생하여 스피커가 정상인지 점검하라는 메시지를 표시합니다.

  ```html
  <audio id="audio-player" src="xxxxx" controls></audio>
  ```

+ 점검 완료 후 재생 중지

  ```javascript
  const audioPlayer = document.getElementById('audio-player');
  if (!audioPlayer.paused) {
      audioPlayer.pause();
  }
  audioPlayer.currentTime = 0;
  ```



#### 5) 네트워크 점검

+ [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)를 호출하여 uplinkClient 및 downlinkClient의 두 Client를 생성합니다.

+ 두 Client가 같은 방에 들어가도록 합니다.

+ 스트림을 푸시하려면 uplinkClient를 사용하십시오. [ClientEvent.NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 수신하고 업스트림 네트워크 품질을 점검하십시오.

+ downlinkClient를 사용하여 스트림을 가져옵니다. [ClientEvent.NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) 이벤트를 수신하고 다운스트림 네트워크 품질을 점검하십시오.

+ 전체 프로세스는 약 15s 동안 지속되며 평균 네트워크 품질은 결국 업스트림 및 다운스트림 네트워크 품질을 평가하는 데 사용됩니다.

> !  점검 절차에 따라 소정의 [기본 서비스 요금](https://cloud.tencent.com/document/product/647/17157#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1)이 발생할 수 있습니다. 푸시 해상도가 지정되지 않은 경우 스트림은 기본적으로 640*480 해상도로 푸시됩니다.

```javascript
let uplinkClient = null; // 업스트림 네트워크 품질 점검
let downlinkClient = null; // 다운스트림 네트워크 품질 점검
let localStream = null; // 테스트용 스트림
let testResult = {
  // 업스트림 네트워크 품질 데이터 기록
  uplinkNetworkQualities: [],
  // 다운스트림 네트워크 품질 데이터 기록
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. 업스트림 네트워크 품질 점검
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppId 입력
    userId: 'user_uplink_test',
    userSig: '', // uplink_test의 userSig
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // 실제 비즈니스 시나리오를 기반으로 video profile 설정
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // 테스트를 위한 방으로 들어갑니다. 충돌을 피하기 위해 방 ID는 무작위여야 합니다.
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. 다운스트림 네트워크 품질 점검
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppId 입력
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
		// 성공적인 구독 후 네트워크 품질 이벤트 수신 시작
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // 테스트를 위한 방으로 들어갑니다. 충돌을 피하기 위해 방 ID는 무작위여야 합니다.
  await downlinkClient.join({ roomId: 8080 });
}

// 3. 점검 시작
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. 15s 후에 점검을 중지하고 평균 네트워크 품질 계산
setTimeout(() => {
  // 평균 업스트림 네트워크 품질 계산
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // 평균 다운스트림 네트워크 품질 계산
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // 점검이 종료됩니다. 관련 상태를 지우십시오.
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## TRTC 호환성 점검 페이지

[TRTC 점검 페이지](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)에서 현재 TRTC SDK를 사용하고자 하는 환경을 점검할 수 있습니다. 보고서 생성을 클릭하여 환경 점검 및 문제 해결을 위한 현재 환경 보고서를 얻을 수도 있습니다.

