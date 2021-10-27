TRTCLiveRoom은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM)을 기반으로 하며, 다음 기능을 지원합니다.

- 호스트가 신규 라이브 룸을 생성하면 시청자가 라이브 룸에 입장해 시청.
- 호스트와 시청자가 비디오의 마이크를 연결해 소통 가능.
- 서로 다른 두 라이브 룸간에 호스트 PK 연결.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 지원, 사용자 정의 메시지를 이용해 댓글 자막, 좋아요, 선물 기능 구현 가능.

TRTCLiveRoom은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [비디오 마이크 연결 라이브 방송(Flutter)](https://intl.cloud.tencent.com/document/product/647/41944)을 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615)를 저지연 라이브 방송 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)의 AVChatroom을 이용해 라이브 방송 채팅방 기능을 구현하고, IM 메시지를 통해 호스트 간의 마이크 연결 프로세스를 연결합니다.

[](id:TRTCLiveRoom)

## TRTCLiveRoom API 개요

### SDK 기본 함수

| API                                             | 설명                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | 컴포넌트 싱글톤 가져오기.           |
| [destroySharedInstance](#destroysharedinstance) | 컴포넌트 싱글톤 폐기.          |
| [registerListener](#registerlistener)           | 이벤트 콜백 설정.           |
| [unRegisterListener](#unregisterlistener)       | 이벤트 콜백 스레드 설정. |
| [login](#login)                                 | 로그인.                   |
| [logout](#logout)                               | 로그아웃.                   |
| [setSelfProfile](#setselfprofile)               | 개인 프로필 정보 수정.           |

### 방 관련 API

| API                                     | 설명                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | 방 생성(호스트 호출). 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방 생성. |
| [destroyRoom](#destroyroom)             | 방 폐기(호스트 호출).                                       |
| [enterRoom](#enterroom)                 | 방 입장(시청자 호출).                                       |
| [exitRoom](#exitroom)                   | 방 퇴장(시청자 호출).                                       |
| [getRoomInfos](#getroominfos)       | 방 리스트의 상세 정보 획득.                                     |
| [getAnchorList](#getanchorlist)     | 방 안의 모든 호스트 리스트 획득. enterRoom() 성공 후 호출해야만 유효.     |
| [getRoomMemberList](#getroommemberlist) | 방 안의 모든 참석자 정보 획득. enterRoom() 성공 후 호출해야만 유효.     |

### 푸시/풀 스트림 관련 API

| API                                       | 설명                                               |
| ----------------------------------------- | -------------------------------------------------- |
| [startCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작.                           |
| [stopCameraPreview](#stopcamerapreview)   | 로컬 비디오 수집 및 미리보기 종료.                           |
| [startPublish](#startpublish)             | 라이브 방송 시작(푸시 스트림).                                 |
| [stopPublish](#stoppublish)               | 라이브 방송 중단(푸시 스트림).                                 |
| [startPlay](#startplay)                   | 원격 비디오 화면 재생. 일반 시청 및 마이크 연결 시나리오에서 호출 가능. |
| [stopPlay](#stopplay)                     | 원격 비디오 화면 렌더링 중단.                             |

### 호스트와 시청자 마이크 연결

| API                                       | 설명               |
| ----------------------------------------- | ------------------ |
| [requestJoinAnchor](#requestjoinanchor)   | 시청자 마이크 연결 요청.     |
| [responseJoinAnchor](#responsejoinanchor) | 호스트가 마이크 연결 요청 처리. |
| [kickoutJoinAnchor](#kickoutjoinanchor)   | 호스트가 시청자 마이크 연결 강제 해제. |

### 호스트 크로스 룸 PK

| API                               | 설명                   |
| --------------------------------- | ---------------------- |
| [requestRoomPK](#requestroompk)   | 호스트가 크로스 룸 PK 요청.      |
| [responseRoomPK](#responseroompk) | 호스트가 크로스 룸 PK 요청에 응답. |
| [quitRoomPK](#quitroompk)         | 크로스 룸 PK 퇴장.          |

### 멀티미디어 제어 관련 API

| API                                       | 설명               |
| ----------------------------------------- | ------------------ |
| [switchCamera](#switchcamera)             | 전면/후면 카메라 전환.   |
| [setMirror](#setmirror)                   | 미러 이미지 표시 여부 설정. |
| [muteLocalAudio](#mutelocalaudio)         | 로컬 오디오 음소거.    |
| [muteRemoteAudio](#muteremoteaudio)       | 원격 오디오 음소거.  |
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 원격 오디오 음소거. |

### 배경 음악 음향 효과 관련 API

| API                                             | 설명                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html) 가져오기. |

### 뷰티 필터 관련 API

| API                                   | 설명                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html) 가져오기. |

### 메시지 발송 관련 API

| API                                     | 설명                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용. |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송.                     |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API 개요</h2>

### 일반적인 이벤트 콜백

| API                                 | 설명                               |
| ----------------------------------- | ---------------------------------- |
| [onError](#onerror)                 | 오류 콜백.                         |
| [onWarning](#onwarning)             | 경고 콜백.                         |
| [onKickedOffline](#onkickedoffline) | 다른 사용자가 동일한 계정으로 로그인 시 강제 로그아웃. |

### 방 이벤트 콜백

| API                                           | 설명                                                 |
| --------------------------------------------- | ---------------------------------------------------- |
| [onEnterRoom](#onenterroom)                   | 로컬 방 입장 콜백.                                       |
| [onUserVideoAvailable](#onuservideoavailable) | 원격 사용자가 메인 스트림에 재생 가능한 비디오를 가지고 있는지 여부(일반적으로 카메라에 사용됨). |
| [onRoomDestroy](#onroomdestroy)               | 방 폐기 콜백.                                   |

### 호스트와 시청자 방 입장/퇴장 이벤트 콜백

| API                                 | 설명                 |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter)     | 새로운 호스트 방 입장 알림 수신. |
| [onAnchorExit](#onanchorexit)       | 호스트 퇴장 알림 수신.   |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 알림 수신. |
| [onAudienceExit](#onaudienceexit)   | 시청자 퇴장 알림 수신.   |

### 호스트와 시청자 마이크 연결 이벤트 콜백

| API                                         | 설명                           |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | 호스트가 시청자의 마이크 연결 요청을 수신할 때의 콜백. |
| [onAnchorAccepted](#onanchoraccepted)       | 호스트가 시청자 마이크 연결 요청 수락.       |
| [onAnchorRejected](#onanchorrejected)       | 호스트가 시청자 마이크 연결 요청 거절.       |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | 마이크가 연결된 시청자가 마이크 연결 강제 해제 알림 수신. |

### 호스트 PK 이벤트 콜백

| API                                   | 설명                   |
| ------------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | 크로스 룸 PK 요청 알림 수신. |
| [onRoomPKAccepted](#onroompkaccepted) | 호스트가 크로스 룸 PK 요청 수락. |
| [onRoomPKRejected](#onroompkrejected) | 호스트가 크로스 룸 PK 요청 거부. |
| [onQuitRoomPK](#onquitroompk)       | 크로스 룸 PK 종료 알림 수신. |

### 메시지 이벤트 콜백

| API                                         | 설명             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | 텍스트 메시지 수신.   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신. |

## SDK 기본 함수

### sharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) 싱글톤 객체를 가져옵니다.

```java
 static Future<TRTCLiveRoom> sharedInstance()
```

### destroySharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) 싱글톤 객체를 폐기합니다.

>?인스턴스 폐기 후에는 외부에 캐시된 TRTCLiveRoom 인스턴스를 다시 사용할 수 없으며, 다시 [sharedInstance](#sharedinstance)를 호출해 새로운 인스턴스를 획득해야 합니다.

```java
static void destroySharedInstance()
```

### registerListener

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944) 이벤트 콜백은 TRTCLiveRoomDelegate를 통해 [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/41944)의 다양한 상태 알림을 받아볼 수 있습니다.

```java
void registerListener(VoiceListenerFunc func);
```

>?registerListener는 TRTCLiveRoom의 프록시 콜백입니다.   


### unRegisterListener

모듈 이벤트 수신 인터페이스 제거.

```java
void unRegisterListener(VoiceListenerFunc func);
```


### login

로그인.

```java
Future<ActionCallback> login(
      int sdkAppId, String userId, String userSig, TRTCLiveRoomConfig config);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형               | 의미                                                         |
| -------- | ------------------ | ------------------------------------------------------------ |
| sdkAppId | int                | TRTC 콘솔 >[[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]> 애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | String         | 현재 사용자의 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig | String               | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |
| config   | TRTCLiveRoomConfig | 전체 설정 정보입니다. 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다.<ul style="margin:0;"><li>useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자가 CDN을 통해 시청하도록 설정하며, 요금이 저렴하지만 딜레이가 비교적 많이 발생합니다. false는 일반 시청자 저지연 시청을 설정하며, 요금이 CDN과 마이크 연결 요금의 중간 정도지만 딜레이가 1초 이내로 제어됩니다.</li><li>CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용됩니다. CDN을 시청하는 재생 도메인으로 지정하는 데 사용되며, 라이브 방송 콘솔>[<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a>] 페이지에서 설정할 수 있습니다.</li></ul> |

### logout

로그아웃.

```java
Future<ActionCallback> logout();
```

### setSelfProfile

개인 프로필 정보 수정.

```java
Future<ActionCallback> setSelfProfile(String userName, String avatarURL);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미       |
| --------- | ------ | ---------- |
| userName  | String | 닉네임.     |
| avatarURL | String | 프로필 사진 주소. |

## 방 관련 API

### createRoom

방 생성(호스트 호출).

```java
Future<ActionCallback> createRoom(int roomId, TRTCCreateRoomParam roomParam);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형      | 의미                                                         |
| --------- | --------- | ------------------------------------------------------------ |
| roomId    | int        | 방 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomID를 1개의 라이브 룸 리스트로 통합할 수 있으며, Tencent Cloud는 현재 라이브 룸 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | RoomParam | 방 정보입니다. 방 이름, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. 방 리스트 및 방 정보가 귀하의 서버에서 직접 관리되고 있다면 해당 매개변수는 생략할 수 있습니다. |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 

1. [호스트] `startCameraPreview()`를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다. 
2. [호스트] `createRoom()`을 호출하여 라이브 룸을 생성하면, 생성 여부가 ActionCallback을 통해 호스트에게 통지됩니다.
3. [호스트] `starPublish()`를 호출하여 푸시 스트림을 시작합니다.

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```java
Future<ActionCallback> destroyRoom();
```


### enterRoom

방 입장(시청자 호출).

```java
Future<ActionCallback> enterRoom(int roomId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미       |
| ------ | ---- | ---------- |
| roomId | int  | 방 식별 번호. |

시청자의 정상적인 라이브 방송 시청 호출 프로세스는 다음과 같습니다. 

1. [시청자]가 귀하의 서버에서 최신 라이브 룸 리스트를 획득하며, 여기에는 여러 라이브 룸의 roomID 및 방 정보가 포함될 수 있습니다.
2. [시청자]가 라이브 룸 1개를 선택하고 `enterRoom()`을 호출하여 해당 방으로 입장합니다.
3. [시청자]가 `startPlay(userId)`를 호출하고 호스트의 userId를 전달하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자 측에서 직접 `startPlay(userId)`를 호출하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userId 정보가 포함되어 있어 다시 `startPlay(userId)`를 호출하면 재생됩니다. 

### exitRoom

방 퇴장.

```java
Future<ActionCallback> exitRoom();
```


### getRoomInfos

방 리스트의 상세 정보를 획득합니다. 방 정보는 호스트가 `createRoom()` 시 roomInfo를 통해 설정할 수 있습니다.

>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```java
Future<RoomInfoCallback> getRoomInfos(List<String> roomIdList);
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형               | 의미         |
| ---------- | ------------------ | ------------ |
| roomIdList | List&lt;String&gt; | 방 번호 리스트. |

### getAnchorList

방 안의 모든 호스트 리스트를 획득합니다. enterRoom() 성공 후 호출해야만 유효합니다.

```java
Future<UserListCallback> getAnchorList();
```

### getRoomMemberList

방 안의 모든 시청자 정보를 획득합니다. `enterRoom()` 성공 후 호출해야만 유효합니다.

```java
Future<UserListCallback> getRoomMemberList(int nextSeq)
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형    | 의미                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| nextSeq | int  | 페이징 풀링 식별로, 첫 번째 풀링에 0을 기입하면 콜백 성공 후 nextSeq가 0이 아니면 페이징하고 0이 될 때까지 다시 풀링을 전달합니다. |

   

## 푸시/풀 스트림 관련 API

### startCameraPreview

로컬 비디오 화면 미리보기를 시작합니다.

```java
Future<void> startCameraPreview(bool isFrontCamera, int viewId);
```

매개변수는 다음과 같습니다.

| 매개변수          | 유형 | 의미                                  |
| ------------- | ---- | ------------------------------------- |
| isFrontCamera | bool | true: 전면 카메라, false: 후면 카메라. |
| viewId        | int  | 비디오 view 콜백 ID.                 |

### stopCameraPreview

로컬 비디오 수집 및 미리보기를 종료합니다.

```java
  Future<void> stopCameraPreview();
```

   

### startPublish

라이브 방송(푸시 스트림)을 시작합니다. 다음과 같은 시나리오에 적용할 수 있습니다.
- 호스트가 방송을 시작할 때 호출.
- 시청자가 마이크 연결을 시작할 때 호출.

```java
Future<void> startPublish(String streamId);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형    | 의미                                                         |
| -------- | ------- | ------------------------------------------------------------ |
| streamId | String? | 라이브 방송 CDN의 streamId를 바인딩하는 데 사용. 시청자가 라이브 방송 CDN을 통해 시청하도록 설정하고 싶은 경우 현재 호스트의 라이브 방송 streamId를 지정해야 합니다. |


### stopPublish

라이브 방송(푸시 스트림)을 중단합니다. 다음과 같은 시나리오에 적용할 수 있습니다.
- 호스트가 라이브 방송을 종료할 때 호출.
- 시청자가 마이크 연결을 종료할 때 호출.


```java
Future<void> stopPublish();
```

### startPlay

원격 비디오 화면을 재생합니다. 일반 시청 및 마이크 연결 시나리오에서 호출할 수 있습니다.

```java
Future<void> startPlay(String userId, int viewId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미               |
| ------ | ------ | ------------------ |
| userId | String | 시청하는 사용자 id. |
| viewId | int    | 비디오 view 콜백 id. |

- **일반 시청 시나리오: **
    - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자 측에서 직접 `enterRoom()` 성공 후 `startPlay(userId)`를 호출하여 호스트의 화면을 재생할 수 있습니다.
    - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userId 정보가 포함되어 있어 다시 `startPlay(userId)`를 호출하면 호스트 화면이 재생됩니다.

- **라이브 방송 마이크 연결 시나리오: **
마이크 연결 요청 후 호스트가 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 콜백을 수신하면 콜백에 있는 userId를 사용하여 `startPlay(userId)`를 호출해 마이크 연결 화면을 재생할 수 있습니다.

### stopPlay

원격 비디오 화면의 렌더링을 중단합니다. `onAnchorExit()`가 콜백되면 해당 인터페이스를 호출합니다.

```java
Future<void> stopPlay(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미             |
| ------ | ------ | ---------------- |
| userId | String | 상대방 사용자 정보. |

## 호스트와 시청자 마이크 연결

### requestJoinAnchor

시청자가 마이크 연결을 요청합니다.

```java
Future<ActionCallback> requestJoinAnchor();
```

호스트와 시청자 마이크 연결 프로세스는 다음과 같습니다.

1. [시청자] `requestJoinAnchor()`를 호출하여 호스트에게 마이크 연결을 요청합니다.
2. [호스트] `TRTCLiveRoomDelegate`의 `onRequestJoinAnchor()` 콜백 알림을 수신합니다.
3. [호스트] `responseJoinAnchor()`를 호출하여 시청자가 보낸 마이크 연결 요청을 수락할지 여부를 결정합니다.
4. [시청자] responseCallback 콜백 알림을 수신합니다. 해당 알림은 호스트가 처리한 결과를 포함하고 있습니다.
5. [시청자] 요청이 수락되면 `startCameraPreview()`가 호출되어 로컬 카메라가 켜집니다.
6. [시청자] `startPublish()`를 호출하면 정식으로 푸시 스트림 상태가 됩니다.
7. [호스트] 시청자의 마이크가 연결 상태가 되면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 수신합니다.
8. [호스트] `startPlay()`를 호출하면 마이크가 연결된 시청자의 비디오 화면을 볼 수 있습니다.
9. [시청자] 라이브 룸에 이미 호스트와 마이크가 연결된 다른 시청자가 있는 경우, 새로 마이크가 연결된 시청자는 `onAnchorEnter()` 알림을 수신하며 `startPlay()`를 호출해 다른 마이크가 연결된 사용자의 비디오 화면을 재생할 수 있습니다.

   

### responseJoinAnchor

호스트의 마이크 연결 요청을 처리합니다. `TRTCLiveRoomDelegate`의 `onRequestJoinAnchor()` 콜백 후 해당 인터페이스를 호출하여 시청자의 마이크 연결 요청을 처리합니다.

```java
Future<ActionCallback> responseJoinAnchor(String userId, boolean agreee);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                     |
| ------ | ------ | ------------------------- |
| userId | String | 시청자 ID.                 |
| agree  | bool   | true: 동의, false: 거절. |


### kickoutJoinAnchor

호스트가 시청자의 마이크 연결을 강제 해제합니다. 호스트가 해당 인터페이스를 호출하여 관중의 마이크 연결을 강제 해제하면, 강제 해제된 시청자는 `TRTCLiveRoomDelegate`의 `onKickoutJoinAnchor()` 콜백 알림을 수신합니다.

```java
Future<ActionCallback> kickoutJoinAnchor(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미          |
| ------ | ------ | ------------- |
| userId | String | 마이크가 연결된 시청자 ID. |


## 호스트 크로스 룸 PK

### requestRoomPK

호스트가 크로스 룸 PK를 요청합니다.

```java
Future<ActionCallback> requestRoomPK(int roomId, String userId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | --------------- |
| roomId | int    | 초대된 방 ID. |
| userId | String | 초대된 호스트 ID. |

호스트와 호스트 사이에 크로스 룸 PK를 진행할 수 있으며, 두 정식 라이브 방송의 호스트 A와 B 사이의 크로스 룸 PK 프로세스는 다음과 같습니다.

1. [호스트 A] `requestRoomPK()`을 호출하여 호스트 B에게 마이크 연결을 요청합니다.
2. [호스트 B] `TRTCLiveRoomDelegate`의 `onRequestRoomPK()` 콜백 알림을 수신합니다.
3. [호스트 B] `responseRoomPK()`를 호출하여 호스트 A의 PK 요청을 수락할지 여부를 결정합니다.
4. [호스트 B] 호스트 A의 요청을 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 A의 비디오 화면을 재생합니다.
5. [호스트 A]는 `onRoomPKAccepted` 또는 `onRoomPKRejected` 콜백을 수신합니다.
6. [호스트 A] 요청이 수락된 경우 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 B의 비디오 화면을 재생합니다.

   

### responseRoomPK

호스트가 크로스 룸 PK 요청에 응답합니다. 호스트가 응답하면 상대방 호스트가 `requestRoomPK`에서 전달한 `responseCallback` 콜백을 수신합니다.

```java
Future<ActionCallback> responseRoomPK(String userId, boolean agree);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                      |
| ------ | ------ | ------------------------- |
| userId | String | PK를 요청한 호스트 ID.   |
| agree  | bool   | true: 동의, false: 거절. |


### quitRoomPK

크로스 룸 PK를 종료합니다. PK 중, 한쪽 호스트가 크로스 룸 PK를 종료하면 다른 호스트는 `TRTCLiveRoomDelegate`의 `onQuitRoomPk()` 콜백 알람을 수신합니다.

```java
Future<ActionCallback> quitRoomPK();
```


## 멀티미디어 제어 관련 API

### switchCamera

전면/후면 카메라를 전환합니다.

```java
Future<void> switchCamera(boolean isFrontCamera);
```

### setMirror

미러 이미지 표시 여부를 설정합니다.

```java
Future<void> setMirror(boolean isMirror);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미       |
| -------- | ---- | --------------- |
| isMirror | bool | 미러 이미지 활성화/비활성화. |

   

### muteLocalAudio

로컬 오디오를 음소거합니다.

```java
Future<void> muteLocalAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                                        | 의미                     |
| ---- | ---- | --------------------------------- |
| mute | boolean | true: 음소거 켜기, false: 음소거 끄기.|

   

### muteRemoteAudio

원격 오디오를 음소거합니다.

```java
Future<void> muteRemoteAudio(String userId, boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                              |
| ------ | ------ | --------------------------------- |
| userId  | String | 원격 사용자 ID.                   |
| mute | boolean | true: 음소거, false: 음소거 해제. |

   

### muteAllRemoteAudio

모든 원격 오디오를 음소거합니다.

```java
Future<void> muteAllRemoteAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                                        | 의미                     |
| ---- | ---- | --------------------------------- |
| mute | boolean | true: 음소거, false: 음소거 해제. |

   

## 배경 음악 음향 효과 관련 API

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_audio_effect_manager/TXAudioEffectManager-class.html) 가져오기.

```java
getAudioEffectManager();
```


## 뷰티 필터 관련 API

### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://pub.dev/documentation/tencent_trtc_cloud/latest/tx_beauty_manager/TXBeautyManager-class.html) 가져오기.

```java
getBeautyManager();
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.

- '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
- '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
- 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
- 메이크업 효과를 추가합니다.
- 손 동작을 인식합니다.


## 메시지 발송 관련 API

### sendRoomTextMsg

방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용

```java
Future<ActionCallback> sendRoomTextMsg(String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| message  | String   | 텍스트 메시지.       |

### sendRoomCustomMsg

사용자 정의 텍스트 메시지 발송

```java
Future<ActionCallback> sendRoomCustomMsg(String cmd, String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                                               |
| ------- | ------ | -------------------------------------------------- |
| cmd     | String | 명령어. 개발자가 사용자 정의할 수 있으며, 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String         | 텍스트 메시지.                                         |


## TRTCLiveRoomDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백.

>?SDK가 복구할 수 없는 오류는 반드시 모니터링하고 상황에 따라 적절한 인터페이스를 사용자에게 제시해야 합니다.

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| errCode | int    | 에러 코드.   |
| errMsg  | String | 오류 정보. |


### onWarning

경고 콜백

매개변수는 다음과 같습니다.

| 매개변수        | 유형   | 의미       |
| ----------- | ------ | ---------- |
| warningCode | int    | 에러 코드.   |
| warningMsg  | String | 경고 정보.                                               |


### onKickedOffline

다른 사용자가 동일한 계정으로 로그인 시 강제 로그아웃.




## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백입니다. 호스트가 퇴장하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.

### onEnterRoom

로컬 방 입장

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                                 |
| ------ | ---- | -------------------------------------------------------- |
| result | int  | result &gt; 0: 방 입장 소요시간(ms), result &lt; 0: 방 입장 오류 코드. |

### onUserVideoAvailable

원격 사용자가 재생 가능한 메인 스트림 비디오 보유 여부(일반적으로 카메라에 사용됨).

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미           |
| --------- | ------ | -------------- |
| userId    | String | 사용자 표식.     |
| available | boolean   | 화면 활성화 여부. |

## 호스트와 시청자 방 입장/퇴장 이벤트 콜백

### onAnchorEnter

새로운 호스트의 방 입장 알림을 수신합니다. 마이크가 연결된 시청자 및 크로스 룸 PK 호스트가 입장하면 시청자는 새로운 호스트의 방 입장 이벤트를 수신하며, 호스트는 `TRTCLiveRoom`의 `startPlay()`을 호출하여 해당 호스트의 비디오 화면을 재생합니다.


매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미            |
| ---------- | ------ | --------------- |
| userId     | String | 새로 방에 입장한 호스트 ID. |
| userName   | String | 사용자 닉네임.     |
| userAvatar | String | 사용자 프로필 사진 주소.    |

### onAnchorExit

호스트의 방 퇴장 알림을 수신합니다. 방 안에 있는 호스트(및 마이크 연결 중인 시청자)는 새로운 호스트의 방 퇴장 알림을 수신하며, `TRTCLiveRoom`의 `stopPlay()`를 호출하여 해당 호스트의 비디오 화면을 끕니다.

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미          |
| ---------- | ------ | -------------- |
| userId     | String | 방에서 퇴장한 호스트 ID.  |
| userName   | String | 사용자 닉네임.     |
| userAvatar | String | 사용자 프로필 사진 주소.           |


### onAudienceEnter

시청자 방 입장 공지 수신.

```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                             | 의미                                |
| -------- | -------------------------------- | ----------------------------------- |
| userInfo | TRTCLiveRoomDef.TRTCLiveUserInfo | 입장한 시청자 사용자 ID, 닉네임, 프로필 사진 등 정보. |


### onAudienceExit

시청자 방 퇴장 공지 수신


매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미          |
| ---------- | ------ | -------------- |
| userId     | String |  퇴장 시청자 정보. |
| userName   | String | 사용자 닉네임.     |
| userAvatar | String | 사용자 프로필 사진 주소.           |

### onRequestJoinAnchor

호스트가 시청자 마이크 연결 요청 수신 시 콜백입니다.


매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미              |
| ---------- | ------ | ----------------- |
| userId     | String | 마이크 연결 요청 사용자 ID. |
| userName   | String | 사용자 닉네임.     |
| userAvatar | String | 사용자 프로필 사진 주소.           |

### onAnchorAccepted

호스트가 시청자의 마이크 연결 요청을 수락합니다.


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | --------------- |
| userId   | String         | 호스트의 사용자 ID.  |


### onAnchorRejected

호스트가 시청자의 마이크 연결 요청을 거절합니다.


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId   | String         | 호스트의 사용자 ID.  |

### onKickoutJoinAnchor

마이크가 연결된 시청자가 마이크 연결 강제 해제 알림을 수신합니다. 마이크가 연결된 시청자가 호스트에 의해 마이크 연결이 강제 해제되었다는 메시지를 수신하며, 호스트는 `TRTCLiveRoom`의 `stopPublish()`를 호출하여 마이크 연결을 해제해야 합니다.


## 호스트 PK 이벤트 콜백

### onRequestRoomPK

크로스 룸 PK 요청을 수신합니다. 호스트가 다른 방 호스트의 PK 요청을 수신하고 PK를 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후, `startPlay()`를 호출하여 PK를 요청한 호스트의 스트림을 재생합니다.

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미             |
| ---------- | ------ | ----------------- |
| userId     | String | 크로스 룸 요청 사용자 ID. |
| userName   | String | 사용자 닉네임.     |
| userAvatar | String | 사용자 프로필 사진 주소.           |

### onRoomPKAccepted

호스트가 크로스 룸 PK 요청을 수락합니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                    |
| ------ | ------ | ----------------------- |
| userId | String | 크로스 룸 PK를 수신한 사용자 ID입니다. |

### onRoomPKRejected

호스트가 크로스 룸 PK 요청을 수락합니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                   |
| ------ | ------ | ----------------------- |
| userId | String | 크로스 룸 PK를 거절한 사용자 ID입니다. |


### onQuitRoomPK

크로스 룸 PK 종료 알림을 수신합니다.


## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지 수신.


매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| message  | String   | 텍스트 메시지.       |


### onRecvRoomCustomMsg

사용자 정의 메시지 수신


매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                                       |
| ------- | ------ | -------------------------------------------------- |
| command  | String            | 명령어. 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String         | 텍스트 메시지.                                         |

