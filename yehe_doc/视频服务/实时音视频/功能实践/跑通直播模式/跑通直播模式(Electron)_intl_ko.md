## 적용 시나리오

TRTC는 4가지 입장 모드를 지원합니다. 영상 통화(VideoCall), 음성 통화(VoiceCall)는 [통화 모드](https://intl.cloud.tencent.com/document/product/647/36069)라고 부르고, 비디오 ILVB(Live)와 음성 ILVB(VoiceChatRoom)는 라이브 방송 모드라고 부릅니다.
라이브 방송 모드의 TRTC는 단일 방에 최대 10만 명이 동시에 접속할 수 있으며 300ms 미만의 마이크 연결 딜레이 및 1000ms 미만의 시청 딜레이, 매끄러운 마이크 켜짐/꺼짐 등의 기능을 갖추고 있습니다. 저지연 ILVB, 10만 인터랙션 강의, 화상 소개팅, 온라인 교육, 원격 교육, 초대형 회의 등의 응용 시나리오에 적합합니다.

## 원리 분석

TRTC 클라우드 서비스는 '인터페이스 노드'와 '프록시 노드'라는 두 가지 서버 노드로 구성되어 있습니다.

-   **인터페이스 노드**
    최고 품질의 회로와 고성능 기기를 사용해 단말기 간의 저지연 마이크 연결 통화 처리에 적합하며, 시간당 단가가 비싼 편입니다.
-   **프록시 노드**
    일반 회로와 일반 성능 기기를 채택하여 동시 접속에 의한 풀 스트림 시청 수요 처리에 적합하며, 시간당 단가가 저렴한 편입니다.

통화 모드에서는 TRTC 방에 있는 모든 사용자가 인터페이스 노드에 할당되므로, 모두가 '호스트'인 셈입니다. 모든 사용자가 언제든지 발언(최고 업스트림 동시 접속 제한은 50회선)할 수 있어 온라인 회의와 같은 시나리오에 적합합니다. 단, 한 개 방의 인원은 300명으로 제한됩니다.

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

`trtc-electron-sdk` 인스턴스 생성:

```javascript
import TRTCCloud from 'trtc-electron-sdk';
let trtcCloud = new TRTCCloud();
```

`onError` 이벤트 수신:

```javascript
// 오류 공지를 수신하여 사용자에게 공지해야 함
let onError = function(err) {
  console.error(err);
}
trtcCloud.on('onError',onError);
```

[](id:step4)
### 4단계: 방 입장 매개변수 TRTCParams 어셈블리

[enterRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) 인터페이스 호출 시 핵심 매개변수 [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)를 입력해야 합니다. 해당 매개변수에 포함되어 있는 필수 입력 필드는 다음과 같습니다.

| 매개변수     | 유형   | 설명                                                         | 예시                   |
| :------- | :----- | :----------------------------------------------------------- | :--------------------- |
| sdkAppId | 숫자 | 애플리케이션 ID. [콘솔](https://console.cloud.tencent.com/trtc/app)>[애플리케이션 관리]>[애플리케이션 정보]에서 확인할 수 있습니다. | 1400000123             |
| userId | 문자열 | 영어 알파벳 대소문자(a-z, A-Z)와 숫자(0-9), 언더바(_), 대시 부호(-)만 허용됩니다. | test_user_001|
| userSig | 문자열 | userId를 기반으로 userSig를 계산할 수 있습니다. 계산 방법은 [UserSig 계산 방법] (https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. | eJyrVareCeYrSy1SslI... |
| roomId   | 숫자   | 기본적으로 입장 속도에 영향을 줄 수 있는 문자열 유형의 방 번호를 지원하지 않습니다. 문자열 유형의 방 번호 지원이 반드시 필요한 경우, [Submit Ticket](https://console.cloud.tencent.com/workorder/category)을 통해 고객센터로 문의하십시오. | 29834  |

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
param.role = TRTCRoleType.TRTCRoleAnchor; // '호스트'로 역할 설정
:::
</dx-codeblock>

>! 
>- TRTC에서는 같은 userId 2개로 방에 동시 입장하면 서로 영향을 미칠 수 있으므로 이를 지원하지 않습니다.
>- 각 엔드는 appScene에서 통일되어야 합니다. 그렇지 않으면 예기치 않은 문제가 발생할 수 있습니다.

[](id:step5)
### 5단계: 호스트의 카메라 미리보기 및 마이크 음성 수집 활성화
1. 호스트 측에서 [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)를 호출하여 로컬 카메라 미리보기를 활성화할 수 있습니다. SDK가 시스템에 카메라 사용 권한을 요청하게 됩니다.
2. 호스트 측에서 `setLocalViewFillMode()`를 호출하여 로컬 비디오 화면의 표시 모드를 설정할 수 있습니다.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fill`: 이 모드는 '채우기'를 의미합니다. 화면은 같은 비율로 확대되거나 잘릴 수 있지만, 검은 부분은 없습니다.
    -   `TRTCVideoFillMode.TRTCVideoFillMode_Fit`: 이 모드는 '맞추기'를 의미합니다. 화면은 해당 콘텐츠가 전부 표시되도록 같은 비율로 축소될 수 있고, 검은 부분이 있을 수 있습니다.
3. 호스트 측에서 [setVideoEncoderParam()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) 인터페이스를 호출하여 로컬 비디오의 인코딩 매개변수를 설정할 수 있습니다. 해당 매개변수는 방에 있는 다른 사용자가 사용자의 화면을 시청할 때 느끼는 [화질](https://intl.cloud.tencent.com/document/product/647/35153)을 결정합니다.
4. 호스트 측에서 [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)를 호출하여 마이크를 활성화합니다. SDK가 시스템에 마이크 사용 권한을 요청하게 됩니다.


<dx-codeblock>
::: javascript javascript
//예시 코드: 로컬 멀티미디어 스트림 배포
trtcCloud.startLocalPreview(view);
trtcCloud.startLocalAudio();
trtcCloud.setLocalViewFillMode(TRTCVideoFillMode.TRTCVideoFillMode_Fill);

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

[](id:step6)
### 6단계: 호스트의 뷰티 필터 효과 설정

1. 호스트 측에서 [setBeautyStyle(style, beauty, white, ruddiness)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle)를 호출하여 뷰티 필터 효과를 활성화할 수 있습니다.
2. 매개변수 설명
    -   style: 뷰티 필터 스타일로 매끄럽게 또는 내추럴 스타일이 있으며, 매끄럽게 스타일은 피부 보정 효과가 더 뚜렷해 엔터테인먼트 시나리오에 적합합니다.
        -   `TRTCBeautyStyle.TRTCBeautyStyleSmooth`: 매끄럽게 스타일로 뷰티쇼에 적합하며 효과가 비교적 뚜렷합니다.
        -   `TRTCBeautyStyle.TRTCBeautyStyleNature`: 내추럴 스타일로 피부 보정 알고리즘이 얼굴의 디테일을 더 많이 유지하여 자연스러운 느낌을 줍니다.
    -   beauty: 뷰티 필터로 0 - 9레벨이 있습니다. 0은 효과 없음, 1 - 9는 숫자가 커질수록 효과가 뚜렷합니다.
    -   white: 미백 효과로 0 - 9레벨이 있습니다. 0은 효과 없음, 1 - 9는 숫자가 커질수록 효과가 뚜렷합니다.
    -   ruddiness: 블러셔 효과로 0 - 9레벨이 있습니다. 0은 효과 없음, 1 - 9는 숫자가 커질수록 효과가 뚜렷합니다. 해당 매개변수는 현재 Windows 플랫폼에서 적용되지 않습니다.

```javascript
// 뷰티 필터 활성화 
trtcCloud.setBeautyStyle(TRTCBeautyStyle.TRTCBeautyStyleNature, 5, 5, 5);
```


[](id:step7)
### 7단계: 호스트의 방 생성 및 푸시 스트리밍 시작

1. 호스트 측에서 [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)의 `role` 필드를 **`TRTCRoleType.TRTCRoleAnchor`**로 설정하여 현재 사용자의 역할이 호스트라는 것을 표시합니다.
2. 호스트 측에서 enterRoom( )을 호출하여 TRTCParams 매개변수 `roomId` 필드의 값이 방 번호인 멀티미디어 룸을 생성하고 `appScene` 매개변수를 지정할 수 있습니다.
    -   `TRTCAppScene.TRTCAppSceneLIVE`: 비디오 ILVB는 매끄러운 마이크 켜짐/꺼짐 및 대기가 필요 없는 호스트 딜레이 300ms 미만의 전환을 지원합니다. 또한 재생 딜레이 1000ms 미만의 시청자 10만 명 동시 재생을 지원합니다. 본 문서는 이 모드를 예로 들어 설명합니다.
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: 음성 ILVB는 매끄러운 마이크 켜짐/꺼짐 및 대기가 필요 없는 호스트 딜레이 300ms 미만의 전환을 지원합니다. 또한 재생 딜레이 1000ms 미만의 시청자 10만 명 동시 재생을 지원합니다.  
    -   `TRTCAppScene`에 대한 자세한 소개는 [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)을 참고하십시오.
3. 방 생성에 성공하면 호스트 측에서 멀티미디어 데이터의 인코딩과 전송 프로세스를 시작하며, 이와 동시에 SDK는 [onEnterRoom(result)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) 이벤트를 콜백합니다. 매개변수 `result`가 0보다 크면 입장에 성공한 것이며, 해당 값은 입장에 걸린 시간을 밀리초(ms) 단위로 나타냅니다. `result`가 0보다 작으면 입장에 실패한 것이며, 해당 값은 입장 실패의 에러 코드입니다.

<dx-codeblock>
::: javascript javascript
let onEnterRoom = function (result) {
  if (result > 0) {
    console.log(`onEnterRoom, 입장 성공, ${result}초 소요`);
  } else {
    console.warn(`onEnterRoom: 방 입장 실패 ${result}`);
  }
};

trtcCloud.on('onEnterRoom', onEnterRoom);

let param = new TRTCParams();
param.sdkAppId = 1400000123;
param.roomId = 29834;
param.userId = 'test_user_001';
param.userSig = 'eJyrVareCeYrSy1SslI...';
param.role = TRTCRoleType.TRTCRoleAnchor;
trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
:::
</dx-codeblock>

[](id:step8)
### 8단계: 시청자의 방 입장 후 라이브 방송 시청

1. 시청자 측에서[TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)의 `role` 필드를 **`TRTCRoleType.TRTCRoleAudience`**로 설정하여 현재 사용자의 역할이 시청자라는 것을 표시합니다.
1. 시청자 측에서 `enterRoom()`을 호출하면 `TRTCParams` 매개변수 중 `roomId`가 가리키는 멀티미디어 방에 입장하며, `appScene` 매개변수를 지정할 수 있습니다.
    -   `TRTCAppScene.TRTCAppSceneLIVE`: 비디오 ILVB
    -   `TRTCAppScene.TRTCAppSceneVoiceChatRoom`: 음성 ILVB
2. 호스트 화면 시청
    -  시청자 측에서 사전에 호스트의 `userId`를 알고 있을 경우, 입장 성공 후 바로 호스트 `userId`를 사용해 [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)를 호출하여 호스트의 화면을 볼 수 있습니다.
    - 시청자는 입장 성공 후 [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) 이벤트 공지를 받게 됩니다. 시청자가 사전에 호스트의 userId를 모를 경우, 콜백에서 확인한 호스트 `userId`를 사용해 [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)를 호출하여 호스트의 화면을 볼 수 있습니다.

<dx-codeblock>
::: html html
<div id="video-container"></div>
<script>
  const videoContainer = document.querySelector('#video-container');
  const roomId = 29834;
  // 방 입장 콜백, 방 입장 성공 시 트리거되는 콜백
  let onEnterRoom = function(result) {
    if (result > 0) {
      console.log(`onEnterRoom, 입장 성공, ${result}초 소요`);
    } else {
      console.warn(`onEnterRoom: 입장 실패 ${result}`);
    }
  };
  // 호스트가 카메라 푸시 스트림 활성화 또는 비활성화 시 트리거되는 콜백
  let onUserVideoAvailable = function(userId, available) {
    if (available === 1) {
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (!view) {
          view = document.createElement('div');
          view.id = id;
          videoContainer.appendChild(view);
        }
        trtcCloud.startRemoteView(userId, view);
        trtcCloud.setRemoteViewFillMode(userId, TRTCVideoFillMode.TRTCVideoFillMode_Fill);
    } else {
        let id = `${userId}-${roomId}-${TRTCVideoStreamType.TRTCVideoStreamTypeBig}`;
        let view = document.getElementById(id);
        if (view) {
          videoContainer.removeChild(view);
        }
    }
  };

  trtcCloud.on('onEnterRoom', onEnterRoom);
  trtcCloud.on('onUserVideoAvailable', onUserVideoAvailable);

  let param = new TRTCParams();
  param.sdkAppId = 1400000123;
  param.roomId = roomId;
  param.userId = 'test_user_001';
  param.userSig = 'eJyrVareCeYrSy1SslI...';
  param.role = TRTCRoleType.TRTCRoleAudience; // '시청자'로 역할 설정
  trtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
</script>
:::
</dx-codeblock>

[](id:step9)
### 9단계: 시청자와 호스트의 마이크 연결

1. 시청자 측에서 [switchRole(TRTCRoleType.TRTCRoleAnchor)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole)을 호출하여 역할을 호스트(`TRTCRoleType.TRTCRoleAnchor`)로 전환합니다.
2. 시청자 측에서 [startLocalPreview()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview)를 호출하여 로컬 화면을 활성화할 수 있습니다.
3. 시청자 측에서 [startLocalAudio()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio)를 호출하여 마이크 음성 수집을 활성화합니다.

<dx-codeblock>
::: javascript javascript
//예시 코드: 시청자 마이크 켜짐
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAnchor);
trtcCloud.startLocalAudio();
trtcCloud.startLocalPreview(frontCamera, view);

//예시 코드: 시청자 마이크 꺼짐
trtcCloud.switchRole(TRTCRoleType.TRTCRoleAudience);
trtcCloud.stopLocalAudio();
trtcCloud.stopLocalPreview();
:::
</dx-codeblock>


[](id:step10)
### 10단계: 호스트 간 크로스 룸 마이크 연결 PK

TRTC에서는 서로 다른 멀티미디어 룸의 두 호스트가 기존의 라이브 룸 시나리오에서 퇴장하지 않고도 '크로스 룸 통화' 기능을 통해 마이크를 연결하여 '크로스 룸 마이크 연결 PK'가 가능합니다.

1. 호스트 A가 [connectOtherRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) 인터페이스를 호출합니다. 현재 인터페이스 매개변수는 JSON 포맷을 사용하며, 호스트 B의 `roomId`와 `userId`를 {"roomId": "978","userId": "userB"}` 포맷으로 만든 매개변수를 인터페이스 함수에 전달해야 합니다.
2. 크로스 룸에 성공하면 호스트 A는 [onConnectOtherRoom(userId, errCode, errMsg)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) 이벤트 콜백을 수신합니다. 이와 동시에 두 라이브 룸에 있는 모든 사용자는 [onUserVideoAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable)과 [onUserAudioAvailable()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) 이벤트 공지를 받게 됩니다.
    예를 들어 방 '001'의 호스트 A가 `connectOtherRoom()`을 통해 방 '002'의 호스트 B와 크로스 룸 통화를 연결하면, 방 '001'의 사용자는 호스트 B의 `onUserVideoAvailable(B, true)` 콜백과 `onUserAudioAvailable(B, true)` 콜백을 받게 됩니다. 그리고 방 '002'의 사용자는 호스트 A의 `onUserVideoAvailable(A, true)` 콜백과 `onUserAudioAvailable(A, true)` 콜백을 받게 됩니다.
3. 두 방의 사용자는 [startRemoteView(userId, view)](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView)를 호출하여 상대 방 호스트의 화면을 볼 수 있으며, 소리는 자동으로 재생됩니다.

![호스트 마이크 연결 연결 흐름도](https://main.qcloudimg.com/raw/bffa420102bb31dee6f76d7f08a16e4f.png)

<dx-codeblock>
::: javascript javascript
//예시 코드: 크로스 룸 마이크 연결 PK
let onConnectOtherRoom = function(userId, errCode, errMsg) {
  if(errCode === 0) {
    console.log(`호스트 ${userId}의 방에 성공적으로 연결`);
  } else {
    console.warn(`다른 호스트 방 연결 실패: ${errMsg}`);
  }
};

const paramJson = '{"roomId": "978","userId": "userB"}';
trtcCloud.connectOtherRoom(paramJson);
trtcCloud.on('onConnectOtherRoom', onConnectOtherRoom); 
:::
</dx-codeblock>

[](id:step11)
### 11단계: 현재 방 퇴장  

[exitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) 방법을 호출하여 퇴장합니다. 퇴장 시 SDK에서 카메라, 마이크 등 하드웨어 기기를 비활성화 및 릴리스해야 합니다. 따라서 퇴장은 금방 완료되지 않으며, [onExitRoom()](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) 콜백을 받아야만 완료됩니다.

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

>! 사용자의 Electron 프로그램에 여러 개의 멀티미디어 SDK가 동시에 통합되었을 경우, `onExitRoom` 콜백을 받은 후 다른 멀티미디어 SDK를 재실행하십시오. 그렇지 않으면 하드웨어 점유 문제가 발생할 수 있습니다.
