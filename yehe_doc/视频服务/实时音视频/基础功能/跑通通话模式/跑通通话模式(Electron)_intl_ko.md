## 적용 시나리오

TRTC는 4가지 입장 모드를 지원합니다. 영상 통화(VideoCall)과 음성 통화(VoiceCall)는 통화 모드라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 [라이브 방송 모드](https://intl.cloud.tencent.com/document/product/647/36070)라고 부릅니다.
통화 모드의 TRTC는 단일 방에 최대 300명이 동시에 접속할 수 있으며 최대 50명이 동시에 발언할 수 있습니다. 일대일 영상 통화, 300명 화상 회의, 온라인 진료, 원격 면접, 화상 고객서비스, 온라인 마피아 게임 등의 응용 시나리오에 적합합니다.

## 원리 분석

TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.

-   **인터페이스 노드**
    최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
-   **프록시 노드**
    일반 회로와 일반 성능 기기를 채택하여 동시 접속에 의한 풀 스트림 시청 수요 처리에 적합하며, 시간당 단가가 저렴한 편입니다.

통화 모드에서는 TRTC 방에 있는 모든 사용자가 인터페이스 노드에 할당되므로, 모두가 '호스트'인 셈입니다. 모든 사용자가 언제든지 발언(업스트림 동시 접속 최대 50회선 가능)할 수 있어 온라인 회의와 같은 시나리오에 적합합니다. 단, 방 하나의 수용 인원은 300명으로 제한됩니다.

![](https://main.qcloudimg.com/raw/e6a7492c3d0151252f7853373f6bcbbc.png)

## 예시 코드

[Github](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)에 로그인하여 본 문서와 관련된 예시 코드를 확인할 수 있습니다.

## 작업 단계

[](id:step1)
### 1단계: 공식 홈페이지 SimpleDemo 실행

먼저 [SimpleDemo(Electron) 실행](https://intl.cloud.tencent.com/document/product/647/35089) 문서를 숙지한 뒤 가이드에 따라 Tencent Cloud가 제공하는 공식 홈페이지 SimpleDemo를 실행하는 것을 권장합니다.

- SimpleDemo가 원활하게 실행되면 프로젝트에 Electron을 설치하는 방법을 마스터한 것입니다.
- 반대로, SimpleDemo 실행에 문제가 발생하면 Electron의 다운로드 및 설치에 문제가 있다는 뜻입니다. 이 경우, Electron 공식 홈페이지의 [설치 가이드](https://www.electronjs.org/docs/tutorial/installation)를 참고할 수 있습니다.

[](id:step2)
### 2단계: 프로젝트를 trtc-electron-sdk로 통합

[1단계](#step1)가 정상적으로 실행되고 효과가 예상과 부합한다면 Electron 환경의 설치 방법을 마스터했다는 뜻입니다.

- Tencent Cloud의 공식 홈페이지 Demo를 기반으로 2차 개발을 진행할 수 있으므로, 프로젝트의 초기 단계는 비교적 순조로울 것입니다.
- 다음과 같은 명령을 실행하여 `trtc-electron-sdk`를 사용자의 현재 프로젝트에 설치할 수 있습니다.
```bash
npm install trtc-electron-sdk --save
```

[](id:step3)
### 3단계: SDK 인스턴스 초기화 및 이벤트 콜백 수신

1. `trtc-electron-sdk` 인스턴스 생성:
```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```
2. `onError` 이벤트 수신
<dx-codeblock>
::: javascript javascript
// 오류 공지를 수신하여 사용자에게 공지해야 함
let onError = function(err) {
    console.error(err);
};
trtcCloud.on('onError',onError);
:::
</dx-codeblock>

[](id:step4)
### 4단계: 방 입장 매개변수 TRTCParams 어셈블리

[enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) 인터페이스 호출 시 핵심 매개변수 [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)를 입력해야 합니다. 해당 매개변수에 포함되어 있는 필수 입력 필드는 다음과 같습니다.

| 매개변수     | 유형   | 설명                                                         | 예시                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 숫자 | 애플리케이션 ID, [콘솔](https://console.cloud.tencent.com/trtc/app) >[애플리케이션 관리]>[애플리케이션 정보]에서 조회 가능 | 1400000123 |
| userId   | 문자열 | 영어 알파벳 대소문자(a-z, A-Z)와 숫자(0-9), 언더바(_), 대시 부호(-)만 허용됩니다. 업무 실제 계정 시스템에 맞게 설정할 것을 권장합니다. | test_user_001|
| userSig  | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. | eJyrVareCeYrSy1SslI... |
| roomId   | 숫자   | 숫자 유형의 방 번호입니다. 문자열 형식의 방 번호를 사용하려면 TRTCParams에서 strRoomId를 사용하십시오. | 29834  |

<dx-codeblock>
::: javascript javascript
import {
  TRTCParams,
  TRTCRoleType 
} from "trtc-electron-sdk/liteav/trtc_define";

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
:::
</dx-codeblock>


>! 
>- TRTC에서는 같은 userId 2개로 방에 동시 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step5)
### 5단계: 방 생성 및 입장

1. [enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom)을 호출하여 `TRTCParams` 매개변수 `roomId`가 지정한 멀티미디어 방에 들어갈 수 있습니다. 해당 방이 존재하지 않는 경우 SDK는 필드 `roomId`를 방 번호로 하는 신규 방을 자동 생성합니다.
2. 응용 시나리오에 따라 적합한 `appScene`  매개변수를 설정합니다. 잘못된 매개변수를 사용하는 경우 랙이 발생하거나 화면 해상도가 떨어질 수 있습니다.
   - 영상 통화는 `TRTCAppScene.TRTCAppSceneVideoCall`로 설정하십시오.
   - 음성 통화는 `TRTCAppScene.TRTCAppSceneAudioCall`로 설정하십시오.
>? `TRTCAppScene`에 대한 자세한 소개는 [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)을 참고하십시오.
3. 방에 입장하면 SDK는 [onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) 이벤트를 콜백합니다. 매개변수 `result`가 0보다 크면 방 입장 성공을 뜻하며, 세부 값은 방 입장 소요 시간으로, 단위는 밀리세컨드(ms)입니다. `result`가 0보다 작으면 방 입장 실패를 뜻하며, 세부 값은 방 입장 실패 에러 코드입니다.

<dx-codeblock>
::: javascript javascript
import TRTCCloud from 'trtc-electron-sdk';
import { TRTCParams, TRTCAppScene } from "trtc-electron-sdk/liteav/trtc_define";
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();

let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, 입장 성공, ${result}초 소요`);
  } else {
    console.warn(`onEnterRoom: 입장 실패 ${result}`);
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
:::
</dx-codeblock>


[](id:step6)
### 6단계: 원격 멀티미디어 스트림 구독

SDK는 자동 구독 및 수동 구독 기능을 지원합니다. 자동 구독은 바로 재생이 가능해 소수 인원의 통화에 적합합니다. 수동 구독은 트래픽 절약을 추구하므로 참가 인원이 많은 회의에 적합합니다.

#### 자동 구독(권장)

특정 방에 입장하면 SDK가 방에 입장한 다른 사용자의 오디오 스트림을 자동 수신하여 '바로 재생' 수준으로 재생합니다.

1.  같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) 이벤트가 공지되고, SDK는 원격 사용자의 음성을 자동 재생합니다.
2.  [muteRemoteAudio(userId,  true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio)를 이용하여 특정 userId의 오디오 데이터를 차단할 수 있으며, [muteAllRemoteAudio(true)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio)를 통해 모든 원격 사용자의 오디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 사용자의 오디오 데이터를 불러오지 않습니다.
3.  같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) 이벤트가 수신됩니다. 단, 이 때 SDK는 비디오 데이터 명령어 처리 방법을 수신하지 못해 비디오 데이터를 자동 처리하지 않습니다. [startRemoteView(userId, view, streamType)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)를 호출하여 원격 사용자의 비디오 데이터와 `view` 표시를 연결합니다.
4.  [setLocalViewFillMode()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode)를 통해 비디오 화면의 표시 모드를 지정합니다.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill` 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit` 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
5.  [stopRemoteView(userId)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView)를 이용하여 특정 userId의 비디오 데이터를 차단할 수 있으며, [stopAllRemoteView()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView)를 통해 모든 원격 사용자의 비디오 데이터를 차단할 수 있습니다. 차단이 완료되면 SDK는 차단 대상 원격 사용자의 비디오 데이터를 불러오지 않습니다.

<dx-codeblock>
::: html html
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
:::
</dx-codeblock>

>? `onUserVideoAvailable()` 이벤트 콜백이 발생한 뒤 즉시 `startRemoteView()`를 호출하여 비디오 스트림을 구독하지 않으면 SDK는 5초 이내에 원격 비디오 데이터의 수신을 중지합니다.

#### 수동 구독

[setDefaultStreamRecvMode(autoRecvAudio, autoRecvVideo)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) 인터페이스를 이용해 SDK를 수동 구독 모드로 설정할 수 있습니다. 수동 구독 모드에서 SDK는 같은 방에 입장한 사용자의 멀티미디어 데이터를 자동 수신하지 않습니다. API 함수를 이용해 직접 트리거해야 합니다.

1.  **방 입장 이전** [setDefaultStreamRecvMode(false, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) 인터페이스를 호출하면 SDK가 수동 구독 모드로 설정됩니다.
2.  같은 방에 입장한 사용자가 오디오 데이터를 업스트림하면 [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) 이벤트가 수신됩니다. 이 때 [muteRemoteAudio(userId, false)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio)를 호출하여 해당 사용자의 오디오 데이터를 수동 구독해야 SDK가 해당 사용자의 오디오 데이터를 수신한 뒤 디코딩하여 재생합니다.
3.  같은 방에 입장한 사용자가 비디오 데이터를 업스트림하면 [onUserVideoAvailable(userId, available)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) 이벤트가 수신됩니다. 이 때 [startRemoteView(userId,  view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)를 호출하여 해당 사용자의 비디오 데이터를 수동 구독해야 SDK가 해당 사용자의 비디오 데이터를 수신한 뒤 디코딩하여 재생합니다.


[](id:step7)
### 7단계: 로컬의 멀티미디어 스트림 배포

1. [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)를 호출하여 마이크 수집을 활성화하고 수집된 오디오를 인코딩 및 발송합니다.
2. [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)를 호출하여 카메라 수집을 활성화하고 수집된 비디오를 인코딩 및 발송합니다.
3. [setLocalViewFillMode()](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode)를 호출하여 로컬 비디오의 표시 모드를 설정합니다.
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fill` 모드: 확대 화면을 뜻하며, 검은 여백 없이 화면을 일정 비율로 확대 및 편집할 수 있습니다.
   - `TRTCVideoFillMode.TRTCVideoFillMode_Fit` 모드: 축소 화면을 뜻하며, 일정 비율로 화면을 축소할 수 있습니다. 콘텐츠가 전부 표시되지만 검은 여백도 발생합니다.
4. [setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) 인터페이스를 호출하면 로컬 비디오의 코드 매개변수를 설정할 수 있습니다. 해당 매개변수는 같은 방 사용자가 시청하는 화면의 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.

<dx-codeblock>
::: javascript javascript
//예시 코드: 로컬 멀티미디어 스트림 배포
trtcCloud.startLocalPreview(view);
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);
trtcCloud.startLocalAudio();
// 로컬 비디오 인코딩 매개변수 설정
let encParam = new TRTCVideoEncParam();
encParam.videoResolution = TRTCVideoResolution.TRTCVideoResolution_640_360;
encParam.resMode = TRTCVideoResolutionMode.TRTCVideoResolutionModeLandscape;
encParam.videoFps = 25;
encParam.videoBitrate = 600;
encParam.enableAdjustRes = true;
trtcCloud.setVideoEncoderParam(encParam);
:::
</dx-codeblock>


>! SDK는 카메라와 마이크의 기본값이 설정되어 있습니다. [setCurrentCameraDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) 및 [setCurrentMicDevice()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice)를 통해 카메라와 마이크 설정을 변경할 수 있습니다.


[](id:step8)
### 8단계: 현재 방에서 퇴장하기

[exitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom)을 호출하여 퇴장합니다. 퇴장 시 SDK에서 카메라, 마이크 등 하드웨어 기기를 비활성화 및 릴리스해야 합니다. 따라서 퇴장은 금방 완료되지 않으며, [onExitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) 콜백을 수신해야 완료됩니다.

<dx-codeblock>
::: javascript javascript
// 퇴장 호출 후 onExitRoom 이벤트 콜백 대기
let onExitRoom = function (reason) {
  console.log(`onExitRoom, reason: ${reason}`);
};
trtcCloud.exitRoom();
trtcCloud.on('onExitRoom', onExitRoom);
:::
</dx-codeblock>

>! Electron이 다수의 멀티미디어 SDK를 동시에 통합했다면 하드웨어 점유 상황을 고려하여 `onExitRoom` 콜백을 수신한 뒤 다른 멀티미디어 SDK를 실행하십시오.
