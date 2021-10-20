TRTCLiveRoom은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM)을 기반으로 하며, 다음 기능을 지원합니다.

- 호스트가 신규 라이브 룸을 생성하면 시청자가 라이브 룸에 입장해 시청.
- 호스트와 시청자가 비디오의 마이크를 연결하여 소통 진행.
- 서로 다른 두 라이브 룸 사이의 호스트 PK 인터랙션.
- 다양한 텍스트 메시지 및 사용자 정의 메시지 지원. 사용자 정의 메시지를 통한 댓글 자막, 좋아요, 선물 기능 구현.

TRTCLiveRoom는 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [비디오 마이크 연결 라이브 방송(iOS）](https://intl.cloud.tencent.com/document/product/647/36060)을 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/34615)를 저지연 라이브 방송 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047/33996)의 AVChatroom을 이용해 라이브 방송 채팅방 기능을 구현하고, IM 메시지를 통해 호스트 간의 마이크 연결 프로세스를 연결합니다.



<h2 id="TRTCLiveRoom">TRTCLiveRoom API 개요</h2>

### SDK 기본 함수

| API                               | 설명           |
| --------------------------------- | -------------- |
| [delegate](#delegate)             | 이벤트 콜백 설정. |
| [login](#login)                   | 로그인.         |
| [logout](#logout)                 | 로그아웃.         |
| [setSelfProfile](#setselfprofile)               | 개인 정보 수정.           |

### 방 관련 API

| API                                 | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | 방 생성(호스트 호출). 방이 없는 경우 시스템에서 자동으로 새로운 방 생성. |
| [destroyRoom](#destroyroom)         | 방 폐기(호스트 호출).                                       |
| [enterRoom](#enterroom)             | 방 입장(시청자 호출).                                       |
| [exitRoom](#exitroom)               | 방 퇴장(시청자 호출).                                       |
| [getRoomInfos](#getroominfos)       | 방 리스트의 상세 정보 획득.                                     |
| [getAnchorList](#getanchorlist)     | 방 안의 모든 호스트 리스트 획득, enterRoom() 성공 후 호출해야만 유효.     |
| [getAudienceList](#getaudiencelist) | 방 안의 모든 시청자 정보 획득, enterRoom() 성공 후 호출해야만 유효.     |

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
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html#interfaceTXAudioEffectManager) 가져오기. |

### 뷰티 필터 관련 API

| API                                   | 설명                                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| [getBeautyManager](#getbeautymanager) | 뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager) 가져오기. |

### 메시지 발송 관련 API

| API                                     | 설명                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용. |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송.                     |

### 디버깅 관련 API

| API                                     | 설명                        |
| --------------------------------------- | --------------------------- |
| [showVideoDebugLog](#showvideodebuglog) | 인터페이스에 debug 정보 표시 여부. |

<h2 id="TRTCLiveRoomDelegate">TRTCLiveRoomDelegate API 개요</h2>

### 일반적인 이벤트 콜백

| API                       | 설명       |
| ------------------------- | ---------- |
| [onError](#onerror)       | 오류 콜백. |
| [onWarning](#onwarning)   | 경고 콜백. |
| [onDebugLog](#ondebuglog) | Log 콜백. |

### 방 이벤트 콜백

| API                                   | 설명                   |
| ------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)       | 방 폐기 콜백.     |
| [onRoomInfoChange](#onroominfochange) | 라이브 방송 방 정보 변경 콜백. |

### 호스트와 시청자 방 입장/퇴장 이벤트 콜백

| API                                 | 설명                 |
| ----------------------------------- | -------------------- |
| [onAnchorEnter](#onanchorenter)     | 새로운 호스트 방 입장 알림 수신. |
| [onAnchorExit](#onanchorexit)       | 호스트 퇴장 알림 수신.   |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 알림 수신.   |
| [onAudienceExit](#onaudienceexit)   | 시청자 퇴장 알림 수신.   |

### 호스트와 시청자 마이크 연결 이벤트 콜백

| API                                         | 설명                           |
| ------------------------------------------- | ------------------------------ |
| [onRequestJoinAnchor](#onrequestjoinanchor) | 호스트가 시청자의 마이크 연결 요청을 수신할 때의 콜백. |
| [onKickoutJoinAnchor](#onkickoutjoinanchor) | 마이크가 연결된 시청자가 마이크 연결 강제 해제 알림 수신. |

### 호스트 PK 이벤트 콜백

| API                                 | 설명                   |
| ----------------------------------- | ---------------------- |
| [onRequestRoomPK](#onrequestroompk) | 크로스 룸 PK 요청 알림 수신. |
| [onQuitRoomPK](#onquitroompk)       | 크로스 룸 PK 종료 알림 수신. |

### 메시지 이벤트 콜백

| API                                         | 설명             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | 텍스트 메시지 수신.   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신. |



## SDK 기본 함수

### delegate

[TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060) 이벤트 콜백은 TRTCLiveRoomDelegate를 통해 [TRTCLiveRoom](https://intl.cloud.tencent.com/document/product/647/36060)의 다양한 상태 알림을 받아볼 수 있습니다.

```objc
@property(nonatomic, weak)id<TRTCLiveRoomDelegate> delegate;
```

>?delegate는 TRTCLiveRoom의 콜백 프록시입니다.


### login

로그인.

```objc
/// 컴포넌트 시스템에 로그인
/// - Parameters:
///   - sdkAppID: TRTC 콘솔>[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다.
///   - userID: 현재 사용자 ID.입니다. 영어 알파벳(a-z, A-Z), 숫자(0~9), 하이픈(-), 언더바(\_)의 문자열로 구성합니다.
///   - userSig: Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오.
///   - config: 전체 설정 정보입니다. 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다. isAttachedTUIKit 항목은 TUIKit 가져오기 및 사용 여부입니다.
///   - callback: 로그인 콜백이며, 성공 시 code는 0입니다.
/// - Note:
///   - userSig의 권장 설정 기간은 7일입니다. usersign 기간 만료로 인한 IM 수신/발신 실패, TRTC 마이크 연결 실패 등을 효과적으로 방지할 수 있습니다.
- (void)loginWithSdkAppID:(int)sdkAppID
                  userID:(NSString *)userID
                 userSig:(NSString *)userSig
                  config:(TRTCLiveRoomConfig *)config
                callback:(Callback _Nullable)callback
NS_SWIFT_NAME(login(sdkAppID:userID:userSig:config:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| sdkAppID | Int                                       | TRTC 콘솔>[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userID   | String                                    | 현재 사용자 ID.입니다. 영어 알파벳(a-z, A-Z), 숫자(0~9), 하이픈(-), 언더바(\_)의 문자열로 구성합니다. |
| userSig  | String                                    | Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |
| config   | TRTCLiveRoomConfig                        | 전체 설정 정보입니다. 로그인 시 초기화하십시오. 로그인 후에는 변경할 수 없습니다.<ul style="margin:0;"><li>useCDNFirst 속성: 시청자의 시청 방식을 설정하는 데 사용합니다. true는 일반 시청자가 CDN을 통해 시청하도록 설정하며, 요금이 저렴하지만 딜레이가 비교적 많이 발생합니다. false는 일반 시청자가 저딜레이를 통해 시청하도록 설정하며, 요금이 CDN과 마이크 연결 요금의 중간 정도지만 딜레이가 1초 이내로 제어됩니다.</li><li>CDNPlayDomain 속성: useCDNFirst를 true로 설정해야만 적용됩니다. CDN을 시청하는 재생 도메인으로 지정하는 데 사용되며, 라이브 방송 콘솔>[<a href="https://console.cloud.tencent.com/live/domainmanage">도메인 관리</a>] 페이지에서 설정할 수 있습니다.</li></ul> |
| callback | (_ code: Int, _ message: String?) -> Void | 로그인 콜백이며, 성공 시 code는 0입니다.                                  |


### logout

로그아웃.

```objc
// 로그아웃
/// - Parameter callback: 로그아웃 콜백이며, 성공 시 code는 0입니다.
- (void)logout:(Callback _Nullable)callback
NS_SWIFT_NAME(logout(_:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                        |
| -------- | ----------------------------------------- | --------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | 로그아웃 콜백이며, 성공 시 code는 0입니다. |


### setSelfProfile

개인 정보 수정.

```objc
/// 사용자 정보 설정으로, 설정한 사용자 정보는 Tencent Cloud IM 클라우드 서비스에 저장됩니다.
/// - Parameters:
///   - name: 사용자 닉네임
///   - avatarURL: 사용자 프로필 사진 주소
///   - callback: 개인 정보 설정 콜백이며, 성공 시 code는 0입니다.
- (void)setSelfProfileWithName:(NSString *)name
                     avatarURL:(NSString * _Nullable)avatarURL
                      callback:(Callback _Nullable)callback
NS_SWIFT_NAME(setSelfProfile(name:avatarURL:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형                                      | 의미                                |
| --------- | ----------------------------------------- | ----------------------------------- |
| name      | String                                    | 닉네임.                              |
| avatarURL | String                                    | 프로필 사진 주소.                          |
| callback  | (_ code: Int, _ message: String?) -> Void | 개인 정보 설정 콜백이며, 성공 시 cod는 0입니다. |


## 방 관련 API

### createRoom

방 생성(호스트 호출).

```objc
/// 방(호스트 호출) 생성을 생성합니다. 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방을 생성합니다.
/// 호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다.
/// 1. [호스트] startCameraPreview()를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다.
/// 2. [호스트] createRoom()을 호출하여 라이브 룸을 생성하면, 생성 여부가 callback을 통해 호스트에게 통지됩니다.
/// 3. [호스트] startPublish()를 호출하여 푸시 스트림을 시작합니다.
/// - Parameters:
///   - roomID: 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomid를 1개의 라이브 룸 리스트로 통합할 수 있으며, Tencent Cloud는 현재 라이브 룸 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다.
///   - roomParam: TRTCCreateRoomParam | 방 정보입니다. 방 이름, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. 방 리스트 및 방 정보가 귀하의 서버에서 직접 관리되고 있다면 해당 매개변수는 생략할 수 있습니다.
///   - callback: 방 입장 결과 콜백이며, 성공 시 code는 0입니다.
/// - Note:
///   - 호스트가 라이브 방송을 시작할 때 호출하며, 이미 생성했던 방을 다시 중복으로 생성할 수 있습니다.
- (void)createRoomWithRoomID:(UInt32)roomID
                   roomParam:(TRTCCreateRoomParam *)roomParam
                    callback:(Callback _Nullable)callback
NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형                                      | 의미                                                         |
| --------- | ----------------------------------------- | ------------------------------------------------------------ |
| roomID    | UInt32                                    | 방 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomID를 1개의 라이브 룸 리스트로 통합할 수 있으며, Tencent Cloud는 현재 라이브 룸 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | TRTCCreateRoomParam                       | 방 정보입니다. 방 이름, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. 방 리스트 및 방 정보가 귀하의 서버에서 직접 관리되고 있다면 해당 매개변수는 생략할 수 있습니다. |
| callback  | (_ code: Int, _ message: String?) -> Void | 방 생성 결과 콜백이며, 성공 시 code는 0입니다.                        |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 

1. [호스트] `startCameraPreview()`를 호출하여 카메라 미리보기를 시작할 때 뷰티 필터 매개변수를 조정할 수 있습니다. 
2. [호스트] `createRoom()`을 호출하여 라이브 룸을 생성하면, 생성 여부가 callback을 통해 호스트에게 통지됩니다.
3. [호스트] `starPublish()`를 호출하여 푸시 스트림을 시작합니다.

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```objc
/// 방 폐기(호스트 호출)
/// 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.
/// - Parameter callback: 방 폐기 결과 콜백이며, 성공 시 code는 0입니다.
/// - Note:
///   - 호스트는 방 생성 후 해당 함수를 호출하여 방을 폐기할 수 있습니다.
- (void)destroyRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(destroyRoom(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |



### enterRoom

방 입장(시청자 호출).

```objc
/// 방 입장(시청자 호출)
/// 시청자의 정상적인 라이브 방송 시청 호출 프로세스는 다음과 같습니다.
/// 1. [시청자]가 귀하의 서버에서 최신 라이브 룸 리스트를 획득하며, 여기에는 여러 라이브 룸의 roomid 및 방 정보가 포함됩니다.
/// 2. [시청자]가 라이브 룸 1개를 선택하고 enterRoom()을 호출하여 해당 방으로 입장합니다.
/// 3. [시청자]는 서버에서 관리하는 방 리스트에 모든 방의 호스트 userID가 포함되어 있는 경우, 직접 enterRoom() 성공 후 startPlay(userID)를 호출하여 호스트 화면을 재생할 수 있습니다.
/// 귀하가 관리하는 방 리스트에 roomid만 있어도 괜찮습니다. 시청자는 enterRoom()에 성공한 후 TRTCLiveRoomDelegate의 onAnchorEnter(userID) 콜백을 빠르게 수신합니다.
/// 이때 콜백에 포함되어 있는 userID를 사용해 startPlay(userID)를 호출하여 호스트 화면을 재생합니다.
/// - Parameters:
///   - roomID: 방 식별 번호.
///   - useCDNFirst: CDN 재생 우선 사용 여부
///   - cdnDomain: CDN 도메인
///   - callback: 방 입장 결과 콜백이며, 성공 시 code는 0입니다.
/// - Note:
///   - 시청자가 라이브 방송 방에 입장할 때 호출합니다.
///   - 호스트는 해당 인터페이스를 호출하여 이미 생성한 방에 입장할 수 없으며, createRoom을 사용해야 합니다.
- (void)enterRoomWithRoomID:(UInt32)roomID
                useCDNFirst:(BOOL)useCDNFirst
                  cdnDomain:(NSString * _Nullable)cdnDomain
                   callback:(Callback)callback
NS_SWIFT_NAME(enterRoom(roomID:useCDNFirst:cdnDomain:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| roomID   | UInt32                                    | 방 식별 번호.                            |
| callback | (_ code: Int, _ message: String?) -> Void | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |



시청자의 정상적인 라이브 방송 시청 호출 프로세스는 다음과 같습니다. 

1. [시청자]가 귀하의 서버에서 최신 라이브 룸 리스트를 획득하며, 여기에는 여러 라이브 룸의 roomID 및 방 정보가 포함될 수 있습니다.
2. [시청자]가 라이브 룸 1개를 선택하고 `enterRoom()`을 호출하여 해당 방으로 입장합니다.
3. [시청자]가 `startPlay(userID)`를 호출하고 호스트의 userID를 전달하여 재생을 시작합니다.
 - 라이브 룸 리스트에 호스트의 userID 정보가 포함되어 있는 경우, 시청자 측에서 직접 `startPlay(userID)`를 호출하여 즉시 재생을 시작할 수 있습니다.
 - 방 입장 전 호스트 userID를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userID)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userID 정보가 포함되어 있어 다시 `startPlay(userID)`를 호출하면 재생됩니다. 



### exitRoom

방 퇴장.

```objc
/// 방 퇴장(시청자 호출)
/// - Parameter callback: 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다.
/// - Note:
///   - 시청자가 라이브 방송 방에서 퇴장할 때 호출합니다.
///   - 호스트는 해당 인터페이스를 호출하여 방을 퇴장할 수 없습니다.

- (void)exitRoom:(Callback _Nullable)callback
NS_SWIFT_NAME(exitRoom(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                  |
| -------- | ----------------------------------------- | ------------------------------------- |
| callback | (_ code: Int, _ message: String?) -> Void | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |

### getRoomInfos

방 리스트의 상세 정보를 획득합니다. 방 정보는 호스트가 `createRoom()` 시 roomInfo를 통해 설정할 수 있습니다.
>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.

```objc
/// 방 리스트의 상세 정보 획득
/// 이는 호스트가 createRoom() 시 roomInfo를 통해 설정한 정보입니다. 방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.
/// - Parameter roomIDs: 방 번호 리스트
/// - Parameter callback: 방 상세 정보 콜백
- (void)getRoomInfosWithRoomIDs:(NSArray<NSNumber *> *)roomIDs
                       callback:(RoomInfoCallback _Nullable)callback
NS_SWIFT_NAME(getRoomInfos(roomIDs:callback:));

```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                                         | 의미               |
| -------- | ------------------------------------------------------------ | ------------------ |
| roomIDs  | [UInt32]                                                       | 방 번호 리스트.       |
| callback | (_ code: Int, _ message: String?, _ roomList: [TRTCLiveRoomInfo]) -> Void | 방 상세 정보 콜백. |



### getAnchorList

방 안의 모든 호스트 리스트를 획득합니다. enterRoom() 성공 후 호출해야만 유효합니다.

```objc
/// 방 안의 모든 호스트 리스트를 획득합니다. enterRoom() 성공 후 호출해야만 유효합니다.
/// - Parameter callback: 사용자 상세 정보 콜백
- (void)getAnchorList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAnchorList(callback:));

```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                                         | 의미               |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | 사용자 상세 정보 콜백. |


### getAudienceList

방 안의 모든 시청자 정보를 획득합니다. `enterRoom()` 성공 후 호출해야만 유효합니다.

```objc
/// 방 안의 모든 시청자 정보를 획득합니다. enterRoom() 성공 후 호출해야만 유효합니다.
/// - Parameter callback: 사용자 상세 정보 콜백
- (void)getAudienceList:(UserListCallback _Nullable)callback
NS_SWIFT_NAME(getAudienceList(callback:));

```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                                         | 의미               |
| -------- | ------------------------------------------------------------ | ------------------ |
| callback | (_ code: Int, _ message: String, _ userList: [TRTCLiveUserInfo]) -> Void | 사용자 상세 정보 콜백. |


## 푸시/풀 스트림 관련 API

### startCameraPreview

로컬 비디오 화면 미리보기를 시작합니다.

```objc
/// 로컬 비디오 화면 미리보기 시작
/// - Parameters:
///   - frontCamera: true: 전면 카메라, false: 후면 카메라.
///   - view: 비디오 모니터를 탑재한 컨트롤러.
///   - callback: 작업 콜백.
- (void)startCameraPreviewWithFrontCamera:(BOOL)frontCamera
                                     view:(UIView *)view
                                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startCameraPreview(frontCamera:view:callback:));

```

매개변수는 다음과 같습니다.

| 매개변수        | 유형                                      | 의미                                  |
| ----------- | ----------------------------------------- | ------------------------------------- |
| frontCamera | Bool                                      | true: 전면 카메라, false: 후면 카메라. |
| view        | UIView                                    | 비디오 화면 컨트롤러.                  |
| callback    | (_ code: Int, _ message: String?) -> Void | 작업 콜백.                            |


### stopCameraPreview

로컬 비디오 수집 및 미리보기를 종료합니다.

```objc
/// 로컬 비디오 수집 및 미리보기 종료
- (void)stopCameraPreview;

```


### startPublish

라이브 방송(푸시 스트림)을 시작합니다. 다음과 같은 시나리오에 적용할 수 있습니다.

- 호스트가 방송을 시작할 때 호출
- 시청자가 마이크 연결을 시작할 때 호출


```objc
/// 라이브 방송(푸시 스트림)을 시작합니다. 다음 두 가지 시나리오에 적용할 수 있습니다.
/// 1. 호스트가 방송을 시작할 때 호출
/// 2. 시청자가 마이크 연결을 시작할 때 호출
/// - Parameters:
///   - streamID: 라이브 방송 CDN의 streamId를 바인딩하는 데 사용합니다. 시청자가 라이브 방송 CDN을 통해 시청하도록 설정하고 싶은 경우 현재 호스트의 라이브 방송 streamId를 지정해야 합니다.
///   - callback: 작업 콜백
- (void)startPublishWithStreamID:(NSString *)streamID
                        callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPublish(streamID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                                         |
| -------- | ----------------------------------------- | ------------------------------------------------------------ |
| streamID | String                                    | 라이브 방송 CDN의 streamID를 바인딩하는 데 사용. 시청자가 라이브 방송 CDN을 통해 시청하도록 설정하고 싶은 경우 현재 호스트의 라이브 방송 streamID를 지정해야 합니다. |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백.                                                   |


### stopPublish

라이브 방송(푸시 스트림)을 중단합니다. 다음과 같은 시나리오에 적용할 수 있습니다.

- 호스트가 라이브 방송을 종료할 때 호출.
- 시청자가 마이크 연결을 종료할 때 호출.

```objc
/// 라이브 방송(푸시 스트림)을 중단합니다. 다음 두 가지 시나리오에 적용할 수 있습니다.
/// 1. 호스트가 라이브 방송을 종료할 때 호출
/// 2. 시청자가 마이크 연결을 종료할 때 호출
/// - Parameter callback: 작업 콜백.
- (void)stopPublish:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPublish(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미       |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백. |



### startPlay

원격 비디오 화면을 재생합니다. 일반 시청 및 마이크 연결 시나리오에서 호출할 수 있습니다.

```objc
/// 원격 비디오 화면을 재생합니다. 일반 시청 및 마이크 연결 시나리오에서 호출할 수 있습니다.
/// [일반 시청 시나리오]
/// 1. 서버에서 관리하는 방 리스트에 모든 방의 호스트 userID가 포함되어 있는 경우, 직접 enterRoom() 성공 후 startPlay(userID)를 호출하여 호스트 화면을 재생할 수 있습니다.
/// 2. 귀하가 관리하는 방 리스트에 roomid만 있어도 괜찮습니다. 시청자는 enterRoom()에 성공한 후 TRTCLiveRoomDelegate의 onAnchorEnter(userID) 콜백을 빠르게 수신합니다.
/// 이때 콜백에 포함되어 있는 userID를 사용해 startPlay(userID)를 호출하여 호스트 화면을 재생합니다.
/// [라이브 방송 마이크 연결 시나리오]
/// 마이크 연결 요청 후 호스트가 TRTCLiveRoomDelegate의 onAnchorEnter(userID) 콜백을 수신하면 콜백에 있는 userID를 사용하여 startPlay(userID)를 호출해 마이크 연결 화면을 재생할 수 있습니다.
/// - Parameters:
///   - userID: 시청하는 사용자 ID.
///   - view: 비디오 화면 view 컨트롤러.
///   - callback: 작업 콜백.
- (void)startPlayWithUserID:(NSString *)userID
                       view:(UIView *)view
                   callback:(Callback _Nullable)callback
NS_SWIFT_NAME(startPlay(userID:view:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                       |
| -------- | ----------------------------------------- | -------------------------- |
| userID   | String                                    | 시청하는 사용자 ID.        |
| view     | UIView                                    | 비디오 화면 view 컨트롤러. |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백.                 |


**일반 시청 시나리오**

- 라이브 룸 리스트에 호스트의 userID 정보가 포함되어 있는 경우, 시청자 측에서 직접 `enterRoom()` 성공 후 `startPlay(userID)`를 호출하여 호스트의 화면을 재생할 수 있습니다.
- 방 입장 전 호스트 userID를 획득할 수 없는 경우, 시청자가 방 입장 후 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userID)` 이벤트 콜백을 수신하게 되고, 해당 콜백에 호스트의 userID 정보가 포함되어 있어 다시 `startPlay(userID)`를 호출하면 호스트 화면이 재생됩니다.

**라이브 방송 마이크 연결 시나리오**
마이크 연결 요청 후 호스트가 `TRTCLiveRoomDelegate`의 `onAnchorEnter(userID)` 콜백을 수신하면 콜백에 있는 userID를 사용하여 `startPlay(userID)`를 호출해 마이크 연결 화면을 재생할 수 있습니다.



### stopPlay

원격 비디오 화면의 렌더링을 중단합니다. `onAnchorExit()`가 콜백되면 해당 인터페이스를 호출합니다.

```objc
/// 원격 비디오 화면 렌더링 중단
/// - Parameters:
///   - userID: 상대방 사용자 정보.
///   - callback: 작업 콜백.
/// - Note:
///   - onAnchorExit 콜백 시 해당 인터페이스를 호출합니다.
- (void)stopPlayWithUserID:(NSString *)userID
                  callback:(Callback _Nullable)callback
NS_SWIFT_NAME(stopPlay(userID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미             |
| -------- | ----------------------------------------- | ---------------- |
| userID   | String                                    | 상대방 사용자 정보. |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백.       |




## 호스트와 시청자 마이크 연결

### requestJoinAnchor

시청자가 마이크 연결을 요청합니다.

```objc
/// 시청자가 마이크 연결 요청
/// - Parameters:
///   - reason: 마이크 연결 요청 이유.
///   - responseCallback: 마이크 연결 요청 콜백.
/// - Note: 시청자가 요청한 후 호스트 측에서 `onRequestJoinAnchor` 콜백을 수신합니다.
- (void)requestJoinAnchor:(NSString *)reason
                  timeout:(double)timeout
         responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestJoinAnchor(reason:timeout:responseCallback:));
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                                        | 의미           |
| ---------------- | ------------------------------------------- | -------------- |
| reason           | String                                     | 마이크 연결 이유 설명.     |
| timeout | long | 호스트 콜백에 응답. |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | 호스트 응답 콜백. |

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

```objc
/// 호스트가 시청자의 마이크 연결 요청에 응답
/// - Parameters:
///   - user: 시청자 ID.
///   - agree: true: 동의, false: 거절.
///   - reason: 마이크 연결 동의/거절 이유 설명.
/// - Note: 호스트가 응답하면 시청자 측에서 `requestJoinAnchor`가 전달된 `responseCallback` 콜백을 수신합니다.
- (void)responseJoinAnchor:(NSString *)userID
                     agree:(BOOL)agree
                    reason:(NSString *)reason
NS_SWIFT_NAME(responseJoinAnchor(userID:agree:reason:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                      |
| ------ | ------- | ------------------------- |
| userID | String  | 시청자 ID.                 |
| agree  | Bool    | true: 동의, false: 거절. |
| reason | String? | 마이크 연결 동의/거절 이유 설명. |


### kickoutJoinAnchor

호스트가 시청자의 마이크 연결을 강제 해제합니다. 호스트가 해당 인터페이스를 호출하여 관중의 마이크 연결을 강제 해제하면, 강제 해제된 시청자는 `TRTCLiveRoomDelegate`의 `onKickoutJoinAnchor()` 콜백 알림을 수신합니다.

```objc
/// 호스트가 시청자 마이크 연결 강제 해제
/// - Parameters:
///   - userID: 마이크 연결된 시청자 ID.
///   - callback: 작업 콜백.
/// - Note: 호스트가 해당 인터페이스를 호출하여 관중의 마이크 연결을 강제 해제하면, 강제 해제된 시청자는 trtcLiveRoomOnKickoutJoinAnchor() 콜백 알림을 수신합니다.
- (void)kickoutJoinAnchor:(NSString *)userID
                 callback:(Callback _Nullable)callback
NS_SWIFT_NAME(kickoutJoinAnchor(userID:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미          |
| -------- | ----------------------------------------- | ------------- |
| userID   | String                                    | 마이크가 연결된 시청자 ID. |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백.    |



## 호스트 크로스 룸 PK

### requestRoomPK

호스트가 크로스 룸 PK를 요청합니다.

```objc
/// 호스트가 크로스 룸 PK 요청
/// - Parameters:
///   - roomID: 초대된 방 ID.
///   - userID: 초대된 호스트 ID.
///   - responseCallback: 크로스 룸 PK 요청 결과 콜백.
/// - Note: 요청하면 상대방 호스트가 `onRequestRoomPK` 콜백 수신
- (void)requestRoomPKWithRoomID:(UInt32)roomID
                         userID:(NSString *)userID
               responseCallback:(ResponseCallback _Nullable)responseCallback
NS_SWIFT_NAME(requestRoomPK(roomID:userID:responseCallback:));
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형                                        | 의미                     |
| ---------------- | ------------------------------------------- | ------------------------ |
| roomID           | UInt32                                      | 초대된 방 ID.          |
| userID           | String                                      | 초대된 호스트 ID.          |
| responseCallback | (_ agreed: Bool, _ reason: String?) -> Void | 크로스 룸 PK 요청 결과 콜백. |

호스트와 호스트 사이에 크로스 룸 PK를 진행할 수 있으며, 두 정식 라이브 방송의 호스트 A와 B 사이의 크로스 룸 PK 프로세스는 다음과 같습니다.

1. [호스트 A] `requestRoomPK()`을 호출하여 호스트 B에게 마이크 연결을 요청합니다.
2. [호스트 B] `TRTCLiveRoomDelegate`의 `onRequestRoomPK()` 콜백 알림을 수신합니다.
3. [호스트 B] `responseRoomPK()`를 호출하여 호스트 A의 PK 요청을 수락할지 여부를 결정합니다.
4. [호스트 B] 호스트 A의 요청을 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 A의 비디오 화면을 재생합니다.
5. [호스트 A] `responseCallback` 콜백 알림을 수신합니다. 해당 알림은 호스트 B가 처리한 결과를 포함하고 있습니다.
6. [호스트 A] 요청이 수락된 경우 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후 `startPlay()`를 호출하여 호스트 B의 비디오 화면을 재생합니다.


### responseRoomPK

호스트가 크로스 룸 PK 요청에 응답합니다. 호스트가 응답하면 상대방 호스트가 `requestRoomPK`에서 전달한 `responseCallback` 콜백을 수신합니다.

```objc
/// 크로스 룸 PK 요청 응답
/// 호스트가 다른 방 호스트의 PK 요청에 응답합니다.
/// - Parameters:
///   - user: PK를 요청한 호스트 ID
///   - agree: true: 동의, false: 거절
///   - reason: PK 동의/거절 이유 설명
/// - Note: 호스트가 응답하면 상대방 호스트가 `requestRoomPK`에서 전달한 `responseCallback` 콜백을 수신합니다.
- (void)responseRoomPKWithUserID:(NSString *)userID
                           agree:(BOOL)agree
                          reason:(NSString *)reason
NS_SWIFT_NAME(responseRoomPK(userID:agree:reason:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                      |
| ------ | ------- | ------------------------- |
| userID | String  | PK를 요청한 호스트 ID.   |
| agree  | Bool    | true: 동의, false: 거절. |
| reason | String? | PK 동의/거절 이유 설명. |


### quitRoomPK

크로스 룸 PK를 종료합니다. PK 중, 한쪽 호스트가 크로스 룸 PK를 종료하면 다른 호스트는 `TRTCLiveRoomDelegate`의 `trtcLiveRoomOnQuitRoomPK()` 콜백 알람을 수신합니다.

```objc
/// 호스트 크로스 룸 PK 퇴장
/// - Parameter callback: 크로스 룸 PK 퇴장 결과 콜백
/// - Note: 두 호스트 중 한 호스트가 크로스 룸 PK 상태에서 나가면 다른 호스트가 `trtcLiveRoomOnQuitRoomPK` 콜백 알림을 수신합니다.
- (void)quitRoomPK:(Callback _Nullable)callback
NS_SWIFT_NAME(quitRoomPK(callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미       |
| -------- | ----------------------------------------- | ---------- |
| callback | (_ code: Int, _ message: String?) -> Void | 작업 콜백. |


## 멀티미디어 제어 관련 API

### switchCamera

전면/후면 카메라를 전환합니다.

```objc
/// 전면/후면 카메라 전환
- (void)switchCamera;
```


### setMirror

미러 이미지 표시 여부를 설정합니다.

```objc
/// 미러 이미지 표시 여부 설정
/// - Parameter isMirror: 미러 이미지 활성화/비활성화.
- (void)setMirror:(BOOL)isMirror
NS_SWIFT_NAME(setMirror(isMirror:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미       |
| -------- | ---- | --------------- |
| isMirror | Bool | 미러 이미지 활성화/비활성화. |


### muteLocalAudio

로컬 오디오를 음소거합니다.

```objc
/// 로컬 오디오 음소거.
/// - Parameter isMuted: true: 음소거 켜기, false: 음소거 끄기.
- (void)muteLocalAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteLocalAudio(isMuted:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형 | 의미                              |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true: 음소거 켜기, false: 음소거 끄기. |

### muteRemoteAudio

원격 오디오를 음소거합니다.

```objc
/// 원격 오디오 음소거
/// - Parameters:
///   - userID: 원격 사용자 ID.
///   - isMuted: true: 음소거 켜기, false: 음소거 끄기.
- (void)muteRemoteAudioWithUserID:(NSString *)userID isMuted:(BOOL)isMuted
NS_SWIFT_NAME(muteRemoteAudio(userID:isMuted:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                              |
| ------- | ------ | --------------------------------- |
| userID  | String | 원격 사용자 ID.                   |
| isMuted | Bool   | true: 음소거 켜기, false: 음소거 끄기. |



### muteAllRemoteAudio

모든 원격 오디오를 음소거합니다.

```objc
/// 모든 원격 오디오 음소거
/// - Parameter isMuted: true: 음소거 켜기, false: 음소거 끄기.
- (void)muteAllRemoteAudio:(BOOL)isMuted
NS_SWIFT_NAME(muteAllRemoteAudio(_:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형 | 의미                              |
| ------- | ---- | --------------------------------- |
| isMuted | Bool | true: 음소거 켜기, false: 음소거 끄기. |

### setAudioQuality

오디오 품질을 설정합니다.

```objc
/// 오디오 품질 설정. 값은 1, 2, 3으로 설정할 수 있으며 저, 중, 고를 의미
/// - Parameter quality 오디오 품질
- (void)setAudioQuality:(NSInteger)quality
NS_SWIFT_NAME(setAudioiQuality(quality:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형      | 의미                         |
| ------- | --------- | ---------------------------- |
| quality | NSInteger | 1: 음성, 2: 표준, 3: 음악. |

## 배경 음악 음향 효과 관련 API

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af962213fefe6988a08820ac9af00df66) 가져오기.

```objc
/// 음향 효과 관리 객체 획득
- (TXAudioEffectManager *)getAudioEffectManager;
```

## 뷰티 필터 관련 API

### getBeautyManager

뷰티 필터 관리 객체 [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#interfaceTXBeautyManager) 가져오기.

```objc
/* 뷰티 필터 관리 객체 TXBeautyManager 획득
*
* 뷰티 필터 관리를 통해 다음 기능을 사용할 수 있습니다.
* - '뷰티 필터 스타일', '미백', '안색 보정', '눈 크게', '갸름하게', 'V라인', '턱 조정', '얼굴 짧게', '코 작게', '반짝이는 눈', '치아 미백', '아래 눈꺼풀 조정', '주름 제거', '팔자 주름 제거' 등 뷰티 효과를 설정할 수 있습니다.
* - '헤어 라인', '눈 간격', '눈 각도', '입 모양', '콧볼', '코 위치', '입술 두께', '얼굴형'을 조정할 수 있습니다.
* - 얼굴 효과(소재) 등 동적 효과를 설정할 수 있습니다.
* - 메이크업 효과 추가합니다.
* - 손 동작을 인식합니다.
*/
- (TXBeautyManager *)getBeautyManager;
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

```objc
/// 텍스트 메시지 발송, 방 안 모든 사용자가 볼 수 있음
/// - Parameters:
///   - message: 텍스트 메시지.
///   - callback: 발송 콜백.
- (void)sendRoomTextMsg:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미           |
| -------- | ----------------------------------------- | -------------- |
| message  | String                                    | 텍스트 메시지.     |
| callback | (_ code: Int, _ message: String?) -> Void | 발송 결과 콜백. |


### sendRoomCustomMsg

사용자 정의 텍스트 메시지 발송.

```objc
/// 사용자 정의 메시지 발송
/// - Parameters:
///   - command: 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용
///   - message: 텍스트 메시지.
///   - callback: 발송 콜백.
- (void)sendRoomCustomMsgWithCommand:(NSString *)command message:(NSString *)message callback:(Callback _Nullable)callback
NS_SWIFT_NAME(sendRoomCustomMsg(command:message:callback:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                                      | 의미                                               |
| -------- | ----------------------------------------- | -------------------------------------------------- |
| command  | String                                    | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String                                    | 텍스트 메시지.                                         |
| callback | (_ code: Int, _ message: String?) -> Void | 발송 결과 콜백.                                     |


## 디버깅 관련 API

### showVideoDebugLog

인터페이스에 debug 정보 표시 여부를 설정합니다.

```objc
/// 인터페이스에 debug 정보 표시 여부 설정
/// - Parameter isShow: Debug 정보 표시/표시하지 않음.
- (void)showVideoDebugLog:(BOOL)isShow
NS_SWIFT_NAME(showVideoDebugLog(_:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                       |
| ------ | ---- | -------------------------- |
| isShow | Bool | Debug 정보 표시/표시하지 않음 |


## TRTCLiveRoomDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백.

>?SDK가 복구할 수 없는 오류는 반드시 모니터링하고 상황에 따라 적절한 인터페이스를 사용자에게 제시해야 합니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
             onError:(NSInteger)code
             message:(NSString  *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onError:message:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스. |
| code         | Int              | 오류 코드.                     |
| message      | String?          | 오류 정보.                   |


### onWarning

경고 콜백.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
           onWarning:(NSInteger)code
             message:(NSString *)message
NS_SWIFT_NAME(trtcLiveRoom(_:onWarning:message:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| code         | Int              | 오류 코드 TRTCWarningCode.     |
| message      | String?          | 경고 정보.                   |



### onDebugLog

Log 콜백.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
          onDebugLog:(NSString *)log
NS_SWIFT_NAME(trtcLiveRoom(_:onDebugLog:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| log          | String           | 로그 정보.                   |


## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백입니다. 호스트가 퇴장하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onRoomDestroy:(NSString *)roomID
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomDestroy:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| roomID       | String           | 방 ID.                    |


### onRoomInfoChange

라이브 방송 방 정보 변경 시 콜백입니다. 라이브 방송 마이크 연결, PK 방 나가기 등 상태 변화를 알려주는 시나리오에 많이 사용됩니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
    onRoomInfoChange:(TRTCLiveRoomInfo *)info
NS_SWIFT_NAME(trtcLiveRoom(_:onRoomInfoChange:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| info         | TRTCLiveRoomInfo | 방 정보.                   |




## 호스트와 시청자 방 입장/퇴장 이벤트 콜백

### onAnchorEnter

새로운 호스트의 방 입장 알림을 수신합니다. 마이크가 연결된 시청자 및 크로스 룸 PK 호스트가 입장하면 시청자는 새로운 호스트의 방 입장 이벤트를 수신하며, 호스트는 `TRTCLiveRoom`의 `startPlay()`을 호출하여 해당 호스트의 비디오 화면을 재생합니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
       onAnchorEnter:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorEnter:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| userID       | String           | 새로 입장한 사용자 ID.              |



### onAnchorExit

호스트의 방 퇴장 알림을 수신합니다. 방 안에 있는 호스트(및 마이크 연결 중인 시청자)는 새로운 호스트의 방 퇴장 알림을 수신하며, `TRTCLiveRoom`의 `stopPlay()`를 호출하여 해당 호스트의 비디오 화면을 끕니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
        onAnchorExit:(NSString *)userID
NS_SWIFT_NAME(trtcLiveRoom(_:onAnchorExit:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| userID       | String           | 퇴장한 사용자 ID.               |



### onAudienceEnter

시청자 방 입장 공지 수신.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onAudienceEnter:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceEnter:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| user         | TRTCLiveUserInfo | 입장한 시청자 정보.               |


### onAudienceExit

시청자 방 퇴장 공지 수신.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
      onAudienceExit:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onAudienceExit:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| user         | TRTCLiveUserInfo | 퇴장한 시청자 정보.               |


## 호스트와 시청자 마이크 연결 이벤트 콜백

### onRequestJoinAnchor

호스트가 시청자 마이크 연결 요청 수신 시 콜백입니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
 onRequestJoinAnchor:(TRTCLiveUserInfo *)user
             reason:(NSString * _Nullable)reason
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestJoinAnchor:reason:timeout:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| user         | TRTCLiveUserInfo | 마이크 연결을 요청한 시청자 정보.           |
| reason       | String?          | 마이크 연결 이유 설명.               |
| timeout      | Double           | 요청 처리 타임 아웃 시간.         |


### onKickoutJoinAnchor

마이크가 연결된 시청자가 마이크 연결 강제 해제 알림을 수신합니다. 마이크가 연결된 시청자가 호스트에 의해 마이크 연결이 강제 해제되었다는 메시지를 수신하며, 호스트는 `TRTCLiveRoom`의 `stopPublish()`를 호출하여 마이크 연결을 해제해야 합니다.

```objc
- (void)trtcLiveRoomOnKickoutJoinAnchor:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnKickoutJoinAnchor(_:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |



## 호스트 PK 이벤트 콜백

### onRequestRoomPK

크로스 룸 PK 요청을 수신합니다. 호스트가 다른 방 호스트의 PK 요청을 수신하고 PK를 수락하면 `TRTCLiveRoomDelegate`의 `onAnchorEnter()` 알림을 기다린 후, `startPlay()`를 호출하여 PK를 요청한 호스트의 스트림을 재생합니다.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
     onRequestRoomPK:(TRTCLiveUserInfo *)user
             timeout:(double)timeout
NS_SWIFT_NAME(trtcLiveRoom(_:onRequestRoomPK:timeout:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| user         | TRTCLiveUserInfo | 크로스 룸 마이크 연결을 요청한 호스트 정보.     |
| timeout      | Double           | 요청 처리 타임 아웃 시간.         |


### onQuitRoomPK

크로스 룸 PK 종료 알림을 수신합니다.

```objc
 - (void)trtcLiveRoomOnQuitRoomPK:(TRTCLiveRoom *)liveRoom
NS_SWIFT_NAME(trtcLiveRoomOnQuitRoomPK(_:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |



## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지 수신.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
   onRecvRoomTextMsg:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomTextMsg:fromUser:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                         |
| ------------ | ---------------- | ---------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| message      | String           | 텍스트 메시지.                   |
| user         | TRTCLiveUserInfo | 발신자 정보.             |



### onRecvRoomCustomMsg

사용자 정의 메시지 수신.

```objc
- (void)trtcLiveRoom:(TRTCLiveRoom *)trtcLiveRoom
onRecvRoomCustomMsgWithCommand:(NSString *)command
             message:(NSString *)message
            fromUser:(TRTCLiveUserInfo *)user
NS_SWIFT_NAME(trtcLiveRoom(_:onRecvRoomCustomMsg:message:fromUser:));
```

매개변수는 다음과 같습니다.

| 매개변수         | 유형             | 의미                                               |
| ------------ | ---------------- | -------------------------------------------------- |
| trtcLiveRoom | TRTCLiveRoomImpl | 현재 TRTCLiveRoom 컴포넌트 인스턴스.                       |
| command      | String           | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message      | String           | 텍스트 메시지.                                         |
| user         | TRTCLiveUserInfo | 발신자 정보.                                   |
