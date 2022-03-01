1. TUIRoom은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM)을 기반으로 하며, 다음 기능을 지원합니다.
- 호스트가 방을 생성하고 방에 입장하는 사람이 방 번호를 입력한 후 참여.
- 방에 입장하는 사람들 간의 화면 공유.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 발송 지원.

2. TUIRoom은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [그룹 멀티미디어 룸(Android)](https://intl.cloud.tencent.com/document/product/647/37283)을 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 사용하는 저지연 멀티미디어 방 컴포넌트입니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 채팅방 기능을 구현합니다(**IM SDK는 Android 버전 사용**).


## TUIRoom API 개요

### TUIRoomCore 기본 함수

| API| 설명  |
| ----------------------------------- | -------------- |
| [getInstance](#getinstance)         | 싱글톤 객체 가져오기. |
| [destroyInstance](#destroyinstance) | 싱글톤 객체 폐기. |
| [setListener](#setlistener)         | 이벤트 콜백 설정. |

### 방 관련 API

| API| 설명 |
| ----------------------------------------- | ---------------------------------- |
| [createRoom](#createroom)                 | 방 생성(호스트 호출).           |
| [destroyRoom](#destroyroom)               | 방 폐기(호스트 호출).           |
| [enterRoom](#enterroom)                   | 방 입장(방 입장 참석자 호출).         |
| [leaveRoom](#leaveroom)                   | 방 퇴장(다른 방 구성원 호출). |
| [getRoomInfo](#getroominfo)               | 방 정보 가져오기.                     |
| [getRoomUsers](#getroomusers)             | 방에 있는 모든 참석자 정보 가져오기.           |
| [getUserInfo](#getuserinfo)               | 특정 사용자 정보 가져오기.               |
| [transferRoomMaster](#transferroommaster) | 호스트 권한 이전(호스트 호출).     |

### 로컬 멀티미디어 작업 인터페이스

| API| 설명  |
| ----------------------------------------- | -------------------------- |
| [startCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작.   |
| [stopCameraPreview](#stopcamerapreview)   | 로컬 비디오 수집 및 미리보기 중지.   |
| [startLocalAudio](#startlocalaudio)                   | 마이크 수집 활성화.            |
| [stopLocalAudio](#stoplocalaudio)                     | 마이크 수집 정지.           |
| [setVideoMirror](#setvideomirror)                     | 로컬 화면 이미지 미리보기 모드 설정. |
| [setSpeaker](#setspeaker)                       | 스피커 활성화 설정.     |

### 원격 사용자 관련 인터페이스

| API| 설명 |
| ----------------------------------- | ---------------------------------- |
| [startRemoteView](#startremoteview)   | 지정된 참석자의 원격 비디오 화면 구독 및 재생. |
| [stopRemoteView](#stopremoteview)     | 구독 취소 및 원격 비디오 화면 재생 중지.   |

### 채팅 메시지 발송 인터페이스

| API| 설명  |
| ----------------------------------- | -------------- |
| [sendChatMessage](#sendchatmessage)     | 채팅 메시지 발송.   |
| [sendCustomMessage](#sendcustommessage) | 사용자 정의 메시지 발송. |

### 필드 제어 관련 인터페이스

| API        | 설명       |
| --------------------------------------------------- | ------------------------------------------------------- |
| [muteUserMicrophone](#muteusermicrophone)           | 사용자의 마이크 비활성화/복구.                               |
| [muteAllUsersMicrophone](#muteallusersmicrophone)   | 모든 사용자의 마이크 비활성화/복원, 상태를 회의실 정보에 동기화. |
| [muteUserCamera](#muteusercamera)                   | 사용자 카메라 비활성화/복원.                               |
| [muteAllUsersCamera](#mutealluserscamera)           | 모든 사용자의 카메라 비활성화/복원, 상태를 방 정보에 동기화. |
| [muteChatRoom](#mutechatroom)                       | 채팅방 음소거 활성화/비활성화(호스트 호출).                     |
| [kickOffUser](#kickoffuser)                         | 방에서 특정인 강제 퇴장(호스트 호출).                        |
| [startCallingRoll](#startcallingroll)               | 호스트 통화 시작.                                        |
| [stopCallingRoll](#stopcallingroll)                 | 호스트 지명 종료.                                        |
| [replyCallingRoll](#replycallingroll)               | 참석자가 호스트의 지명에 응답.                                    |
| [sendSpeechInvitation](#sendspeechinvitation)       | 호스트의 참석자 발언 초대.                                    |
| [cancelSpeechInvitation](#cancelspeechinvitation)   | 호스트의 참석자 발언 초대 취소.                                |
| [replySpeechInvitation](#replyspeechinvitation)     | 참석자가 호스트의 발언 요청 동의/거절.                         |
| [sendSpeechApplication](#sendspeechapplication)     | 참석자 발언 신청.                                          |
| [replySpeechApplication](#replyspeechapplication)   | 호스트의 참석자 발언 신청 동의/거부.                         |
| [forbidSpeechApplication](#forbidspeechapplication) | 호스트의 발언 신청 금지.                                    |
| [sendOffSpeaker](#sendoffspeaker)                   | 호스트의 참석자 발언 금지.                                  |
| [sendOffAllSpeakers](#sendoffallspeakers)           | 호스트의 전원 발언 금지.                                  |
| [exitSpeechState](#exitspeechstate)                 | 참석자 발언 중지, 시청자로 전환.                               |

### 화면 공유 인터페이스

| API        | 설명       |
|-----|-----|
| [startScreenCapture](#startscreencapture) | 화면 공유 시작. |
| [stopScreenCapture](#stopscreencapture) | 화면 수집 중지. |

### 뷰티 필터 관련 API

| API        | 설명       |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager.](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager) 가져오기|


### 관련 설정 인터페이스

| API| 설명 |
| ----------------------------------------------- | ---------------------- |
| [setVideoQosPreference](#setvideoqospreference) | 네트워크 트래픽 제어 관련 매개변수 설정.|

### SDK 버전 인터페이스 함수 가져오기

| API  | 설명|
| ------------------------------- | --------------- |
| [getSDKVersion](#getsdkversion) | SDK 버전 가져오기.|

## TUIRoomCoreListener API 개요[](id:TUIRoomCoreListener)

### 오류 이벤트 콜백

| API  | 설명         |
| ------------------- | ---------- |
| [onError](#onerror) | 오류 콜백.|

### 기본 이벤트 콜백

| API  | 설명|
| ------------------------------------------- | ------------------ |
| [onDestroyRoom](#ondestroyroom)             | 방 해산 콜백.     |
| [onUserVoiceVolume](#onuservoicevolume)     | 볼륨 크기 콜백 콜백. |
| [onRoomMasterChanged](#onroommasterchanged) | 호스트 변경 콜백.   |

### 원격 사용자 이벤트 콜백

| API | 설명  |
| ------------------------------------------------------------ | -------------------------------- |
| [onRemoteUserEnter](#onremoteuserenter)                      | 원격 사용자 방 입장 콜백.           |
| [onRemoteUserLeave](#onremoteuserleave)                      | 원격 사용자 방 퇴장 콜백.           |
| [onRemoteUserCameraAvailable](#onremoteusercameraavailable)  | 원격 사용자 카메라 활성화 여부 콜백. |
| [onRemoteUserScreenVideoAvailable](#onremoteuserscreenvideoavailable) | 원격 사용자 화면 공유 활성화 여부 콜백.   |
| [onRemoteUserAudioAvailable](#onremoteuseraudioavailable)    | 원격 사용자의 오디오 업스트림 활성화 여부 콜백.   |
| [onRemoteUserEnterSpeechState](#onremoteuserenterspeechstate) | 원격 사용자 발언 시작 콜백.           |
| [onRemoteUserExitSpeechState](#onremoteuserexitspeechstate)  | 원격 사용자가 발언 종료 콜백.           |

### 메시지 이벤트 콜백

| API  | 설명|
| ------------------------------------------------- | ------------------ |
| [onReceiveChatMessage](#onreceivechatmessage)     | 텍스트 메시지 수신 콜백. |
| [onReceiveRoomCustomMsg](#onreceiveroomcustommsg) | 사용자 정의 메시지 수신 콜백. |

### 필드 제어 이벤트 콜백

| API        | 설명       |
| ------------------------------------------------------------ | ---------------------------------- |
| [onReceiveSpeechInvitation](#onreceivespeechinvitation)      | 사용자가 호스트의 발언 초대 수신 콜백.       |
| [onReceiveInvitationCancelled](#onreceiveinvitationcancelled) | 사용자가 호스트의 발언 초대 취소 수신 콜백.   |
| [onReceiveSpeechApplication](#onreceivespeechapplication)    | 호스트가 사용자의 발언 요청 수신 콜백.     |
| [onSpeechApplicationCancelled](#onspeechapplicationcancelled) | 사용자의 발언 신청 취소 콜백.             |
| [onSpeechApplicationForbidden](#onspeechapplicationforbidden) | 사회자 발언 신청 금지 콜백.           |
| [onOrderedToExitSpeechState](#onorderedtoexitspeechstate)  | 참석자가 발언 중단 요청 수신 콜백.         |
| [onCallingRollStarted](#oncallingrollstarted)                | 호스트 지명 시작 시 참석자가 수신하는 콜백.   |
| [onCallingRollStopped](#oncallingrollstopped)                | 호스트 지명 종료 시 참석자가 수신하는 콜백.   |
| [onMemberReplyCallingRoll](#onmemberreplycallingroll)        | 참석자의 지명 응답 시 호스트가 수신하는 콜백.   |
| [onChatRoomMuted](#onchatroommuted)                          | 호스트의 채팅방 음소거 상태 변경 콜백.     |
| [onMicrophoneMuted](#onmicrophonemuted)                      | 호스트의 마이크 비활성화 설정 콜백.         |
| [onCameraMuted](#oncameramuted)                              | 호스트의 카메라 비활성화 설정 콜백.         |
| [onReceiveKickedOff](#onreceivekickedoff)                    | 참석자가 수신하는 호스트의 내보내기 콜백.         |


### 네트워크 품질 및 기술 메트릭에 대한 통계를 위한 콜백 API

| API  | 설명|
| ------------------------------------- | ------------------ |
| [onStatistics](#onstatistics)         | 기술 지표 통계 콜백. |
| [onNetworkQuality](#onnetworkquality) | 네트워크 품질 콜백.     |

### 화면 공유 관련 콜백

| API  | 설명|
| ------------------------------------------------- | ------------------ |
| [onScreenCaptureStarted](#onscreencapturestarted) | 화면 공유 콜백 시작. |
| [onScreenCaptureStopped](#onscreencapturestopped) | 화면 공유 콜백 중지. |

## TUIRoomCore 기본 함수

### getInstance

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) 싱글톤 객체 가져오기.
```java
public static TUIRoomCore getInstance(Context context);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| context | Context | Android 컨텍스트로, 내부가 ApplicationContext로 전환되어 시스템 API 호출에 사용됩니다. |


### destroyInstance

```java
void destroyInstance();
```

### setListener

[TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) 이벤트 콜백. TUIRoomCoreListener을 통해 [TUIRoomCore](https://intl.cloud.tencent.com/document/product/647/37283) 에서 다양한 상태 알림을 받을 수 있습니다.

```java
void setListener(TUIRoomCoreListener listener);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| listener | TUIRoomCoreListener | 이벤트 콜백 클래스 수신. |

### createRoom

방을 생성합니다(호스트 호출).
```java
void createRoom(String roomId, TUIRoomCoreDef.SpeechMode speechMode, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형 | 의미  |
|-----------| ------------- | -------------------------------------- |
| roomId  | String  | 방 Id. 귀하가 직접 할당하고 통합 관리합니다. |
| speechMode| TUIRoomCoreDef.SpeechMode | 발언 모드. |
| callback | TUIRoomCoreCallback.ActionCallback | 방 생성 결과 콜백.|

호스트 정상 호출 프로세스는 다음과 같습니다.
1. **호스트**는 `createRoom()`을 호출하여 방을 생성하고, 방 생성 성공 여부는 `TUIRoomCoreCallback.ActionCallback`을 통해 호스트에게 알림됩니다.
2. **호스트**는 'startCameraPreview()'를 호출하여 카메라 캡처 및 미리보기를 시작합니다.
3. **호스트**는 'startLocalAudio()'를 호출하여 로컬 마이크를 켭니다.

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.
```java
void destroyRoom(TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형 | 의미  |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | 방 폐기 결과 콜백. |

### enterRoom

방에 입장합니다(방 가입 참석자 호출).
```java
void enterRoom(String roomId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| roomId | String | 방 Id. |
| callback | UIRoomCoreCallback.ActionCallback | 결과 콜백.  |


방 가입 참석자의 방 입장 정상 호출 프로세스는 다음과 같습니다.
1. **방 가입 참석자**는 'enterRoom'을 호출하고 roomId를 입력하여 방에 입장합니다.
2. **방 입장 참석자**는 `startCameraPreview()`를 호출하여 카메라 미리보기를 열고 `startLocalAudio()`를 호출하여 마이크 수집을 시작합니다.
3. **방 입장 참석자**는 `onRemoteUserCameraAvailable` 이벤트를 수신하고 `startRemoteView()`를 호출하여 비디오 재생을 시작합니다.

### leaveRoom

방에서 퇴장합니다(방 입장 참석자 호출).
```java
 void leaveRoom(TUIRoomCoreCallback.ActionCallback callback);
```

  매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| callback | UIRoomCoreCallback.ActionCallback | 결과 콜백.|

### getRoomInfo

방 정보 가져오기.
```java
TUIRoomCoreDef.RoomInfo getRoomInfo();
```

### getRoomUsers

방의 모든 구성원에 대한 정보를 가져옵니다.
```java
 List<TUIRoomCoreDef.UserInfo> getRoomUsers();
```

### getUserInfo

방 참석자 정보를 가져옵니다.
```java
void getUserInfo(String userId, TUIRoomCoreCallback.UserInfoCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| userId    | String | 사용자 Id.     |
| callback | UIRoomCoreCallback.UserInfoCallback | 방 참석자 세부 정보 콜백. |


### setSelfProfile

사용자 정보를 설정합니다.
```java
void setSelfProfile(String userName, String avatarURL, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미  |
| ---------- | ------ | -------------- |
| userName  | String | 사용자 이름.  |
| avatarURL | String | 사용자 프로필 URL. |
| callback | TUIRoomCoreCallback.ActionCallback | 성공적인 결과 콜백의 설정 여부. |


### transferRoomMaster

그룹을 다른 사용자에게 이전합니다.
```java
 void transferRoomMaster(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| userId    | String | 사용자 Id.     |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


## 로컬 푸시 스트림 인터페이스

### startCameraPreview

로컬 카메라 미리보기를 시작합니다.
```java
void startCameraPreview(boolean isFront, TXCloudVideoView view);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형  | 의미 |
| ---- | -------------- | ---------- |
| isFront | boolean | true: 전면 카메라, false: 후면 카메라. |
| view | TXCloudVideoView | 비디오 모니터를 탑재한 컨트롤러. |


### stopCameraPreview

로컬 카메라 미리보기를 중지합니다.
```java
 void stopCameraPreview();
```

### startLocalAudio

마이크 수집을 시작합니다.
```java
 void startLocalAudio(int quality);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형  | 의미 |
| ---- | -------------- | ---------- |
| quality | int | 수집된 사운드의 음질: <li/>TRTC_AUDIO_QUALITY_MUSIC<li/>TRTC_AUDIO_QUALITY_DEFAULT<li/>TRTC_AUDIO_QUALITY_SPEECH |

### stopLocalAudio

마이크 수집을 중지합니다.
```java
void stopLocalAudio();
```

### setVideoMirror

로컬 화면 미리보기 모드를 설정합니다.
```java
 void setVideoMirror(int type);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형  | 의미 |
| ---- | -------------- | ---------- |
| type | int | 이미지 유형. |

### setSpeaker

스피커를 활성화합니다.
```java
 void setSpeaker(boolean isUseSpeaker);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형  | 의미 |
| ---- | -------------- | ---------- |
| isUseSpeaker | boolean | true: 스피커, false: 핸드셋.|

## 원격 사용자 관련 인터페이스

### startRemoteView
원격 사용자의 비디오 스트림을 구독합니다.

```java
void startRemoteView(String userId, TXCloudVideoView view, TUIRoomCoreDef.SteamType streamType, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형 | 의미  |
| -------------- | ------------- | -------------------------- |
| userId | String | 재생할 사용자 ID.  |
| view | TXCloudVideoView  | 영상 화면 view 컨트롤러. |
| streamType  | TUIRoomCoreDef.SteamType | 스트림 유형.|
| callback  | TUIRoomCoreCallback.ActionCallback | 결과 콜백.|


### stopRemoteView

구독을 취소하고 원격 영상 화면 재생을 중지합니다.
```java
void stopRemoteView(String userId, TUIRoomCoreCallback.ActionCallback callback);

```

매개변수 리스트는 다음과 같습니다.

| 매개변수        | 유형    | 의미  |
| ------- | ------------- | ----------------------- |
| userId | String | 재생을 중지할 사용자 ID.|
| callback  | TUIRoomCoreCallback.ActionCallback | 결과 콜백.|

### switchCamera

전면/후면 카메라를 전환합니다.
```java
void switchCamera(boolean isFront);

```

매개변수 리스트는 다음과 같습니다.

| 매개변수        | 유형    | 의미  |
| ------- | ------------- | ----------------------- |
| isFront | boolean | true: 전면 카메라, false: 후면 카메라. |

## 메시지 인터페이스 보내기

### sendChatMessage

방 안에서 텍스트 메시지 발송, 일반적으로 텍스트 채팅에 사용됩니다.
```java
void sendChatMessage(String message, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| message | string | 메시지 내용. |
| callback  | TUIRoomCoreCallback.ActionCallback | 발송 결과 콜백.|


### sendCustomMessage

사용자 정의 메시지 발송.
```java
void sendCustomMessage(String data, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| data | String | 메시지 콘텐츠. |
| callback  | TUIRoomCoreCallback.ActionCallback | 발송 결과 콜백.|

## 필드 제어 관련 인터페이스

### muteUserMicrophone

사용자의 마이크를 비활성화/복구합니다.
```java
void muteUserMicrophone(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| mute  | boolean  | 비활성화 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### muteAllUsersMicrophone

모든 사용자의 마이크를 비활성화/복구합니다.
```java
void muteAllUsersMicrophone(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ---- | ---- | ---------- |
| mute | boolean | 비활성화 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


### muteUserCamera

사용자의 카메라를 비활성화/복구합니다.
```java
void muteUserCamera(String userId, boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| mute  | boolean  | 비활성화 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### muteAllUsersCamera

모든 사용자의 카메라를 비활성화/복구합니다.
```java
void muteAllUsersCamera(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ---- | ---- | ---------- |
| mute  | boolean  | 비활성화 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### muteChatRoom

텍스트 채팅을 비활성화/복구합니다.
```java
void muteChatRoom(boolean mute, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ---- | ---- | ---------- |
| mute  | boolean  | 비활성화 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


### kickOffUser

호스트의 내보내기.
```java
void kickOffUser(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### startCallingRoll

호스트가 지명을 시작합니다.
```java
 void startCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### stopCallingRoll

호스트가 지명을 종료합니다.
```java
 void stopCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
 
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### replyCallingRoll

참석자가 호스트의 지명에 응답합니다.
```java
void replyCallingRoll(TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


### sendSpeechInvitation

호스트가 참석자에게 발언 초대합니다.
```java
void sendSpeechInvitation(String userId, TUIRoomCoreCallback.InvitationCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| callback | TUIRoomCoreCallback.InvitationCallback | 결과 콜백. |

### cancelSpeechInvitation

호스트가 참석자의 발언 초대를 취소합니다.
```java
 void cancelSpeechInvitation(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### replySpeechInvitation

참석자는 호스트의 발언 초대에 동의/거절합니다.
```java
void replySpeechInvitation(boolean agree, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| agree | boolean  | 동의 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### sendSpeechApplication

참석자가 발언을 신청합니다.
```java
void sendSpeechApplication(TUIRoomCoreCallback.InvitationCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.InvitationCallback | 결과 콜백. |

### cancelSpeechApplication

참석자가 발언 신청을 취소합니다.
```java
void cancelSpeechApplication(TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### replySpeechApplication

호스트가 참석자의 발언 신청에 동의/거부합니다.
```java
void replySpeechApplication(boolean agree, String userId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| agree  | boolean| 동의 여부. |
| userId  | String| 사용자 ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### forbidSpeechApplication

호스트가 발언 신청을 금지합니다.
```java
 void forbidSpeechApplication(boolean forbid, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형 | 의미 |
| ------ | ---- | ---------- |
| forbid | boolean | 금지 여부. |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


### sendOffSpeaker

호스트가 참석자 발언을 금지합니다.
```java
void sendOffSpeaker(String userId, TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| userId  | String| 사용자 ID.  |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### sendOffAllSpeakers

호스트가 모든 참석자의 발언을 금지합니다.
```java
void sendOffAllSpeakers(TUIRoomCoreCallback.ActionCallback callback);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |

### exitSpeechState

참석자는 발언을 중지하고 시청자로 전환합니다.
```java
void exitSpeechState(TUIRoomCoreCallback.ActionCallback callback);
```
매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형  | 의미 |
| -------- | -------- | ---------- |
| callback | TUIRoomCoreCallback.ActionCallback | 결과 콜백. |


## 화면 공유 인터페이스
### startScreenCapture

화면 공유를 시작합니다.
```java
void startScreenCapture(TRTCCloudDef.TRTCVideoEncParam encParams, TRTCCloudDef.TRTCScreenShareParams screenShareParams);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| encParams | TRTCCloudDef.TRTCVideoEncParam | 화면 공유 설정 시 인코딩 매개변수입니다. 위의 권장 설정을 참고하십시오. encParams가 null인 경우, startScreenCapture 호출 전 인코딩 매개변수 설정이 적용됩니다. |
| screenShareParams | TRTCCloudDef.TRTCScreenShareParams | 화면 공유 특수 설정을 설정합니다. 시스템으로 인한 App 강제 종료를 방지하고 사용자 프라이버시 보호를 위해 floatingView 설정을 권장합니다. |

>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58)를 참고하십시오.

### stopScreenCapture

화면 수집을 중지합니다.
```java
void stopScreenCapture();
```

## 뷰티 필터 관련 API
### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)를 가져옵니다.
```java
TXBeautyManager getBeautyManager();
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
- '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
- '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
- 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
- 메이크업 효과를 추가합니다.
- 손 동작을 인식합니다.

## 관련 설정 인터페이스

### setVideoQosPreference

네트워크 트래픽 제어와 관련된 매개변수를 설정합니다.
```java
 void setVideoQosPreference(TRTCCloudDef.TRTCNetworkQosParam preference);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미  |
| ---------- | --------------------- | -------------- |
| preference | TRTCCloudDef.TRTCNetworkQosParam | 네트워크 트래픽 제어 정책. |

### setAudioQuality

오디오 품질을 설정합니다.
```java
void setAudioQuality(int quality);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| quality | int  | 오디오의 품질입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참고하십시오. |

### setVideoResolution

해상도를 설정합니다.

```java
void setVideoResolution(int resolution);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| resolution | int | 비디오 해상도. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#aa3b72c532f3ffdf64c6aacab26be5f87)를 참고하십시오. |


### setVideoFps

프레임 레이트를 설정합니다.
```java
void setVideoFps(int fps);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| fps | int | 비디오에서 수집하는 프레임 레이트. |

>?**권장 설정값**: 15fps 또는 20fps를 권장합니다. 5fps는 랙이 심하게 발생하며, 10fps 이하는 약간의 랙이 발생하고, 20fps 이상은 너무 높습니다(영화 프레임 레이트 24fps).


### setVideoBitrate

비트 레이트를 설정합니다.
```java
void setVideoBitrate(int bitrate);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| bitrate | int | 비트 레이트, SDK는 타깃 비트 레이트에 따라 인코딩하며, 네트워크가 불안정한 상태에서만 자체적으로 비디오 비트 레이트를 줄입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html)를 참고하십시오. |

>? **권장 설정값**: TRTCVideoResolution의 각 단계별 권장 최적 비트 레이트를 참고하고, 이를 기반으로 적합하게 높일 수 있습니다. 예를 들어 TRTC_VIDEO_RESOLUTION_1280_720의 권장 비트 레이트는 1200kbps이지만, 1500kbps로 설정하여 더 선명한 화면을 볼 수도 있습니다.

### enableAudioEvaluation

볼륨 알림을 활성화합니다.
```java
void enableAudioEvaluation(boolean enable);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| enable | boolean |  true: 활성화, false: 비활성화. |

>? 활성화하면 음량 크기값에 대한 SDK의 평가를 onUserVolumeUpdate에서 가져옵니다.

### setAudioPlayVolume

재생 볼륨을 설정합니다.
```java
void setAudioPlayVolume(int volume);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 재생 음량으로, 0-100으로 설정할 수 있으며 기본 값은 100입니다. |

### setAudioCaptureVolume

마이크 수집 볼륨을 설정합니다.
```java
void setAudioCaptureVolume(int volume);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 수집 음량으로, 0-100으로 설정할 수 있으며 기본 값은 100입니다. |

### startFileDumping

녹음을 시작합니다.
```java
void startFileDumping(TRTCCloudDef.TRTCAudioRecordingParams trtcAudioRecordingParams);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| trtcAudioRecordingParams | TRTCCloudDef.TRTCAudioRecordingParams | 녹음 매개변수. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDef__android.html#classcom_1_1tencent_1_1trtc_1_1TRTCCloudDef_1_1TRTCAudioRecordingParams)를 참고하십시오. |

>? 해당 방법으로 호출하면 SDK에서 통화 중 모든 오디오(로컬 오디오, 원격 오디오, BGM 등 포함)를 하나의 파일로 녹음합니다. 방 입장 여부에 상관 없이 해당 인터페이스를 호출하면 모두 적용되며, leaveRoom 호출 시 녹음 중인 경우 녹음은 자동으로 중지됩니다.

### stopFileDumping

녹음을 중지합니다.
```java
void stopFileDumping();
```

## SDK 버전 인터페이스 가져오기

### getSdkVersion

SDK 버전 정보를 가져옵니다.
```java
int getSdkVersion();
```

## 오류 이벤트 콜백
### onError

```java
void onError(int code, String message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| code    | int    | 오류 코드.|
| message | String | 오류 정보. |

## 기본 이벤트 콜백

### onDestroyRoom

방 해산 콜백입니다.
```java
void onDestroyRoom();
```

### onUserVoiceVolume

사용자 볼륨 크기 콜백입니다.
```java
void onUserVoiceVolume(String userId, int volume);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------------------------------- |
| userId | String | 사용자 ID.  |
| volume | int | 사용자의 볼륨 크기, 범위: 0 - 100. |

### onRoomMasterChanged

호스트 변경 콜백입니다.
```java
void onRoomMasterChanged(String previousUserId, String currentUserId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| previousUserId | String | 변경 전의 호스트 사용자 ID. |
| currentUserId | String | 변경 후의 호스트 사용자 ID. |


## 원격 사용자 콜백 이벤트

### onRemoteUserEnter

원격 사용자 방 입장 콜백입니다.
```java
void onRemoteUserEnter(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onRemoteUserLeave

원격 사용자 방 퇴장 콜백입니다.
```java
void onRemoteUserLeave(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onRemoteUserCameraAvailable

원격 사용자 카메라 활성화 여부입니다.
```java
void onRemoteUserCameraAvailable(String userId, boolean available);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형| 의미  |
| --------- | ------ | ----------------------------------------- |
| userId| String | 사용자 ID.|
| available | boolean| true: 동영상 스트리밍 데이터 있음, false: 동영상 스트리밍 데이터 없음. |

### onRemoteUserScreenVideoAvailable

참석자의 비디오 공유 알림을 **활성화**/**비활성화**합니다.
```java
void onRemoteUserScreenVideoAvailable(String userId, boolean available);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형| 의미  |
| --------- | ------ | ----------------------------------------- |
| userId| String | 사용자 ID.|
| available | boolean| 화면 공유 스트림 데이터가 있는지 여부. |

### onRemoteUserAudioAvailable

원격 사용자 오디오 업스트림 활성화 여부 콜백입니다.
```java
void onRemoteUserAudioAvailable(String userId, boolean available);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형| 의미  |
| --------- | ------ | ----------------------------------------- |
| userId| String | 사용자 ID.|
| available | boolean | 오디오 데이터가 있는지 여부. |

### onRemoteUserEnterSpeechState

원격 사용자가 발언을 시작합니다.
```java
void onRemoteUserEnterSpeechState(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onRemoteUserExitSpeechState

원격 사용자가 발언을 종료합니다.
```java
void onRemoteUserExitSpeechState(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|


## 채팅방 메시지 이벤트 콜백

### onReceiveChatMessage

텍스트 메시지를 수신합니다.
```java
void onReceiveChatMessage(String userId, String message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미 |
| ------- | ------ | ---------- |
| userId | String | 사용자 ID.  |
| message  | String   | 텍스트 메시지.|

### onReceiveRoomCustomMsg

사용자 정의 메시지를 수신합니다.
```java
void onReceiveRoomCustomMsg(String userId, String data);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | ------------ |
| userId    | String | 사용자 ID.|
| message | String | 사용자 정의 메시지.|

## 필드 제어 메시지 콜백

### onReceiveSpeechInvitation

사용자가 호스트로부터 발언 초대를 받았을 때의 콜백입니다.
```java
void onReceiveSpeechInvitation(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | ------------ |
| userId | String | 호스트 사용자 ID. |

### onReceiveInvitationCancelled

사용자가 호스트로부터 발언 초대 취소를 받았을 때의 콜백입니다.
```java
void onReceiveInvitationCancelled(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | ------------ |
| userId | String | 호스트 사용자 ID. |


### onReceiveSpeechApplication

호스트가 사용자의 발언 요청를 받았을 때의 콜백입니다.
```java
void onReceiveSpeechApplication(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onSpeechApplicationCancelled

사용자가 발언 신청을 취소하는 콜백입니다.
```java
void onSpeechApplicationCancelled(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onSpeechApplicationForbidden

호스트가 발언 신청을 금지하는 콜백입니다.
```java
void onSpeechApplicationForbidden(boolean isForbidden);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형 | 의미 |
| --------- | ---- | ---------- |
| isForbidden | boolean | 금지 여부. |

### onOrderedToExitSpeechState

참석자가 발언 중지를 요청받은 콜백입니다.
```java
void onOrderedToExitSpeechState(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | ------------ |
| userId | String | 호스트 사용자 ID. |


### onCallingRollStarted

호스트가 지명을 시작하면 참석자가 수신하는 콜백입니다.
```java
void onCallingRollStarted(String userId);
```

### onCallingRollStopped

호스트가 지명을 종료하면 참석자가 수신하는 콜백입니다.
```java
void onCallingRollStopped(String userId);
```

### onMemberReplyCallingRoll

참석자가 지명에 응답하면 호스트가 수신하는 콜백입니다.
```java
void onMemberReplyCallingRoll(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형| 의미|
| ------- | ------ | --------- |
| userId    | String | 사용자 ID.|

### onChatRoomMuted

호스트의 채팅방 음소거 여부 변경에 대한 콜백입니다.
```java
void onChatRoomMuted(boolean muted);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형   | 의미           |
| ----- | ---- | ---------- |
| muted | boolean | 음소거 여부. |

### onMicrophoneMuted

호스트의 마이크 음소거 설정에 대한 콜백입니다.
```java
void onMicrophoneMuted(boolean muted);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형   | 의미           |
| ----- | ---- | ---------- |
| muted | boolean | 음소거 여부. |

### onCameraMuted

호스트의 카메라 음소거 설정에 대한 콜백입니다.
```java
void onCameraMuted(boolean muted);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형   | 의미           |
| ----- | ---- | ---------- |
| muted | boolean | 음소거 여부. |

### onReceiveKickedOff

호스트의 내보내기 콜백.
```java
void onReceiveKickedOff(String userId);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형   | 의미           |
| ----- | ---- | ---------- |
| userId | String | 호스트/관리자 사용자 ID. |

## 통계 및 품질 콜백

### onStatistics

기술 지표 통계 콜백입니다.
```java
void onStatistics(TRTCStatistics statistics);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수| 유형 | 의미 |
| ------ | ---------------------- | ---------- |
| statis | TRTCStatistics | 통계 데이터. |

### onNetworkQuality

네트워크 상태 콜백입니다.
```java
void onNetworkQuality(TRTCCloudDef.TRTCQuality localQuality, List<TRTCCloudDef.TRTCQuality> remoteQuality);

```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
|-----|-----|-----|
| localQuality | TRTCCloudDef.TRTCQuality | 업스트림 네트워크 품질. |
| remoteQuality | List&amp;lt;TRTCCloudDef.TRTCQuality&amp;gt; | 다운스트림 네트워크 품질. |

>? 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#aba07d4191391dadef900422521f34e5b)를 참고하십시오.


## 화면 공유 이벤트 콜백

### onScreenCaptureStarted

화면 공유 시작 콜백입니다.

```java
 void onScreenCaptureStarted();
```

### onScreenCaptureStopped

화면 공유 중지 콜백입니다.

```java
void onScreenCaptureStopped(int reason);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
| ------ | ---- | ------------------------------------------------------ |
| reason | int  | 중지 사유입니다. 0: 사용자가 중지, 1: 다른 애플리케이션으로 인한 강제 중지. |
