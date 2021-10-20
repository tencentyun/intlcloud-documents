TRTCLiveRoom은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM)을 기반으로 하며, 다음 기능을 지원합니다.
- 호스트가 신규 라이브 룸을 생성하면 시청자가 라이브 룸에 입장해 시청.
- 호스트와 시청자가 비디오의 마이크를 연결하여 소통 진행.
- 서로 다른 두 라이브 룸 사이의 호스트 PK 인터랙션.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 지원. 사용자 정의 메시지를 통한 댓글 자막, 좋아요, 선물 기능 구현.

TRTCLiveRoom는 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [비디오 마이크 연결 라이브 방송(Android)](https://intl.cloud.tencent.com/document/product/647/36061)을 참고하십시오.
- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615)를 저지연 라이브 방송 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)의 AVChatroom을 이용해 라이브 방송 채팅방 기능을 구현하고, IM 메시지를 통해 호스트 간의 마이크 연결 프로세스를 연결합니다.

[](id:TRTCLiveRoom)
## TRTCLiveRoom API 개요

### SDK 기본 함수

| API                 | 설명       |
|-----|-----|
| [sharedInstance](#sharedinstance)               | 컴포넌트 싱글톤 가져오기.           |
| [destroySharedInstance](#destroysharedinstance) | 컴포넌트 싱글톤 폐기.           |
| [setDelegate](#setdelegate) | 이벤트 콜백 설정.|
| [setDelegateHandler](#setdelegatehandler) | 이벤트 콜백이 속한 스레드 설정. |
| [login](#login) | 로그인.|
| [logout](#logout) | 로그아웃. |
| [setSelfProfile](#setselfprofile) | 개인 프로필 정보 수정.|

### 방 관련 API

| API                 | 설명       |
|-----|-----|
| [createRoom](#createroom) | 방(호스트 호출) 생성. 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방 생성. |
| [destroyRoom](#destroyroom) | 방 폐기(호스트 호출). |
| [enterRoom](#enterroom) | 방 입장(시청자 호출). |
| [exitRoom](#exitroom) | 방 퇴장(시청자 호출). |
| [getRoomInfos](#getroominfos) | 방 리스트의 상세 정보 획득. |
| [getAnchorList](#getanchorlist) | 방 안의 모든 호스트 리스트 획득, enterRoom() 성공 후 호출해야만 유효. |
| [getAudienceList](#getaudiencelist) | 방 안의 모든 시청자 정보 획득, enterRoom() 성공 후 호출해야만 유효. |

### 푸시/풀 스트림 관련 API

| API                 | 설명       |
|-----|-----|
| [startCameraPreview](#startcamerapreview) | 로컬 비디오 화면 미리보기 시작. |
| [stopCameraPreview](#stopcamerapreview) | 로컬 비디오 수집 및 미리보기 종료. |
| [startPublish](#startpublish) | 라이브 방송 시작(푸시 스트림). |
| [stopPublish](#stoppublish) | 라이브 방송 중단(푸시 스트림). |
| [startPlay](#startplay) | 원격 비디오 화면 재생. 일반 시청 및 마이크 연결 시나리오에서 호출 가능. |
| [stopPlay](#stopplay) | 원격 비디오 화면 렌더링 중단. |

### 호스트와 시청자 마이크 연결

| API                 | 설명       |
|-----|-----|
| [requestJoinAnchor](#requestjoinanchor) | 시청자 마이크 연결 요청. |
| [responseJoinAnchor](#responsejoinanchor) | 호스트가 마이크 연결 요청 처리. |
| [kickoutJoinAnchor](#kickoutjoinanchor) | 호스트가 시청자 마이크 연결 강제 해제. |

### 호스트 크로스 룸 PK

| API                 | 설명       |
|-----|-----|
| [requestRoomPK](#requestroompk) | 호스트가 크로스 룸 PK 요청.|
| [responseRoomPK](#responseroompk) | 호스트가 크로스 룸 PK 요청에 응답. |
| [quitRoomPK](#quitroompk) | 크로스 룸 PK 퇴장.|

### 멀티미디어 제어 관련 API

| API                 | 설명       |
|-----|-----|
| [switchCamera](#switchcamera) | 전면/후면 카메라 전환. |
| [setMirror](#setmirror) | 미러 이미지 표시 여부 설정. |
| [muteLocalAudio](#mutelocalaudio) | 로컬 오디오 음소거. |
| [muteRemoteAudio](#muteremoteaudio) | 원격 오디오 음소거. |
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 원격 오디오 음소거.|

### 배경 음악 음향 효과 관련 API

| API                 | 설명       |
|-----|-----|
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager) 가져오기.|

### 뷰티 필터 관련 API

| API                 | 설명       |
|-----|-----|
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager) 가져오기.|

### 메시지 발송 관련 API

| API                 | 설명       |
|-----|-----|
| [sendRoomTextMsg](#sendroomtextmsg) | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용. |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송. |

### 디버깅 관련 API

| API                 | 설명       |
|-----|-----|
| [showVideoDebugLog](#showvideodebuglog) | 인터페이스에 debug 정보 표시 여부. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API 개요</h2>

### 일반적인 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onError](#onerror) | 오류 콜백.|
| [onWarning](#onwarning) | 경고 콜백. |
| [onDebugLog](#ondebuglog) | Log 콜백. |

### 방 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onRoomDestroy](#onroomdestroy) | 방 폐기 콜백. |
| [onRoomInfoChange](#onroominfochange) | 라이브 방송 방 정보 변경 콜백. |

### 호스트와 시청자 방 입장/퇴장 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onAnchorEnter](#onanchorenter) | 새로운 호스트 방 입장 알림 수신. |
| [onAnchorExit](#onanchorexit) | 호스트 퇴장 알림 수신. |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 알림 수신. |
| [onAudienceExit](#onaudienceexit) | 시청자 퇴장 알림 수신. |

### 호스트와 시청자 마이크 연결 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onRequestJoinAnchor](#onrequestjoinanchor) | 호스트가 시청자의 마이크 연결 요청을 수신할 때의 콜백. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | 마이크가 연결된 시청자가 마이크 연결 강제 해제 알림 수신. |

### 호스트 PK 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onRequestRoomPK](#onrequestroompk) | 크로스 룸 PK 요청 알림 수신.|
| [onQuitRoomPK](#onquitroompk) | 크로스 룸 PK 종료 알림 수신. |

### 메시지 이벤트 콜백

| API                 | 설명       |
|-----|-----|
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | 텍스트 메시지 수신. |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신. |

## SDK 기본 함수

[](id:sharedInstance)
### sharedInstance

[TRTCLiveRoom](https://cloud.tencent.com/document/product/647/43182) 컴포넌트 싱글톤 가져오기.
```java
 public static synchronized TRTCLiveRoom sharedInstance(Context context);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| context | Context | Android 컨텍스트로, 내부가 ApplicationContext로 전환되어 시스템 API 호출에 사용됩니다. |

   

### destroySharedInstance

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061) 컴포넌트 싱글톤 폐기.
>?인스턴스 폐기 후에는 외부에 캐시된 TRTCLiveRoom 인스턴스를 다시 사용할 수 없으며, 다시 [sharedInstance](#sharedInstance)를 호출해 새로운 인스턴스를 획득해야 합니다.

```java
public static void destroySharedInstance();
```

### setDelegate

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061)이벤트 콜백은 TRTCLiveRoomDelegate를 통해 [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36061)의 다양한 상태 알림을 받아볼 수 있습니다.
```java
public abstract void setDelegate(TRTCLiveRoomDelegate delegate);
```

>?setDelegate는 TRTCLiveRoom의 콜백 프록시입니다.   

### setDelegateHandler

이벤트 콜백이 속한 스레드를 설정합니다.
```java
public abstract void setDelegateHandler(Handler handler);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| handler | Handler | TRTCLiveRoom 상의 다양한 상태 알림 콜백은 해당 handler를 통해 통지합니다. setDelegate와 함께 사용하지 마십시오. |

   

### login

로그인.

<dx-codeblock>
::: java java
public abstract void login(int sdkAppId,
 String userId, String userSig,
 TRTCLiveRoomDef.TRTCLiveRoomConfig config, 
 TRTCLiveRoomCallback.ActionCallback callback);
:::
</dx-codeblock>

매개변수 리스트

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| sdkAppId | int | TRTC 콘솔>[애플리케이션 관리(https://console.cloud.tencent.com/trtc/app)>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | String | 현재 사용자 ID.입니다. 영어 알파벳(a-z, A-Z), 숫자(0~9), 하이픈(-), 언더바(\_)의 문자열로 구성합니다. |
| userSig  | String                                    | Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |
| config | TRTCLiveRoomConfig | 전체 설정 정보입니다. 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다.<ul style="margin:0;"><li>useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자가 CDN을 통해 시청하도록 설정하며, 요금이 저렴하지만 딜레이가 비교적 많이 발생합니다. false는 일반 시청자가 저지연를 통해 시청하도록 설정하며, 요금이 CDN과 마이크 연결 요금의 중간 정도지만 딜레이가 1초 이내로 제어됩니다.</li><li>CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용됩니다. CDN을 시청하는 재생 도메인으로 지정하는 데 사용되며, 라이브 방송 콘솔>[<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a>] 페이지에서 설정할 수 있습니다.</li></ul> |
| callback | ActionCallback | 로그인 콜백이며, 성공 시 code는 0입니다. |

   

### logout

로그아웃.
```java
public abstract void logout(TRTCLiveRoomCallback.ActionCallback callback);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | ActionCallback | 로그아웃 콜백이며, 성공 시 code는 0입니다. |

   

### setSelfProfile

개인 정보 수정.
```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미       |
|-----|-----|-----|
| userName  | String         | 닉네임.                              |
| avatarURL | String         | 프로필 사진 주소.                          |
| callback  | ActionCallback | 개인 정보 설정 콜백이며, 성공 시 code는 0입니다. |

   


## 방 관련 API
### createRoom

방 생성(호스트 호출).
```java
public abstract void createRoom(int roomId, TRTCLiveRoomDef.TRTCCreateRoomParam roomParam, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| roomId | int | 방 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomID를 1개의 라이브 룸 리스트로 통합할 수 있으며, Tencent Cloud는 현재 라이브 룸 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | TRTCCreateRoomParam | 방 정보입니다. 방 이름, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. 방 리스트 및 방 정보가 귀하의 서버에서 직접 관리되고 있다면 해당 매개변수는 생략할 수 있습니다. |
| callback | ActionCallback | 방 생성 결과 콜백이며, 성공 시 code는 0입니다. |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 
1. [호스트] `startCameraPreview()`를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다. 
2. [호스트] `createRoom()`을 호출하여 라이브 룸을 생성하면, 생성 여부가 ActionCallback을 통해 호스트에게 통지됩니다.
3. [호스트] `starPublish()`를 호출하여 푸시 스트림을 시작합니다.

   

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.
```java
public abstract void destroyRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | ActionCallback | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |


### enterRoom

방 입장(시청자 호출).
```java
public abstract void enterRoom(int roomId, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미       |
|-----|-----|-----|
| roomId   | int            | 방 식별 번호.                            |
| callback | ActionCallback | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |


시청자의 정상적인 라이브 방송 시청 호출 프로세스는 다음과 같습니다. 
1. [시청자]가 귀하의 서버에서 최신 라이브 룸 리스트를 획득하며, 여기에는 여러 라이브 룸의 roomID 및 방 정보가 포함될 수 있습니다.
2. [시청자]가 라이브 룸 1개를 선택하고 `enterRoom()`을 호출하여 해당 방으로 입장합니다.
3. [시청자]가 `startPlay(userId)`를 호출하고 호스트의 userId를 전달하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자 측에서 직접 `startPlay(userId)`를 호출하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userId 정보가 포함되어 있어 다시 `startPlay(userId)`를 호출하면 재생됩니다. 

   

### exitRoom

방 퇴장.
```java
public abstract void exitRoom(TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | ActionCallback | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |

   

### getRoomInfos

방 리스트의 상세 정보를 획득합니다. 방 정보는 호스트가 `createRoom()` 시 roomInfo를 통해 설정할 수 있습니다.
>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```java
public abstract void getRoomInfos(List<Integer> roomIdList, TRTCLiveRoomCallback.RoomInfoCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| roomIdList | List&lt;Integer&gt; | 방 번호 리스트.       |
| callback | RoomInfoCallback | 방 상세 정보 콜백. |


### getAnchorList

방 안의 모든 호스트 리스트를 획득합니다. enterRoom() 성공 후 호출해야만 유효합니다.
```java
public abstract void getAnchorList(TRTCLiveRoomCallback.UserListCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | UserListCallback | 사용자 상세 정보 콜백. |

   

### getAudienceList

방 안의 모든 시청자 정보를 획득합니다. `enterRoom()` 성공 후 호출해야만 유효합니다.
```java
public abstract void getAudienceList(TRTCLiveRoomCallback.UserListCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | UserListCallback | 사용자 상세 정보 콜백. |

   

## 푸시/풀 스트림 관련 API
### startCameraPreview

로컬 비디오 화면 미리보기를 시작합니다.
```java
public abstract void startCameraPreview(boolean isFront, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| isFront | boolean | true: 전면 카메라, false: 후면 카메라. |
| view | TXCloudVideoView | 비디오 모니터를 탑재한 컨트롤러. |
| callback | ActionCallback | 작업 콜백. |

   

### stopCameraPreview

로컬 비디오 수집 및 미리보기를 종료합니다.
```java
public abstract void stopCameraPreview();
```

   

### startPublish

라이브 방송(푸시 스트림)을 시작합니다. 다음과 같은 시나리오에 적용할 수 있습니다.
- 호스트가 방송을 시작할 때 호출
- 시청자가 마이크 연결을 시작할 때 호출


```java
public abstract void startPublish(String streamId, TRTCLiveRoomCallback.ActionCallback callback);
```
매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| streamId | String | 라이브 방송 CDN의 streamId를 바인딩하는 데 사용. 시청자가 라이브 방송 CDN을 통해 시청하도록 설정하고 싶은 경우 현재 호스트의 라이브 방송 streamId를 지정해야 합니다. |
| callback | ActionCallback | 작업 콜백. |


### stopPublish

라이브 방송(푸시 스트림)을 중단합니다. 다음과 같은 시나리오에 적용할 수 있습니다.
- 호스트가 라이브 방송을 종료할 때 호출
- 시청자가 마이크 연결을 종료할 때 호출


```java
public abstract void stopPublish(TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | ActionCallback | 작업 콜백. |



   

### startPlay

원격 비디오 화면을 재생합니다. 일반 시청 및 마이크 연결 시나리오에서 호출할 수 있습니다.
```java
public abstract void startPlay(String userId, TXCloudVideoView view, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 시청하는 사용자 id. |
| view | TXCloudVideoView | 비디오 화면 view 컨트롤러. |
| callback | ActionCallback | 작업 콜백. |

**일반 시청 시나리오**
- 라이브 룸 리스트에 호스트의 userId 정보가 포함되어 있는 경우, 시청자 측에서 직접 `enterRoom()` 성공 후 `startPlay(userId)`를 호출하여 호스트의 화면을 재생할 수 있습니다.
- 방 입장 전 호스트 userId를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userId 정보가 포함되어 있어 다시 `startPlay(userId)`를 호출하면 호스트 화면이 재생됩니다.

**라이브 방송 마이크 연결 시나리오**
마이크 연결 요청 후 호스트가 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userId)` 콜백을 수신하면 콜백에 있는 userId를 사용하여 startPlay(userId)를 호출해 마이크 연결 화면을 재생할 수 있습니다.

   

### stopPlay

원격 비디오 화면의 렌더링을 중단합니다. `onAnchorExit()`가 콜백되면 해당 인터페이스를 호출합니다.
```java
public abstract void stopPlay(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 상대방 사용자 정보. |
| callback | ActionCallback | 작업 콜백. |


## 호스트와 시청자 마이크 연결
### requestJoinAnchor

시청자가 마이크 연결을 요청합니다.
```java
public abstract void requestJoinAnchor(String reason, int timeout, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| reason | String | 마이크 연결 이유 설명. |
| timeout | int | 타임 아웃 시간. |
| callback | ActionCallback | 호스트 응답 콜백.           |


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
public abstract void responseJoinAnchor(String userId, boolean agree, String reason);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 시청자 ID. |
| agree | boolean | true: 동의, false: 거절. |
| reason | String | 마이크 연결 동의/거절 이유 설명. |


### kickoutJoinAnchor

호스트가 시청자의 마이크 연결을 강제 해제합니다. 호스트가 해당 인터페이스를 호출하여 관중의 마이크 연결을 강제 해제하면, 강제 해제된 시청자는 `TRTCLiveRoomDelegate`의 `onKickoutJoinAnchor()` 콜백 알림을 수신합니다.

```java
public abstract void kickoutJoinAnchor(String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 마이크가 연결된 시청자 ID. |
| callback | ActionCallback | 작업 콜백. |



## 호스트 크로스 룸 PK
### requestRoomPK

호스트가 크로스 룸 PK를 요청합니다.
```java
public abstract void requestRoomPK(int roomId, String userId, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| roomId | int | 초대된 방 ID. |
| userId | String | 초대된 호스트 ID. |
| callback | ActionCallback | 크로스 룸 PK 요청 결과 콜백. |

호스트와 호스트 사이에 크로스 룸 PK를 진행할 수 있으며, 두 정식 라이브 방송의 호스트 A와 B 사이의 크로스 룸 PK 프로세스는 다음과 같습니다.
1. [호스트 A] `requestRoomPK()`을 호출하여 호스트 B에게 마이크 연결을 요청합니다.
2. [호스트 B] `TRTCLiveRoomDelegate`의 `onRequestRoomPK()` 콜백 알림을 수신합니다.
3. [호스트 B] `responseRoomPK()`를 호출하여 호스트 A의 PK 요청을 수락할지 여부를 결정합니다.
4. [호스트 B] 호스트 A의 요청을 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 A의 비디오 화면을 재생합니다.
5. [호스트 A] `responseCallback` 콜백 알림을 수신합니다. 해당 알림은 호스트 B가 처리한 결과를 포함하고 있습니다.
6. [호스트 A] 요청이 수락된 경우 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 B의 비디오 화면을 재생합니다.

   

### responseRoomPK

호스트가 크로스 룸 PK 요청에 응답합니다. 호스트가 응답하면 상대방 호스트가 `requestRoomPK`에서 전달한 `responseCallback` 콜백을 수신합니다.
```java
public abstract void responseRoomPK(String userId, boolean agree, String reason);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | PK를 요청한 호스트 ID. |
| agree | boolean | true: 동의, false: 거절. |
| reason | String | PK 동의/거절 이유 설명. |


### quitRoomPK

크로스 룸 PK를 종료합니다. PK 중, 한쪽 호스트가 크로스 룸 PK를 종료하면 다른 호스트는 `TRTCLiveRoomDelegate`의 `onQuitRoomPk()` 콜백 알람을 수신합니다.
```java
public abstract void quitRoomPK(TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| callback | ActionCallback | 작업 콜백. |


## 멀티미디어 제어 관련 API
### switchCamera

전면/후면 카메라를 전환합니다.
```java
public abstract void switchCamera();
```

   

### setMirror

미러 이미지 표시 여부를 설정합니다.
```java
public abstract void setMirror(boolean isMirror);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| isMirror | boolean | 미러 이미지 활성화/비활성화. |

   

### muteLocalAudio

로컬 오디오를 음소거합니다.
```java
public abstract void muteLocalAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| mute | boolean | true: 음소거 켜기, false: 음소거 끄기.|

   

### muteRemoteAudio

원격 오디오를 음소거합니다.
```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 원격 사용자 ID. |
| mute | boolean | true: 음소거 켜기, false: 음소거 끄기.|

   

### muteAllRemoteAudio

모든 원격 오디오를 음소거합니다.
```java
public abstract void muteAllRemoteAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| mute | boolean | true: 음소거 켜기, false: 음소거 끄기.|

   

## 배경 음악 음향 효과 관련 API
### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 가져오기.
```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## 뷰티 필터 관련 API
### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html#classcom_1_1tencent_1_1liteav_1_1beauty_1_1TXBeautyManager)를 가져옵니다.
```java
public abstract TXBeautyManager getBeautyManager();
```

뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
- '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
- '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
- 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
- 메이크업 효과를 추가합니다.
- 손 동작을 인식합니다.


## 메시지 발송 관련 API
### sendRoomTextMsg

방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용.
```java
public abstract void sendRoomTextMsg(String message, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미             |
|-----|-----|-----|
| message  | String         | 텍스트 메시지.     |
| callback | ActionCallback | 발송 결과 콜백. |

   

### sendRoomCustomMsg

사용자 정의 텍스트 메시지 발송.
```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCLiveRoomCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| cmd      | String         | 명령어. 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String         | 텍스트 메시지.     |
| callback | ActionCallback | 발송 결과 콜백. |

   

## 디버깅 관련 API
### showVideoDebugLog

인터페이스에 debug 정보 표시 여부를 설정합니다.
```java
public abstract void showVideoDebugLog(boolean isShow);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| isShow | boolean | Debug 정보 표시/표시하지 않음. |

   

## TRTCLiveRoomDelegate 이벤트 콜백

## 일반적인 이벤트 콜백
### onError

오류 콜백.
>?SDK가 복구할 수 없는 오류는 반드시 모니터링하고 상황에 따라 적절한 인터페이스를 사용자에게 제시해야 합니다.

```java
void onError(int code, String message);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| code    | int    | 오류 코드.   |
| message | String | 오류 정보. |


### onWarning

경고 콜백.
```java
void onWarning(int code, String message);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| code    | int    | 오류 코드.   |
| message | String | 경고 정보. |

   

### onDebugLog

Log 콜백.
```java
void onDebugLog(String message);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| message | String | 로그 정보. |

   


## 방 이벤트 콜백
### onRoomDestroy

방 폐기 콜백입니다. 호스트가 퇴장하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.
```java
void onRoomDestroy(String roomId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미      |
|-----|-----|-----|
| roomId | String | 방 ID. |



   

### onRoomInfoChange

라이브 방송 방 정보 변경 시 콜백입니다. 라이브 방송 마이크 연결, PK 방 나가기 등 상태 변화를 알려주는 시나리오에 많이 사용됩니다.
```java
void onRoomInfoChange(TRTCLiveRoomDef.TRTCLiveRoomInfo roomInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| roomInfo | TRTCLiveRoomInfo | 방 정보. |

   


## 호스트와 시청자 방 입장/퇴장 이벤트 콜백
### onAnchorEnter

새로운 호스트의 방 입장 알림을 수신합니다. 마이크가 연결된 시청자 및 크로스 룸 PK 호스트가 입장하면 시청자는 새로운 호스트의 방 입장 이벤트를 수신하며, 호스트는 `TRTCLiveRoom`의 `startPlay()`을 호출하여 해당 호스트의 비디오 화면을 재생합니다.
```java
void onAnchorEnter(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 새로 방에 입장한 호스트 ID. |


### onAnchorExit

호스트의 방 퇴장 알림을 수신합니다. 방 안에 있는 호스트(및 마이크 연결 중인 시청자)는 새로운 호스트의 방 퇴장 알림을 수신하며, `TRTCLiveRoom`의 `stopPlay()`를 호출하여 해당 호스트의 비디오 화면을 끕니다.
```java
void onAnchorExit(String userId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userId | String | 퇴장한 사용자 ID. |


### onAudienceEnter

시청자 방 입장 공지 수신.
```java
void onAudienceEnter(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 입장 시청자 정보. |

   

### onAudienceExit

시청자 방 퇴장 공지 수신.
```java
void onAudienceExit(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 퇴장 시청자 정보. |

   


## 호스트와 시청자 마이크 연결 이벤트 콜백
### onRequestJoinAnchor

호스트가 시청자 마이크 연결 요청 수신 시 콜백입니다.
```java
void onRequestJoinAnchor(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, String reason, int timeOut);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 마이크 연결을 요청한 시청자 정보. |
| reason | String | 마이크 연결 이유 설명. |
| timeout | int | 요청 처리 만료 시간. 상위 레이어에서 해당 시간이 초과하여 처리하지 않은 경우 자동으로 해당 요청 폐기. |

   

### onKickoutJoinAnchor

마이크가 연결된 시청자가 마이크 연결 강제 해제 알림을 수신합니다. 마이크가 연결된 시청자가 호스트에 의해 마이크 연결이 강제 해제되었다는 메시지를 수신하며, 호스트는 `TRTCLiveRoom`의 `stopPublish()`를 호출하여 마이크 연결을 해제해야 합니다.
```java
void onKickoutJoinAnchor();
```



## 호스트 PK 이벤트 콜백
### onRequestRoomPK

크로스 룸 PK 요청을 수신합니다. 호스트가 다른 방 호스트의 PK 요청을 수신하고 PK를 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후, `startPlay()`를 호출하여 PK를 요청한 호스트의 스트림을 재생합니다.
```java
void onRequestRoomPK(TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, int timeout);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| userInfo | TRTCLiveUserInfo | 크로스 룸 마이크 연결을 요청한 호스트 정보. |
| timeout | int | 요청 처리 만료 시간. |


### onQuitRoomPK

크로스 룸 PK 종료 알림을 수신합니다.
```java
void onQuitRoomPK();
```

   


## 메시지 이벤트 콜백
### onRecvRoomTextMsg

텍스트 메시지 수신.
```java
void onRecvRoomTextMsg(String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| message | String | 텍스트 메시지.|
| userInfo | TRTCLiveUserInfo | 발신자 정보.|

   

### onRecvRoomCustomMsg

사용자 정의 메시지 수신.
```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| command | String | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message | String | 텍스트 메시지.|
| userInfo | TRTCLiveUserInfo | 발신자 정보. |


[](id:TRTCAudioEffectManager)
## TRTCAudioEffectManager
### playBGM

배경 음악을 재생합니다.
```java
void playBGM(String url, int loopTimes, int bgmVol, int micVol, TRTCCloud.BGMNotify notify);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| url | String | 배경 음악 파일 경로. |
| loopTimes | int | 루프 횟수 |
| bgmVol | int | BGM 음량 |
| micVol | int | 수집 음량 |
| notify | TRTCCloud.BGMNotify | 재생 알림 |

   

### stopBGM

배경 음악 재생을 정지합니다.
```java
void stopBGM();
```

   

### pauseBGM

배경 음악을 일시 정지 합니다.
```java
void pauseBGM();
```

   

### resumeBGM

배경 음악을 계속해서 재생합니다.
```java
void resumeBGM();
```

   

### setBGMVolume

배경 음악의 음량 크기를 설정합니다. 배경 음악 재생 오디오 믹싱 시 사용하며, 배경 음악 음량 크기를 제어합니다.
```java
void setBGMVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 음량 크기이며, 100으로 표시되면 정상 음량입니다. 0 - 100으로 설정할 수 있으며, 기본값은 100입니다. |

   

### setBGMPosition

배경 음악 재생 진행 상황을 설정합니다.
```java
int setBGMPosition(int position);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| position | int | 배경 음악 재생 진행 상황으로, 단위는 밀리초(ms)입니다. |

__반환__

0: 성공.

   

### setMicVolume

마이크의 음량 크기를 설정합니다. 배경 음악 재생 오디오 믹싱 시 사용하며, 마이크 음량 크기를 제어합니다.
```java
void setMicVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| volume | Int | 음량 크기. 0 - 100으로 설정할 수 있으며, 기본값은 100입니다. |

   

### setReverbType

에코 효과를 설정합니다.
```java
void setReverbType(int reverbType);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| reverbType | int | 에코 유형이며, 자세한 내용은 `TRTCCloudDef`의 [TRTC_REVERB_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a60ecba31f49f70780e623d24bcfa1a7d) 정의를 참고하십시오. |

   

### setVoiceChangerType

음성 변조 유형을 설정합니다.
```java
void setVoiceChangerType(int type);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| type | int | 음성 변조 유형이며, 자세한 내용은 `TRTCCloudDef`의 [TRTC_VOICE_CHANGER_TYPE](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__android.html#a899e72b3e4a16288e6c2edfd779e3beb) 정의를 참고하십시오. |

   

### playAudioEffect

재생 음향효과입니다. 음향 효과별로 구체적인 ID를 지정해야 하며, 해당 ID를 통해 음향 효과를 시작, 정지, 음량 등을 설정할 수 있습니다. aac, mp3, m4a 포맷을 지원합니다.
```java
void playAudioEffect(int effectId, String path, int count, boolean publish, int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| effectId | int | 음향 효과 ID. |
| path | String | 음향 효과 경로. |
| count | int | 루프 횟수. |
| publish | boolean | 푸시 스트림 여부 / true: 시청자에게 푸시, false: 로컬 미리듣기. |
| volume | int | 음량 크기. 0 - 100으로 설정할 수 있으며, 기본값은 100입니다. |

   

### pauseAudioEffect

음향 효과 재생을 일시 정지합니다.
```java
void pauseAudioEffect(int effectId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| effectId | int | 음향 효과 ID. |

   

### resumeAudioEffect

음향 효과를 다시 재생합니다.
```java
void resumeAudioEffect(int effectId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| effectId | int | 음향 효과 ID. |

   

### stopAudioEffect

음향 효과 재생을 정지합니다.
```java
void stopAudioEffect(int effectId);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| effectId | int | 음향 효과 ID. |

   

### stopAllAudioEffects

모든 음향효과 재생을 정지합니다.
```java
void stopAllAudioEffects();
```

   

### setAudioEffectVolume

음향 효과 음량을 설정합니다.
```java
void setAudioEffectVolume(int effectId, int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| effectId | int | 음향 효과 ID. |
| volume | int | 음량 크기. 0 - 100으로 설정할 수 있으며, 기본값은 100입니다. |

   

### setAllAudioEffectsVolume

모든 음향 효과의 음량을 설정합니다.
```java
void setAllAudioEffectsVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
|-----|-----|-----|
| volume | int | 음량 크기. 0 - 100으로 설정할 수 있으며, 기본값은 100입니다. |

   
