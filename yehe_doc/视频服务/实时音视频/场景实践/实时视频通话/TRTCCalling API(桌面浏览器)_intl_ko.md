## TRTCCalling 소개

[TRTCCalling](https://www.npmjs.com/package/trtc-calling-js) 모듈은 Tencent Cloud TRTC와 IM 서비스를 기반으로 조합하여 구성되며, 1대1 및 다중 사용자 비디오/음성 통화를 지원합니다. 자세한 구현 방법은 [실시간 비디오 통화(데스크톱 브라우저)](https://intl.cloud.tencent.com/document/product/647/38927)를 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)를 사용하는 저 딜레이 멀티미디어 통화 모듈입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/zh/document/product/1047)를 사용하여 신호 정보를 발송 및 처리합니다.

## TRTCCalling API 

#### 이벤트 구독/구독 취소 관련 인터페이스 함수 

본 모듈은 이벤트 배포를 기반으로 관리하며, 응용 레이어는 모듈이 전달하는 이벤트에 따라 인터랙티브하게 변경할 수 있습니다.

| API                                                                         | 설명         |
| --------------------------------------------------------------------------- | ------------ |
| [on(eventName, callback, context)](#on(eventname.2C-callback.2C-context))   | 이벤트 구독     |
| [off(eventName, callback, context)](#off(eventname.2C-callback.2C-context)) | 이벤트 구독 취소 |

#### SDK 기본 함수

| API                                                         | 설명                                           |
| ----------------------------------------------------------- | ---------------------------------------------- |
| [login({userID, userSig})](#login(.7Buserid.2C-usersig.7D)) | IM 인터페이스에 로그인, 모든 기능은 먼저 로그인 한 후 사용할 수 있음 |
| [logout()](#logout())                                       | 인터페이스에 로그인, 로그인 후 다시 발신 작업을 할 수 없음            |

#### 통화 작업 관련 인터페이스 함수

| API                                                                                       | 설명         |
| ----------------------------------------------------------------------------------------- | ------------ |
| [call({userID, type, timeout}))](#call(.7Buserid.2C-type.2C-timeout.7D))                  | 1명에게 통화 초대 |
| [groupCall({userIDList, type, groupID})](#groupcall(.7Buseridlist.2C-type.2C-groupid.7D)) | 그룹 통화 초대 |
| [accept({inviteID, roomID, callType})](#accept(.7Binviteid.2C-roomid.2C-calltype.7D))     | 통화 초대 수락 |
| [reject({inviteID, isBusy, callType})](#reject(.7Binviteid.2C-isbusy.2C-calltype.7D))     | 통화 초대 거절 |
| [hangup()](#hangup())                                                                     | 현재 통화 끊기 |

#### 비디오 제어 관련 인터페이스 함수

| API                                                                                           | 설명               |
| --------------------------------------------------------------------------------------------- | ------------------ |
| [startRemoteView({userID, videoViewDomID})](#startremoteview(.7Buserid.2C-videoviewdomid.7D)) | 원격 화면 렌더링 실행   |
| [stopRemoteView({userID, videoViewDomID})](#stopremoteview(.7Buserid.2C-videoviewdomid.7D))   | 원격 화면 렌더링 중지   |
| [startLocalView({userID, videoViewDomID})](#startlocalview(.7Buserid.2C-videoviewdomid.7D))   | 로컬 화면 렌더링 실행   |
| [stopLocalView({userID, videoViewDomID})](#stoplocalview(.7Buserid.2C-videoviewdomid.7D))     | 로컬 화면 렌더링 중지   |
| [openCamera()](#opencamera())                                                                 | 카메라 실행         |
| [closeCamera()](#closecamera())                                                               | 카메라 끄기         |
| [setMicMute(isMute)](#setmicmute(ismute))                                                     | 디바이스 마이크 음소거 여부 |


## TRTCCalling 상세 설명

### TRTCCalling 모듈 인스턴스 생성

먼저 [TRTC 콘솔](https://console.cloud.tencent.com/trtc/app)에서 애플리케이션을 생성하여 SDKAppID를 획득합니다.
생성 후, `new TRTCCalling()`을 통해 TRTCCalling 모듈 인스턴스를 획득할 수 있습니다.

```javascript javascript
let options = {
  SDKAppID: 0 // 액세스 시 0이 IM 어플리케이션의 SDKAppID로 대체됩니다.
};
let trtcCalling = new TRTCCalling(options);
```

### 이벤트 구독/구독 취소 관련 인터페이스 함수 




#### on(eventName, callback, context)

리스너 모듈에서 전송하는 이벤트에 사용되며, 이벤트에 대한 자세한 사항은 [이벤트 리스트](#event)를 확인하십시오.

```javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.on('onInvited', handleInvite, this);
```




#### off(eventName, callback, context)

이벤트 리스너 취소에 사용

```javascript javascript
let handleInvite = function ({inviteID, sponsor, inviteData}) {
    console.log(`inviteID: ${inviteID}, sponsor: ${sponsor}, inviteData: ${JSON.stringify(inviteData)}`);
};
trtcCalling.off('onInvited', handleInvite, this);
```

### SDK 기본 함수

#### login({userID, userSig})

로그인 인터페이스

```javascript javascript
trtcCalling.login({userID, userSig})
```

매개변수 리스트

| 매개변수    | 유형   | 의미                                                                                                                    |
| ------- | ------ | ----------------------------------------------------------------------------------------------------------------------- |
| userID  | String | 현재 사용자 ID, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(\_)만 허용됩니다.|
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |




#### logout()

 로그아웃 인터페이스

```javascript javascript
trtcCalling.logout()
```

### 통화 작업 관련 인터페이스 함수




#### call({userID, type, timeout})

1대1 통화 초대에서 type은 통화 유형으로, 1-음성 통화, 2-비디오 통화

```javascript javascript
trtcCalling.call({userID, type, timeout})
```

매개변수 리스트

| 매개변수    | 유형   | 의미                     |
| ------- | ------ | ------------------------ |
| userID  | String | 초대된 사용자의 userID          |
| type    | Number | 1: 음성 통화, 2: 비디오 통화 |
| timeout | Number | 시간 미초과 시 0, 단위: s(초)  |



#### groupCall({userIDList, type, groupID})
groupID 매개변수는 IM SDK 상의 그룹 ID로, 해당 매개변수를 입력하는 경우 통화 요청 정보가 그룹 정보 시스템을 통해 전송됩니다. 해당 정보 전송 방식은 비교적 간단하면서 신뢰성이 높습니다. 입력하지 않는 경우 TRTCCalling 모듈이 개별 발송 방식을 사용하여 1개씩 통지합니다.

```javascript javascript
trtcCalling.groupCall({userIDList, type, groupID})
```

매개변수 리스트

| 매개변수       | 유형   | 의미                     |
| ---------- | ------ | ------------------------ |
| userIDList | Array  | 초대 리스트                 |
| type       | Number | 1: 음성 통화, 2: 비디오 통화 |
| groupID    | String | IM 그룹 ID(선택사항)       |




#### accept({inviteID, roomID, callType})
초대 받은 후, 해당 인터페이스를 호출하여 해당 초대를 허락합니다.
>? 이전 invitation을 처리하지 않은 경우 모듈이 기본적으로 회선을 점유하여 이후의 초대들에 대해 모두 통화 중을 회신합니다.

```javascript javascript
import TrtcCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.accept({inviteID, roomID, callType})
})
```

매개변수 리스트

| 매개변수     | 유형   | 의미                     |
| -------- | ------ | ------------------------ |
| inviteID | String | 초대 ID, 초대 1회 식별    |
| roomID   | Number | 통화 방 번호 ID            |
| callType | Number | 1: 음성 통화, 2: 비디오 통화 |



#### reject({inviteID, isBusy, callType})
초대 받은 후, 해당 인터페이스를 호출하여 해당 초대를 거절합니다.

```javascript javascript
import TrtcCalling from 'trtc-calling-js';
trtcCalling.on(TrtcCalling.EVENT.INVITED, ({inviteID, sponsor, inviteData}) => {
  // ...
  trtcCalling.reject({inviteID, isBusy, callType})
})
```

매개변수 리스트

| 매개변수     | 유형    | 의미                     |
| -------- | ------- | ------------------------ |
| inviteID | String  | 초대 ID, 초대 1회 식별    |
| isBusy   | Boolean | 통화 중 여부             |
| callType | Number  | 1: 음성 통화, 2: 비디오 통화 |


#### hangup()
1. 현재 통화 중인 경우 해당 함수를 호출하여 전화를 종료할 수 있습니다.
2. 통화 미연결 시 통화 취소로도 사용할 수 있습니다.

```javascript javascript
trtcCalling.hangup()
```


### 비디오 제어 관련 인터페이스 함수
#### startRemoteView({userID, videoViewDomID})
원격 사용자의 카메라 데이터를 지정한 DOM ID 노드로 렌더링합니다.

``` javascript javascript
trtcCalling.startRemoteView({userID, videoViewDomID})
```

매개변수 리스트

| 매개변수           | 유형   | 의미                                                      |
| -------------- | ------ | --------------------------------------------------------- |
| userID         | String | 사용자 ID                                                   |
| videoViewDomID | String | 해당 사용자 데이터는 해당 DOM ID 노드에 렌더링되는 video 태그를 통해 재생됩니다. |

#### stopRemoteView({userID, videoViewDomID})
원격 사용자의 카메라 데이터를 렌더링된 DOM 노드에서 삭제합니다.

``` javascript javascript
trtcCalling.stopRemoteView({userID, videoViewDomID})
```

매개변수 리스트

| 매개변수           | 유형   | 의미                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | 사용자 ID                                           |
| videoViewDomID | String | 해당 DOM ID 노드의 video 태그를 제거하여 비디오 재생을 중지합니다. |

#### startLocalView({userID, videoViewDomID})
로컬 사용자의 카메라 데이터를 지정한 DOM ID 노드로 렌더링합니다.

```javascript javascript
trtcCalling.startLocalView({userID, videoViewDomID})
```

매개변수 리스트

| 매개변수           | 유형   | 의미                                                        |
| -------------- | ------ | ----------------------------------------------------------- |
| userID         | String | 사용자 ID                                                     |
| videoViewDomID | String | 로컬 사용자 데이터는 해당 DOM ID 노드에 렌더링되는 video 태그를 통해 재생됩니다. |

#### stopLocalView({userID, videoViewDomID})

로컬 사용자의 카메라 데이터를 렌더링된 DOM 노드에서 삭제합니다.

``` javascript javascript
trtcCalling.stopLocalView({userID, videoViewDomID})
```

매개변수 리스트

| 매개변수           | 유형   | 의미                                              |
| -------------- | ------ | ------------------------------------------------- |
| userID         | String | 사용자 ID                                           |
| videoViewDomID | String | 해당 DOM ID 노드의 video 태그를 제거하여 비디오 재생을 중지합니다. |

#### openCamera()
로컬 카메라 켜기

```javascript javascript
trtcCalling.openCamera()
```

####  closeCamera()
카메라 끄기

``` javascript javascript
trtcCalling.closeCamera()
```

####  setMicMute(isMute) 
마이크 켜기/끄기

```javascript javascript
trtcCalling.setMicMute(true) // 마이크 켬
```

매개변수 리스트

| 매개변수   | 유형    | 의미                                         |
| ------ | ------- | -------------------------------------------- |
| isMute | Boolean | <li/>true: 마이크 끔 <li/>false: 마이크 켬 |


[](id:event)
## TRTCCalling 이벤트 리스트

다음 코드를 참조하여 TRTCCalling 모듈에서 전송되는 각 종 이벤트를 캐치할 수 있습니다.

```javascript javascript
import TrtcCalling from 'trtc-calling-js';
// etc
function handleInviteeReject({userID}) {

}
trtcCalling.on(TrtcCalling.EVENT.REJECT, handleInviteeReject)
```

### 초대 발신자 이벤트

|                     CODE                      |   이벤트 수신자   |           설명            |
| :-------------------------------------------: | :------------: | :-----------------------: |
|               [REJECT](#reject)               |     초대 발신자     |     초대 수신자가 통화 거절      |
|              [NO_RESP](#no_resp)              |     초대 발신자     |    초대 수신자의 응답 시간 초과     |
|            [LINE_BUSY](#line_busy)            |     초대 발신자     | 초대 수신자가 현재 통화 중인 상태  |
|              [INVITED](#invited)              |     초대 수신자     |      초대 통지 수신       |
|       [CALLING_CANCEL](#calling_cancel)       |     초대 수신자     |     해당 통화 취소됨      |
|      [CALLING_TIMEOUT](#calling_timeout)      |     초대 수신자     |    해당 통화 응답 시간 초과     |
|           [USER_ENTER](#user_enter)           | 초대 발신자 및 수신자 |         사용자 방 입장          |
|           [USER_LEAVE](#user_leave)           | 초대 발신자 및 수신자 |       사용자 방 퇴장        |
|             [CALL_END](#call_end)             | 초대 발신자 및 수신자 |       이번 통화 종료        |
|           [KICKED_OUT](#kicked_out)           | 초대 발신자 및 수신자 |   중복 로그인으로 방에서 퇴장됨    |
| [USER_VIDEO_AVAILABLE](#user_video_available) | 초대 발신자 및 수신자 | 원격 사용자가 카메라 켬/끔 |
| [USER_AUDIO_AVAILABLE](#user_audio_available) | 초대 발신자 및 수신자 | 원격 사용자가 마이크 켬/끔 |

### 범용 이벤트 콜백

#### USER_ENTER

사용자 방 입장

```javascript javascript
function handleUserEnter({userID}) {

}
```

매개변수 리스트

|매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID | String | 사용자 ID |

#### USER_LEAVE

사용자 방 퇴장

``` javascript javascript
function handleUserLeave({userID}) {

}
```

매개변수 리스트

|매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID | String | 사용자 ID |

#### CALL_END

이번 통화 종료

```javascript javascript
function handleCallEnd() {

}
```

#### KICKED_OUT

중복 로그인으로 방에서 퇴장됨

```javascript javascript
function handleKickedOut() {

}
```

#### USER_VIDEO_AVAILABLE

원격 사용자가 카메라 켬/끔

```javascript javascript
function handleUserVideoChange({userID, isVideoAvailable}) {

}
```

매개변수 리스트

| 매개변수             | 유형    | 의미                                                        |
| ---------------- | ------- | ----------------------------------------------------------- |
| userID           | String  | 사용자 ID                                                     |
| isVideoAvailable | Boolean | <li/>true: 원격 사용자가 카메라 켬<li/>false: 원격 사용자가 카메라 끔 |

#### USER_AUDIO_AVAILABLE

원격 사용자가 마이크 켬/끔

```javascript javascript
function handleUserAudioChange({userID, isAudioAvailable}) {

}
```

매개변수 리스트

| 매개변수             | 유형    | 의미                                                          |
| ---------------- | ------- | ------------------------------------------------------------- |
| userID           | String  | 사용자 ID                                                       |
| isAudioAvailable | Boolean | <li/>true: 원격 사용자가 마이크 켬 <li/> false: 원격 사용자가 마이크 끔 |

### 초대 발신자 이벤트 콜백

#### REJECT

사용자가 통화 거절

```javascript javascript
function handleInviteeReject({userID}) {

}
```

매개변수 리스트

|매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID | String | 사용자 ID |

#### NO_RESP

초대한 사용자 응답 없음

```javascript javascript
function handleNoResponse({userID, userIDList}) {

}
```

매개변수 리스트

|매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID | String | 사용자 ID |
| userIDList | Array  | 시간 초과 사용자 리스트 |

#### LINE_BUSY

초대 수신자가 현재 통화 중인 상태

``` javascript javascript
function handleInviteeLineBusy({userID}) {

}
```

매개변수 리스트

|매개변수   | 유형   | 의미    |
| ------ | ------ | ------- |
| userID | String | 사용자 ID |

### 초대 수신자 이벤트 콜백

#### INVITED
초대 통지 수신

```javascript javascript
function handleNewInvitationReceived({
    sponsor, userIDList, isFromGroup, inviteData, inviteID
}) {

}
```

매개변수 리스트

| 매개변수        | 유형    | 의미                                                                                                       |
| ----------- | ------- | ---------------------------------------------------------------------------------------------------------- |
| sponsor     | String  | 초대 발신자                                                                                                     |
| userIDList  | Array   | 동시에 초대를 수신한 사용자                                                                                           |
| isFromGroup | Boolean | IM 그룹 초대 여부                                                                                           |
| inviteData  | Object  | <li/>신규 사용자 초대: {version, callType, roomID} <li/> 마지막 사용자 종료: {version, callType, callEnd} |
| inviteID    | String  | 초대 ID, 초대 1회 식별                                                                                      |

#### CALLING_CANCEL

해당 통화 취소됨

```javascript javascript
function handleInviterCancel() {

}
```

#### CALLING_TIMEOUT

이번 통화 응답 시간 초과

```javascript javascript
function handleCallTimeout() {

}
```

## TRTCCalling 에러 코드 리스트

리스너 이벤트의 ERROR 필드를 통해 모듈에서 발생하는 오류를 처리할 수 있습니다. 예시 코드는 다음과 같습니다.

```javascript javascript
import TrtcCalling from 'trtc-calling-js';
let onError = function(error) {
  console.log(error)
};
trtcCalling.on(TRTCCalling.EVENT.ERROR, onError);
```

## FAQ

#### 통화 연결이 되지 않거나 로그아웃되는 이유는 무엇입니까?
현재 모듈에서는 다중 인스턴스 로그인 및 **오프라인 신호 전송** 기능을 지원하지 않습니다. 로그인 계정이 고유한지 확인하십시오.
> ?
> - **다중 인스턴스**: 1개의 UserID로 중복 로그인하거나 서로 다른 단말기에서 로그인하는 경우 신호에 혼란이 발생합니다.
> - **오프라인 전송**: 인스턴스는 온라인에서만 정보를 수신할 수 있으며, 오프라인 시 수신한 신호는 온라인 시 중복 전송되지 않습니다.
