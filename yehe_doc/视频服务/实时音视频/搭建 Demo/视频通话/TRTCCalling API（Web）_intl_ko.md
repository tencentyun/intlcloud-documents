## TRTCCalling 소개

[TRTCCalling](https://www.npmjs.com/package/trtc-calling-js) 컴포넌트는 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 기반으로 하며, 1대1 및 그룹 음성/영상 통화를 지원합니다. 자세한 구현 방법은 [실시간 영상 통화(Web)](https://intl.cloud.tencent.com/document/product/647/38927)를 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저지연 멀티미디어 통화 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 메시지를 발송 및 처리합니다.

## 환경 요건
최신 버전의 Chrome 브라우저를 사용하십시오. 현재 데스크톱 버전 Chrome 브라우저는 TRTC Web SDK를 지원하며 관련된 특성이 비교적 완벽하므로 Chrome 브라우저를 권장합니다. 자세한 내용은 [환경 요건](https://intl.cloud.tencent.com/document/product/647/38927#.E7.8E.AF.E5.A2.83.E8.A6.81.E6.B1.82)을 참고하십시오.

## TRTCCalling API 

#### 이벤트 구독/구독 취소 API  

본 컴포넌트는 이벤트 전달을 기반으로 관리하며, 애플리케이션 레이어는 컴포넌트가 전달하는 이벤트에 따라 UI 상호 작용을 변경할 수 있습니다.

| API                                       | 설명         |
| ----------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on)   | 이벤트 구독     |
| [off(eventName, callback, context)](#off) | 이벤트 구독 취소 |

#### SDK 기본 함수

| API                                | 설명                                          |
| ---------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login) | IM 인터페이스 로그인. 모든 기능은 로그인 후 사용할 수 있습니다. |
| [logout()](#logout)                |  인터페이스 로그아웃. 로그아웃 후에는 발신 작업을 진행할 수 없습니다.            |

#### 통화 작업 API 

| API                                                          | 설명        |
| ------------------------------------------------------------ | ------------ |
| [call({userID, type, offlinePushInfo}))](#call)              | 1:1 통화 초대 |
| [groupCall({userIDList, type, groupID, offlinePushInfo})](#groupCall) | 그룹 통화 초대 |
| [accept()](#accept)                                          | 통화 초대 수락 |
| [reject()](#reject)                                           | 통화 초대 거절 |
| [hangup()](#hangup)                                        | 현재 통화 끊기 |

#### 비디오 제어 API 

| API                                                          | 설명                  |
| ------------------------------------------------------------ | ---------------------- |
| [startRemoteView({userID, videoViewDomID})](#startRemoteView) | 원격 화면 렌더링 실행   |
| [stopRemoteView({userID})](#stopRemoteView)   | 원격 화면 렌더링 중지   |
| [startLocalView({userID, videoViewDomID})](#startLocalView)   | 로컬 화면 렌더링 실행   |
| [stopLocalView({userID})](#stopLocalView) | 로컬 화면 렌더링 중지       |
| [openCamera()](#openCamera)                                                                 | 카메라 켜기         |
| [closeCamera()](#closeCamera)                                                               | 카메라 끄기         |
| [setMicMute(isMute)](#setMicMute)    | 마이크 음소거/음소거 해제 |
| [setVideoQuality(profile)](#setVideoQuality)|   비디오 품질 설정 |
| [switchToAudioCall()](#switchToAudioCall) | 음성 통화로 전환   |
| [switchToVideoCall()](#switchToVideoCall) | 영상 통화로 전환    |
| [getCameras()](#getCameras)                 | 카메라 디바이스 리스트 획득   |
| [getMicrophones()](#getMicrophones)     | 마이크 디바이스 리스트 획득   |
| [switchDevice({deviceType, deviceId})](#switchDevice) | 카메라 또는 마이크 디바이스 전환 |


## TRTCCalling 상세 설명

### TRTCCalling 인스턴스 생성

먼저 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에서 애플리케이션을 생성하여 SDKAppID를 획득합니다.
생성 후, `new TRTCCalling()`을 통해 TRTCCalling 컴포넌트 인스턴스를 획득합니다.

```js
  npm i trtc-js-sdk --save
  npm i tim-js-sdk --save
  npm i tsignaling --save
  npm i trtc-calling-js --save
  // node로 다운로드한 종속성인 경우 import를 사용하여 가져오기
  import TRTCCalling from 'trtc-calling-js';

  // script로 trtc-calling-js를 사용해야 하는 경우 순서를 따라야합니다.
  // trtc.js 수동 가져오기
  <script src="./trtc.js"></script>
  // tim-js.js를 수동으로 가져옵니다.
  <script src="./tim-js.js"></script>
  // tsignaling.js를 수동으로 가져옵니다.
  <script src="./tsignaling.js"></script>
  // trtc-calling-js.js를 수동으로 가져옵니다.
  <script src="./trtc-calling-js.js"></script>

let options = {
  SDKAppID: 0, // 연결 시 0을 IM 애플리케이션의 SDKAppID로 대체합니다.
  // v0.10.2부터 tim 매개변수가 추가되었습니다.
  // tim 매개변수는 TIM 인스턴스의 고유성을 보장하기 위해 비즈니스의 기존 TIM 인스턴스에 적용됩니다.
  tim: tim
};
let trtcCalling = new TRTCCalling(options);
```



### 이벤트 구독/구독 취소 API  

[](id:on)
#### on(eventName, callback, context)

컴포넌트가 전달한 이벤트를 수신하는데 사용됩니다. 이벤트에 대한 자세한 내용은 [이벤트 리스트](#event)를 참고하십시오.

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
:::
</dx-codeblock>



[](id:off)
#### off(eventName, callback, context)

이벤트 수신 취소에 사용됩니다.

<dx-codeblock>
::: javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
:::
</dx-codeblock>

### SDK 기본 함수

[](id:login)
#### login({userID, userSig})

인터페이스 로그인에 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.login({userID, userSig})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID  | String | 현재의 사용자 ID. 영어 알파벳(a-z, A-Z), 숫자(0-9), 하이픈(-), 언더바(\_)의 문자열로 구성합니다.                   |
| userSig  | String         | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |

[](id:logout)
#### logout()

 인터페이스 로그아웃에 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.logout()
:::
</dx-codeblock>

### 통화 작업 API 

[](id:call)
#### call({userID, type, offlinePushInfo})

1대1 통화 초대에 사용되며, type은 통화 유형으로, 1-음성 통화, 2-영상 통화입니다.

>?
>- v1.0.0부터 timeout 매개변수가 취소되었습니다.
>- v1.0.0부터 offlinePushInfo 매개변수(**오프라인 푸시는 Android 또는 iOS만 지원. Web 및 WeChat 미니프로그램 미지원**)가 추가되었습니다.

<dx-codeblock>
::: javascript javascript
// v1.0.0 이전 버전
trtcCalling.call({userID, type, timeout});

// v1.0.0 및 이후 버전
const offlinePushInfo = {
  title: '',
  description: '1개의 통화 요청이 있습니다'.
}
trtcCalling.call({userID, type, offlinePushInfo})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수            | 유형   | 의미                                                       |
| --------------- | ------ | ---------------------------------------------------------- |
| userID          | String | 초대된 사용자의 userID          |
| type            | Number | 1: 음성 통화, 2: 영상 통화                                   |
| timeout         | Number | 0: 타임 아웃 설정하지 않음(단위: s(초)).  **v1.0.0 이전 버전만 해당**        |
| offlinePushInfo | Object | 사용자 정의 오프라인 메시지 푸시(선택사항). **v1.0.0 및 이후 버전만 해당** |

offlinePushInfo 매개변수 (v1.0.0 및 이후 버전만 해당)

| 매개변수                 | 유형   | 의미                                                   |
| -------------------- | ------ | ------------------------------------------------------ |
| title                | String | 오프라인 푸시 제목(선택사항)                                   |
| description          | String | 오프라인 푸시 내용(선택사항)                                    |
| androidOPPOChannelID | String | OPPO 휴대폰 시스템 8.0 및 이후 버전 오프라인 푸시의 채널 ID 설정(선택사항) |
| extension            | String | 오프라인 푸시 패스스루 콘텐츠(옵션). **TRTCCalling 버전>=1.0.2, tsignaling 버전 >= 0.9.0만 해당** |

[](id:groupCall)
#### groupCall({userIDList, type, groupID, offlinePushInfo})
groupID 매개변수는 IM SDK 상의 그룹 ID로, 해당 매개변수를 입력하는 경우 통화 요청 정보가 그룹 정보 시스템을 통해 전송됩니다. 해당 정보 전송 방식은 비교적 간단하면서 신뢰성이 높습니다. 입력하지 않는 경우 TRTCCalling 컴포넌트가 개별 발송 방식을 사용하여 1개씩 통지합니다.

>?v1.0.0부터 offlinePushInfo 매개변수(**오프라인 푸시는 Android 또는 iOS만 지원. Web 및 WeChat 미니프로그램 미지원**)가 추가되었습니다.

<dx-codeblock>
::: javascript javascript
// v1.0.0 이전 버전
trtcCalling.groupCall({userIDList, type, groupID});

// v1.0.0 및 이후 버전
const offlinePushInfo = {
  title: '',
  description: '1개의 통화 요청이 있습니다'.
}
trtcCalling.groupCall({userIDList, type, groupID, offlinePushInfo})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수            | 유형   | 의미                                                       |
| --------------- | ------ | ---------------------------------------------------------- |
| userIDList      | Array  | 초대 리스트                                                   |
| type            | Number | 1: 음성 통화, 2: 영상 통화                                   |
| groupID         | String | IM 그룹 ID(선택사항)                                         |
| offlinePushInfo | Object | 사용자 정의 오프라인 메시지 푸시(선택사항). **v1.0.0 및 이후 버전만 해당** |

offlinePushInfo 매개변수 (v1.0.0 및 이후 버전만 해당)

| 매개변수                 | 유형   | 의미                                                   |
| -------------------- | ------ | ------------------------------------------------------ |
| title                | String | 오프라인 푸시 제목(선택사항)                                   |
| description          | String | 오프라인 푸시 내용(선택사항)                                    |
| androidOPPOChannelID | String | OPPO 휴대폰 시스템 8.0 및 이후 버전 오프라인 푸시의 채널 ID 설정(선택사항) |
| extension            | String | 오프라인 푸시 패스스루 콘텐츠(옵션). **TRTCCalling 버전>=1.0.2, tsignaling 버전 >= 0.9.0만 해당** |

[](id:accept)
#### accept()
초대 받은 후, 초대 수락에 사용됩니다.

>?
>- 이전 invitation이 처리되지 않은 경우, 컴포넌트가 기본적으로 ‘회선 통화 중’을 나타내는 메시지를 반환합니다.
>- v1.0.0 및 이후 버전은 params 매개변수가 취소되었습니다.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // v1.0.0 이전 버전
  const { roomID, callType } = inviteData;
  trtcCalling.accept({inviteID, roomID, callType})
  // v1.0.0 및 이후 버전
  trtcCalling.accept();
})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형   | 의미                                                  |
| -------- | ------ | ----------------------------------------------------- |
| inviteID | String | 초대 식별 ID(수신 이벤트 INVITED의 콜백 데이터 inviteID). **v1.0.0 이전 버전에만 해당**    |
| roomID   | Number | 통화방 ID(수신 이벤트 INVITED의 콜백 데이터에 대한 inviteData.roomID). **v1.0.0 이전 버전에만 해당**            |
| callType | Number  | 1: 음성 통화, 2: 영상 통화(수신 이벤트 INVITED 콜백 데이터 inviteData.callType). **v1.0.0이전 버전만 해당** |


[](id:reject)
#### reject()
초대 받은 후, 초대 거절에 사용됩니다.

>?v1.0.0 및 이후 버전은 params 매개변수가 취소되었습니다.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
trtcCalling.on(TRTCCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  // v1.0.0 이전 버전
  const { callType } = inviteData;
  trtcCalling.reject({inviteID, isBusy, callType})
  // v1.0.0 및 이후 버전
  trtcCalling.reject();
})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미                                                  |
| -------- | ------- | ----------------------------------------------------- |
| inviteID | String  |  초대 식별 ID(수신 이벤트 INVITED의 콜백 데이터 inviteID). **v1.0.0 이전 버전에만 해당**   |
| isBusy   | Boolean | 통화 중 여부. **v1.0.0 이전 버전만 해당**             |
| callType | Number  | 1: 음성 통화, 2: 영상 통화(수신 이벤트 INVITED 콜백 데이터 inviteData.callType). **v1.0.0이전 버전만 해당** |

[](id:hangup)
#### hangup()
1. 현재 통화 중인 경우 이 API를 호출하여 통화를 종료할 수 있습니다.
2. 아직 연결되지 않은 경우, 이 API를 호출하여 통화를 취소할 수 있습니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.hangup()
:::
</dx-codeblock>


### 비디오 제어 API 
[](id:startRemoteView)
#### startRemoteView({userID, videoViewDomID})
지정된 DOM ID 노드에서 원격 사용자의 카메라 데이터를 렌더링하는데 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수           | 유형   | 의미                                                      |
| -------------- | ------ | --------------------------------------------------------- |
| userID         | String | 사용자 ID                                                   |
| videoViewDomID | String | 사용자의 데이터가 렌더링될 DOM ID 노드. 데이터는 노드의 video 태그를 통해 재생됩니다. |

[](id:stopRemoteView)
#### stopRemoteView({userID})
원격 사용자의 카메라 데이터를 렌더링된 DOM 노드에서 삭제하는데 사용됩니다.

>?v1.0.0 및 이후 버전은 videoViewDomID 매개변수가 제거되었습니다.

<dx-codeblock>
::: javascript javascript
// v1.0.0 이전 버전
trtcCalling.stopRemoteView({userID, videoViewDomID});
// v1.0.0 및 이후 버전
trtcCalling.stopRemoteView({userID});

:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수           | 유형   | 의미                                                        |
| -------------- | ------ | ------------------------------------------------------------ |
| userID         | String | 사용자 ID                                                     |
| videoViewDomID | String | video 태그를 삭제할 DOM ID 노드. 비디오 재생이 중지됩니다. **v1.0.0 이전 버전만 해당** |

[](id:startLocalView)
#### startLocalView({userID, videoViewDomID})
로컬 사용자의 카메라 데이터를 지정한 DOM ID 노드로 렌더링하는데 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수           | 유형   | 의미                                                        |
| -------------- | ------ | ----------------------------------------------------------- |
| userID         | String | 사용자 ID                                                     |
| videoViewDomID | String | 로컬 사용자의 데이터가 렌더링될 DOM ID 노드. 데이터는 노드의 video 태그를 통해 재생됩니다.  |

[](id:stopLocalView)
#### stopLocalView({userID})

로컬 사용자의 카메라 데이터를 렌더링된 DOM 노드에서 삭제하는데 사용됩니다.

>?v1.0.0 및 이후 버전은 videoViewDomID 매개변수가 제거되었습니다.

<dx-codeblock>
::: javascript javascript
// v1.0.0 이전 버전
trtcCalling.stopLocalView({userID, videoViewDomID});
// v1.0.0 및 이후 버전
trtcCalling.stopLocalView({userID});
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수           | 유형   | 의미                                                        |
| -------------- | ------ | ------------------------------------------------------------ |
| userID         | String | 사용자 ID                                                     |
| videoViewDomID | String | video 태그를 삭제할 DOM ID 노드. 비디오 재생이 중지됩니다. **v1.0.0 이전 버전만 해당** |

[](id:openCamera)
#### openCamera()
로컬 카메라 켜기에 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.openCamera()
:::
</dx-codeblock>

[](id:closeCamera)
####  closeCamera()
카메라 끄기에 사용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.closeCamera()
:::
</dx-codeblock>

[](id:setMicMute)
####  setMicMute(isMute) 
마이크 켜기/끄기.

<dx-codeblock>
::: javascript javascript
trtcCalling.setMicMute(true) // 마이크 끄기
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미                                         |
| ------ | ------- | -------------------------------------------- |
| isMute | Boolean | <li/>true: 마이크 끄기 <li/> false: 마이크 켜기 |

[](id:setVideoQuality)
####  setVideoQuality(profile) 
비디오 품질 설정에 사용됩니다.
>?  
>- v0.8.0 및 이후 버전에 추가된 API입니다.
>- 이 API는 call, groupCall, accept 이전에 호출되어야 적용됩니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.setVideoQuality('720p') // 비디오 품질을 720p로 설정
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형    | 의미                                         |
| ------ | ------- | -------------------------------------------- |
| profile | String | <li/>480p: 640 × 480 <li/>720p: 1280 × 720  <li/>1080p: 1920 × 1080  |

[](id:switchToAudioCall)
####  switchToAudioCall() 
영상 통화를 음성 통화로 전환하는데 사용됩니다.
>?  
>- v0.10.0 및 이후 버전에 추가된 API입니다.
>- 1v1 통화에서만 지원됩니다.
>- ERROR 이벤트 수신 실패. code: 60001.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToAudioCall() // 영상 통화를 음성 통화로 전환합니다.
:::
</dx-codeblock>

[](id:switchToVideoCall)
####  switchToVideoCall() 
음성 통화를 영상 통화로 전환하는데 사용됩니다.
>?  
>- v0.10.0 및 이후 버전에 추가된 API입니다.
>- 1v1 통화에서만 지원됩니다.
>- ERROR 이벤트 수신 실패, code: 60002.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchToVideoCall() // 음성 통화를 영상 통화로 전환합니다.
:::
</dx-codeblock>

[](id:getCameras)
####  getCameras() 

카메라 디바이스 리스트 가져오기에 사용됩니다.

>?v0.10.0 및 이후 버전에 추가된 API입니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.getCameras() // 카메라 리스트 가져오기
:::
</dx-codeblock>

[](id:getMicrophones)
####  getMicrophones() 

마이크 디바이스 리스트 가져오기에 사용됩니다.

>?v0.10.0 및 이후 버전에 추가된 API입니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.getMicrophones() // 마이크 리스트 가져오기
:::
</dx-codeblock>

[](id:switchDevice)
####  switchDevice({deviceType, deviceId})

카메라 또는 마이크 디바이스 전환에 사용됩니다.

>?v0.10.0 및 이후 버전에 추가된 API입니다.

<dx-codeblock>
::: javascript javascript
trtcCalling.switchDevice({deviceType: 'video', deviceId: deviceId}) // 디바이스 전환
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수       | 유형   | 의미                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| deviceType | String | video: 카메라, audio: 마이크                                 |
| deviceId   | String | <li/>카메라 디바이스 식별은 getCameras()를 통해 가져옵니다<li/>마이크 디바이스 식별은 getMicrophones()를 통해 가져옵니다 |

[](id:event)
## TRTCCalling 이벤트 리스트

다음 코드를 참고하여 [TRTCCalling 컴포넌트 이벤트](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/module-EVENT.html)를 수신할 수 있습니다.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject)
:::
</dx-codeblock>

### 초대 발신자 이벤트

|                     CODE                      |   이벤트 수신자   |           설명            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     초대 발신자     |     초대 수신자가 통화 거절      |
|              [NO_RESP](#no_resp)              |     초대 발신자     |    시간 초과, 초대 수신자 응답 없음     |
|            [LINE_BUSY](#line_busy)            |     초대 발신자     | 초대 수신자 통화 중  |
|              [INVITED](#invited)              |     초대 수신자     |      초대 수신       |
|       [CALLING_CANCEL](#calling_cancel)       |     초대 수신자     |     통화가 취소됨            |
|      [CALLING_TIMEOUT](#calling_timeout)      |     초대 수신자     |    시간 초과, 통화 응답 없음     |
|           [USER_ENTER](#user_enter)           | 초대 발신자 및 수신자 |         사용자 방 입장          |
|           [USER_LEAVE](#user_leave)           | 초대 발신자 및 수신자 |       사용자 방 퇴장        |
|             [CALL_END](#call_end)             | 초대 발신자 및 수신자 |       통화 종료        |
|           [KICKED_OUT](#kicked_out)           | 초대 발신자 및 수신자 |   중복 로그인으로 방에서 퇴장됨    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | 초대 발신자 및 수신자 | 원격 사용자의 카메라 ON/OFF |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | 초대 발신자 및 수신자 | 원격 사용자의 마이크 ON/OFF |

### 일반적인 이벤트 콜백

#### SDK_READY

SDK ready 상태 진입 시, 이 콜백을 수신합니다.

>?v1.0.0 및 이후의 버전은 이 이벤트가 추가됩니다.

<dx-codeblock>
::: javascript javascript
let onSDKReady = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.SDK_READY, onSDKReady);
:::
</dx-codeblock>

#### USER_ENTER

사용자의 방 입장.
트리거 조건: 사용자의 방 입장.

<dx-codeblock>
::: javascript javascript
let handleUserEnter = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_ENTER, handleUserEnter);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID     | String | 사용자 ID      |

#### USER_LEAVE

사용자 방 퇴장.
트리거 조건: 사용자의 방 퇴장.

<dx-codeblock>
::: javascript javascript
let handleUserLeave = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.USER_LEAVE, handleUserLeave);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID     | String | 사용자 ID      |

#### GROUP_CALL_INVITEE_LIST_UPDATE

그룹 채팅의 초대 리스트 업데이트 시, 이 콜백 수신을 수신합니다.

>?v1.0.0 및 이후의 버전은 이 이벤트가 추가됩니다.

<dx-codeblock>
::: javascript javascript
let handleGroupInviteeListUpdate = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.GROUP_CALL_INVITEE_LIST_UPDATE, handleGroupInviteeListUpdate);
:::
</dx-codeblock>

#### CALL_END

통화 종료.
트리거 조건: 통화 종료.

<dx-codeblock>
::: javascript javascript
let handleCallingEnd = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALL_END, handleCallingEnd);
:::
</dx-codeblock>

#### KICKED_OUT

중복 로그인으로 방에서 퇴장됨.
트리거 조건: 다른 페이지에서 중복 로그인.

<dx-codeblock>
::: javascript javascript
let handleKickedOut = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.KICKED_OUT, handleKickedOut);
:::
</dx-codeblock>

#### USER_VIDEO_AVAILABLE

원격 사용자의 카메라 ON/OFF.
트리거 조건: 원격 사용자의 카메라 ON/OFF.

<dx-codeblock>
::: javascript javascript
let handleUserVideoChange = function({userID, isVideoAvailable}) {
  console.log(userID, isVideoAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_VIDEO_AVAILABLE, handleUserVideoChange);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수             | 유형    | 의미                                                        |
| ---------------- | ------- | ----------------------------------------------------------- |
| userID           | String  | 사용자 ID                                                     |
| isVideoAvailable | Boolean | <li/>true: 원격 사용자가 카메라 켬<li/>false: 원격 사용자가 카메라 끔 |

#### USER_AUDIO_AVAILABLE

원격 사용자의 마이크 ON/OFF.
트리거 조건: 원격 사용자의 마이크 ON/OFF.

<dx-codeblock>
::: javascript javascript
let handleUserAudioChange = function({userID, isAudioAvailable}) {
  console.log(userID, isAudioAvailable)
};
trtcCalling.on(TRTCCalling.EVENT.USER_AUDIO_AVAILABLE, handleUserAudioChange);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수             | 유형    | 의미                                                          |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID           | String  | 사용자 ID                                                       |
| isAudioAvailable | Boolean | <li/>true: 원격 사용자가 마이크 켬 <li/> false: 원격 사용자가 마이크 끔 |

### 초대 발신자 이벤트 콜백

#### REJECT

사용자의 통화 거절.
트리거 조건: 초대된 사용자의 통화 거절. 발신자는 REJECT 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleInviteeReject = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.REJECT, handleInviteeReject);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID     | String | 사용자 ID      |

#### NO_RESP

초대 받은 사용자 응답 없음.
트리거 조건: call/groupCall에 timeout이 설정된 경우, 초대 수신자가 timeout 내에 수신하지 않으면 발신자는 NO_RESP 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleNoResponse = function({userID, userIDList}) {
  console.log(userID, userIDList)
};
trtcCalling.on(TRTCCalling.EVENT.NO_RESP, handleNoResponse);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수       | 유형   | 의미         |
| ---------- | ------ | ------------ |
| userID     | String | 사용자 ID      |
| userIDList | Array  | 시간 초과 사용자 리스트 |

#### LINE_BUSY

초대된 수신자 통화 중.
트리거 조건: 초대 수신자가 이미 통화 중. 발신자는 LINE_BUSY 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleLineBusy = function({userID}) {
  console.log(userID)
};
trtcCalling.on(TRTCCalling.EVENT.LINE_BUSY, handleLineBusy);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID     | String | 사용자 ID      |

### 초대 수신자 이벤트 콜백

#### INVITED

초대 수신.
트리거 조건: 통화 초대 수신. 초대된 사용자는 INVITED 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleNewInvitationReceived = function({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {
  console.log(sponsor, userIDList, isFromGroup, inviteData, inviteID)
};
trtcCalling.on(TRTCCalling.EVENT.INVITED, handleNewInvitationReceived);
:::
</dx-codeblock>

매개변수 리스트는 다음과 같습니다.

| 매개변수        | 유형    | 의미                                                                                                     |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | 초대 발신자                                                                                                   |
| userIDList  | Array   | 동시에 초대를 수신한 사용자                                                                                         |
| isFromGroup | Boolean | IM 그룹 초대 여부                                                                                         |
| inviteData  | Object  | <li/>신규 사용자 초대: {version, callType, roomID} <li/> 마지막으로 통화를 종료한 사용자: {version, callType, callEnd} |
| inviteID    | String | 초대 식별 ID.                                                                                    |

#### CALLING_CANCEL

통화가 취소됨.
트리거 조건: 발신 중 통화가 취소됨. 초대된 사용자는 CALLING_CANCEL 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleCallingCancel = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_CANCEL, handleCallingCancel);
:::
</dx-codeblock>

#### CALLING_TIMEOUT

통화 응답 시간 초과.
트리거 조건: call/groupCall이 timeout으로 설정된 경우, 초대 수신자가 timeout 내에 수신하지 않으면 초대 수신자는 CALLING_TIMEOUT 이벤트 콜백을 수신함.

<dx-codeblock>
::: javascript javascript
let handleCallingTimeout = function(event) {
  console.log(event)
};
trtcCalling.on(TRTCCalling.EVENT.CALLING_TIMEOUT, handleCallingTimeout);
:::
</dx-codeblock>

## TRTCCalling 에러 코드 리스트

EVENT의 ERROR 필드 수신을 통해 컴포넌트에서 발생하는 오류를 처리할 수 있습니다. 예시 코드는 다음과 같습니다.

<dx-codeblock>
::: javascript javascript
import TRTCCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error)
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
:::
</dx-codeblock>

#### Error code

| code  | 오류 유형     | 의미                       |
| ----- | ------------ | -------------------------- |
| 60001     | 메소드 호출 실패  | switchToAudioCall 호출 실패 |
| 60002     | 메소드 호출 실패  | switchToVideoCall 호출 실패 |
| 60003 | 권한 획득 실패 | 사용 가능한 마이크 디바이스 없음.      |
| 60004 | 권한 획득 실패 | 사용 가능한 카메라 디바이스가 없음.        |
| 60005 | 권한 획득 실패 | 사용자가 디바이스 사용을 금지함.           |
| 60006 | 환경 점검 실패 | 현재 환경은 WebRTC 미지원(>=v1.0.4버전)      |

## 업데이트 가이드

- **TRTCCalling 버전 업데이트 >= 1.0.2**
	- 참고: TSignaling 버전 업데이트 필요 >= 0.9.0
	- 원인: [업데이트 로그](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/tutorial-CHANGELOG.html#h2-3)
- **1.0.2 >= TRTCCalling 버전 업데이트 >=1.0.0**
	- 참고: TSignaling 버전 업데이트 필요 >= 0.8.0
	- 원인: [업데이트 로그](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/tutorial-CHANGELOG.html#h2-5)

## FAQ

#### 통화 연결이 되지 않거나 로그아웃되는 이유는 무엇입니까?
현재 컴포넌트에서는 다중 인스턴스 로그인 및 **오프라인 신호 전송** 기능을 지원하지 않습니다. 현재 로그인되어 있는 계정의 유일성을 확인하십시오.
> ?
> - **다중 인스턴스**: 1개의 UserID로 중복 로그인하거나 여러 단말에서 로그인하는 경우 신호에 혼란이 발생합니다.
> - **오프라인 푸시**: 온라인 인스턴스만 메시지를 수신할 수 있습니다. 오프라인 인스턴스로 전송된 메시지는 인스턴스의 온라인 상태 전환 후 다시 전송되지 않습니다.
더 많은 FAQ는 [TRTCCalling Web FAQ](https://intl.cloud.tencent.com/document/product/647/43096)를 참고하십시오.

## 기술 컨설팅
자세한 내용은 [고객센터](https://intl.cloud.tencent.com/contact-us)를 참고하십시오. 또는 colleenyu@tencent.com 으로 이메일을 보내주십시오.


## 참고 문서
- [TRTCCalling web 공식 웹사이트 체험](https://web.sdk.qcloud.com/component/trtccalling/demo/web/latest/index.html#/login)
- [TRTCCalling npm](https://www.npmjs.com/package/trtc-calling-js)
- [TRTCCalling web demo 소스 코드](https://github.com/tencentyun/TRTCSDK/tree/master/Web/TRTCScenesDemo/trtc-calling-web)
- [TRTCCalling web API](https://web.sdk.qcloud.com/component/trtccalling/doc/web/zh-cn/TRTCCalling.html)
- [TRTCCalling web 관련 질문](https://intl.cloud.tencent.com/document/product/647/43096)
