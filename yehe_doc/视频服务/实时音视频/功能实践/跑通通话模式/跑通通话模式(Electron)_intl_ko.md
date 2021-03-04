## 적용 시나리오

TRTC는 4가지 입장 모드를 지원합니다. 그중 영상 통화(VideoCall)과 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/36070)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석

TRTC 클라우드 서비스는 '인터페이스'와 '프록시' 라는 상이한 서버 노드로 구성됩니다.

- **인터페이스**
    인터페이스 노드는 가장 우수한 회로와 고성능 기기를 채택하여 엔드 투 엔드의 마이크 통화 시 딜레이 시간이 짧고, 시간당 높은 과금이 적용됩니다.
- **프록시**
    프록시 노드는 일반 회로와 일반 성능의 기기를 채택하여 동시 접속에 의한 시청 수요를 충족할 수 있으며, 시간당 낮은 과금이 적용됩니다.

통화 모드에서 TRTC 방에 입장한 모든 사용자는 인터페이스를 할당받습니다. 각 사용자 모두가 '호스트'로서 언제든지 발언할 수 있어(업스트림 동시 접속 최대 50개) 온라인 회의 등 시나리오의 사용에 적합합니다. 단, 단일 방 참가자 수는 300명으로 제한됩니다.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드

[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)에 로그인하면 본 문서와 관련된 예시 코드를 받을 수 있습니다.

## 작업 순서

<span id="step1"></span>
### 1단계: 공식 홈페이지 SimpleDemo 실행

먼저 [SimpleDemo(Electron) 제작](https://intl.cloud.tencent.com/document/product/647/35089) 문서를 숙지한 뒤 가이드에 따라 공식 홈페이지 SimpleDemo를 실행하는 것을 권장합니다.

SimpleDemo가 정상 실행된다면 프로젝트에 Electron를 설치하는 것도 손쉽게 가능합니다.

반대로 SimpleDemo 실행에 장애가 있다면 높은 확률로 Electron의 다운로드와 설치가 원활치 않게 됩니다. 이 경우 Electron 공식 홈페이지의 [설치 가이드](https://www.electronjs.org/docs/tutorial/installation)를 참조하십시오.

<span id="step2"></span>
### 2단계: 프로젝트에 trtc-electron-sdk 통합

Electron 환경에서의 정확한 설치 방법을 사용했다면 [1단계](#step1)에서 정상 실행되고, 예상한 효과가 연출됩니다.

이제 공식 홈페이지 Demo를 토대로 2차 개발을 할 수 있으며, 프로젝트의 초기 단계를 원활히 진행할 수 있습니다.

또한 다음 명령어를 실행하여 `trtc-electron-sdk`를 현재 프로젝트에 설치할 수 있습니다.

```bash
npm install trtc-electron-sdk --save
```

<span id="step3"></span>
### 3단계: SDK 인스턴스 초기화 및 이벤트 리슨 콜백

`trtc-electron-sdk` 인스턴스 생성

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

`onError` 이벤트 리스너

```javascript
// 오류 통지는 리스너를 통해 파악하고 사용자에게 고지됨
let onError = function(err) {
  console.error(err);
};
trtcCloud.on('onError',onError);
```

<span id="step4"></span>
### 4단계: 방 입장 매개변수 TRTCParams 어셈블리

[enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) 인터페이스 호출 시 핵심 매개변수[TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html) 하나를 입력해야 합니다. 다음 필드는 매개변수 필수 작성 사항입니다.

| 매개변수     | 유형   | 설명                                                         | 예시                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 숫자 | 애플리케이션 ID,  [콘솔](https://console.cloud.tencent.com/trtc/app) >[Application Management]>[Application Info]에서 조회 가능 | 1400000123 |
| userId  | 문자열 | 영문 알파벳 대소문자(a~z, A~Z), 숫자(0~9), 언더바, 하이픈만 입력 가능 | test_user_001 |
| userSig | 문자열 | userId로 userSig 계산, 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166) 참조  | eJyrVareCeYrSy1SslI... |
| roomId | 숫자 | 문자열 타입의 방 번호 미지원이 기본값임. 이 타입으로 방 번호 설정 시 방 입장 속도 느려짐. 문자열 타입의 방 번호를 꼭 사용해야 할 경우 [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 문의 | 29834 |

```javascript
import {
  TRTCParams,
  TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
```

>! TRTC에서는 2개의 동일한 userId로 동시에 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.

<span id="step5"></span>
### 5단계: 방 생성 및 입장

1. [enterRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom)을 호출하여 `TRTCParams` 매개변수 `roomId`가 지정한 멀티미디어 방에 들어갈 수 있습니다. 해당 방이 존재하지 않는 경우 SDK는 필드 `roomId`를 방 번호로 하는 신규 방을 자동 생성합니다.

2. 응용 시나리오에 따라 적합한 `appScene` 매개변수를 설정하십시오. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.

   - 영상 통화는 `TRTCAppScene.TRTCAppSceneVideoCall`로 설정하십시오.
   - 음성 통화는 `TRTCAppScene.TRTCAppSceneAudioCall`로 설정하십시오.

   [TRTCAppScene ](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)을 클릭하면 'TRTCAppScene'에 관한 자세한 내용을 확인할 수 있습니다.

3. 방에 입장하면 SDK는 [onEnterRoom(result)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) 이벤트를 콜백합니다. 매개변수 `result`가 0보다 크면 방 입장 성공을 뜻하며, 세부 값은 방 입장 소요 시간으로, 단위는 밀리세컨드(ms)입니다. `result`가 0보다 작으면 방 입장 실패를 뜻하며, 세부 값은 방 입장 실패 에러 코드입니다.

```javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, 방 입장 성공, ${result}초 소요`);
  } else {
    console.warn(`onEnterRoom: 방 입장 실패 ${result}`);
  }
};

// 방 입장 성공 이벤트 구독
trtcCloud.on('onEnterRoom', onEnterRoom);

// 입장하려는 방이 개설되어 있지 않은 경우, TRTC가 신규 방을 자동 생성합니다.
let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneVideoCall);
```

<span id="step6"></span>
### 6단계: 원격 멀티미디어 스트림 구독

SDK는 자동 구독 및 수동 구독 기능을 지원합니다. 자동 구독은 바로 재생이 가능해 소수 인원의 통화에 적합합니다. 수동 구독은 트래픽 절약을 추구하므로 참가 인원이 많은 회의에 적합합니다.

#### 자동 구독(권장)

특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.

1. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.

2. [muteRemoteAudio(userId, true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio)를 이용하여 특정 userId의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.

3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) 이벤트가 공지됩니다. 단, 이때 SDK는 비디오 데이터 명령어 처리법을 수신받지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)를 호출하여 원격 사용자의 비디오 데이터와 표시 `view`를 연결하십시오.

4. [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode)를 통해 비디오 화면의 표시 모드를 지정하십시오.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
  
5. [stopRemoteView(userId)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView)를 이용하여 특정 userId의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

```html
<div id="video-container"></div>

<script>
  import TRTCCloud from 'trtc-electron-sdk';
  const trtcCloud = new TRTCCloud();
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;

  /**
   * 카메라 비디오 활성화 여부
   * @param {number} uid - 사용자 표식
   * @param {boolean} available - 화면 활성화 여부
   **/
  let onUserVideoAvailable = function (uid, available) {
    console.log(`onUserVideoAvailable: uid: ${uid}, available: ${available}`);
    if (available === 1) {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (!view) {
        view = document.createElement('div');
        view.id = id;
        videoContainer.appendChild(view);
      }
      trtcCloud.startRemoteView(uid, view);
      trtcCloud.setRemoteViewFillMode(uid, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    } else {
      let id = `${uid}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
      let view = document.getElementById(id);
      if (view) {
        videoContainer.removeChild(view);
      }
    }
  };

  // 인스턴스 코드: 구독 통지(또는 구독 취소)한 원격 사용자의 비디오 화면
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

</script>
```

>? `onUserVideoAvailable()` 이벤트 콜백이 발생한 뒤 즉시 `startRemoteView()`를 호출하여 비디오 스트림을 구독하지 않으면 SDK는 5초 이내에 원격 비디오 데이터의 수신을 중지합니다.

#### 수동 구독 

[setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) 인터페이스를 이용해 SDK를 수동 구독 모드로 설정할 수 있습니다. 수동 구독 모드에서 SDK는 같은 방에 입장한 사용자의 멀티미디어 데이터를 자동 수신하지 않습니다. API 함수를 이용해 직접 트리거해야 합니다.

1. **방 입장 이전** [setDefaultStreamRecvMode(false, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setDefaultStreamRecvMode) 인터페이스를 호출하면 SDK가 수동 구독 모드로 설정됩니다.
2. 같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) 이벤트가 공지됩니다. 이때 [muteRemoteAudio(userId, false)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3. 같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable(userId, available)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) 이벤트가 공지됩니다. 이때 [startRemoteView(userId, view)](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.


<span id="step7"></span>
### 7단계: 로컬의 멀티미디어 스트림 배포

1. [startLocalAudio()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio)를 호출하면 로컬 마이크 수집 기능이 실행되고, 수집한 음성을 인코딩한 뒤 송신할 수 있습니다.
2. [startLocalPreview()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview)를 호출하면 로컬 카메라가 실행되고, 수집한 화면을 인코딩한 뒤 송신할 수 있습니다.
3. [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode)를 호출하면 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fill` 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fit` 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
4. [setVideoEncoderParam()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화면 질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.

```javascript
//예시 코드: 로컬의 멀티미디어 스트림 배포
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
//로컬의 비디오 코드 매개변수 설정
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
```

>! SDK는 카메라와 마이크의 기본값이 설정돼 있습니다. [setCurrentCameraDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentCameraDevice)와 [setCurrentMicDevice()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDevice)를 통해 카메라와 마이크 설정을 변경할 수 있습니다.


<span id="step8"></span>
### 8단계: 현재 방에서 퇴장하기

[exitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) 을 호출하여 방에서 퇴장합니다. 이때 SDK가 카메라와 마이크 등 기기를 차단 및 릴리스하기 때문에 [onExitRoom()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) 콜백을 수신한 뒤에야 퇴장 처리됩니다.

```javascript
// 퇴장 호출 뒤 onExitRoom 이벤트 콜백 대기
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
```

>! Electron이 다수의 멀티미디어 SDK를 동시에 통합했다면 하드웨어 점유 상황을 고려하여 `onExitRoom` 콜백을 수신한 뒤 다른 멀티미디어 SDK를 실행하십시오.
