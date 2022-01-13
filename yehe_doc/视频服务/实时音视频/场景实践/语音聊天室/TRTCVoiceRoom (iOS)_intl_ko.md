TRTCVoiceRoom은 Tencent Cloud의 Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 기반으로 구성되며, 다음 기능을 지원합니다.

- 방 주인이 신규 음성 채팅방을 생성하면 청취자가 음성 채팅방에 입장하여 청취 및 인터랙션.
- 방 주인이 청취자에게 마이크 켜기 요청 또는 마이크가 켜진 사용자의 마이크 강제 끄기.
- 방 주인의 자리 차단 및 청취자 마이크 연결 신청 차단.
- 청취자가 마이크 켜기를 신청하여 마이크가 켜진 호스트가 될 수 있고, 다른 사람들과 음성으로 인터랙션할 수 있으며, 언제든지 마이크를 끄고 일반 청취자가 될 수 있습니다.
- 다양한 텍스트 메시지 및 사용자 정의 메시지를 지원합니다. 사용자 정의 메시지를 이용해 댓글 자막, 좋아요, 선물 기능 등을 구현할 수 있습니다.

TRTCVoiceRoom은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [음성 채팅방(iOS)](https://intl.cloud.tencent.com/document/product/647/37287)을 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저지연 음성 채팅 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 AVChatroom을 사용해 채팅방 기능을 구현하며, IM 속성 인터페이스를 통해 마이크 위치 리스트 등 방 정보를 저장하고 초대 신호를 마이크 켜기 신청/마이크 넘기기에 사용할 수 있습니다.


<h2 id="TRTCVoiceRoom">TRTCVoiceRoom API 개요</h2>

### SDK 기본 함수

| API                                             | 설명                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | 컴포넌트 싱글톤 가져오기.           |
| [destroySharedInstance](#destroysharedinstance) | 컴포넌트 싱글톤 폐기.          |
| [setDelegate](#setdelegate)                     | 이벤트 콜백 설정.           |
| [setDelegateHandler](#setdelegatehandler)       | 이벤트 콜백이 있는 스레드 설정. |
| [login](#login)                                 | 로그인.                   |
| [logout](#logout)                               | 로그아웃.                   |
| [setSelfProfile](#setselfprofile)               | 개인 정보 수정.           |

### 방 관련 API

| API                                 | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | 방 생성(방 주인 호출), 방이 없는 경우 시스템에서 자동으로 새로운 방 생성. |
| [destroyRoom](#destroyroom)         | 방 폐기(방 주인 호출).                                       |
| [enterRoom](#enterroom)             | 방 입장(청취자 호출).                                       |
| [exitRoom](#exitroom)               | 방 퇴장(청취자 호출).                                       |
| [getRoomInfoList](#getroominfolist) | 방 리스트의 세부 정보 획득.                                     |
| [getUserInfoList](#getuserinfolist) | 지정 userId의 사용자 정보 획득, nil인 경우 방 안에 있는 모든 사용자 정보 획득. |

### 마이크 위치 관리 API

| API                     | 설명                                  |
| ----------------------- | ----------------------------------- |
| [enterSeat](#enterseat) | 마이크 연결(청취자와 방 주인 모두 호출 가능).  |
| [moveSeat](#moveseat)   | 마이크 위치 이동 (마이크 연결된 호스트 호출 가능). |
| [leaveSeat](#leaveseat) | 마이크 연결 해제(호스트 호출).  |
| [pickSeat](#pickseat)   | 마이크 넘기기(방 주인 호출).             |
| [kickSeat](#kickseat)   | 마이크 강제 끄기(방 주인 호출).             |
| [muteSeat](#muteseat)   | 특정 마이크 위치 음소거/음소거 해제(방 주인 호출). |
| [closeSeat](#closeseat) | 특정 마이크 위치 차단/차단 해제(방 주인 호출).     |

### 로컬 오디오 작업 API

| API                                             | 설명                 |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | 마이크 수집 시작.     |
| [stopMicrophone](#stopmicrophone)               | 마이크 수집 중지.     |
| [setAudioQuality](#setaudioquality)             | 오디오 품질 설정.           |
| [muteLocalAudio](#mutelocalaudio)               | 로컬 음소거 활성화/비활성화.  |
| [setSpeaker](#setspeaker)                       | 스피커 활성화 설정.     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | 마이크 수집 음량 설정.|
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 재생 볼륨 설정.       |
| [setVoiceEarMonitorEnable](#setvoiceearmonitorenable) | 인이어 모니터링 활성화/비활성화.       |


### 원격 사용자 오디오 작업 API

| API                                           | 설명                   |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 특정 사용자 음소거/음소거 해제. |
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 사용자 음소거/음소거 해제. |

### 배경 음악 음향 효과 관련 API

| API                                             | 설명                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html#interfacecom_1_1tencent_1_1liteav_1_1audio_1_1TXAudioEffectManager) 가져오기. |

### 메시지 발송 관련 API

| API                                     | 설명                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용. |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송.                     |

### 초대 신호 관련 API

| API                                           | 설명             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | 사용자에게 초대 발송. |
| [acceptInvitation](#acceptinvitation) | 초대 수락.       |
| [rejectInvitation](#rejectinvitation) | 초대 거부.       |
| [cancelInvitation](#cancelinvitation) | 초대 취소.       |

<h2 id="TRTCVoiceRoomDelegate">TRTCVoiceRoomDelegate API 개요</h2>

### 일반적인 이벤트 콜백

| API                        | 설명        |
| ------------------------- | ---------- |
| [onError](#onerror)       | 오류 콜백. |
| [onWarning](#onwarning)   | 경고 콜백. |
| [onDebugLog](#ondebuglog) | Log 콜백. |

### 방 이벤트 콜백

| API                                   | 설명                     |
| ----------------------------------------- | ---------------------- |
| [onRoomDestroy](#onroomdestroy)           | 방 폐기 콜백.     |
| [onRoomInfoChange](#onroominfochange)     | 음성 채팅방 정보 변경 콜백. |
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 볼륨 콜백.     |

### 마이크 위치 변경 콜백

| API                                     | 설명                                  |
| --------------------------------------- | ------------------------------------- |
| [onSeatListChange](#onseatlistchange)   | 전체 마이크 위치 리스트 변경.                |
| [onAnchorEnterSeat](#onanchorenterseat) | 사용자 마이크 켜짐(직접 마이크 켬/방 주인 특정 사용자 마이크 켬). |
| [onAnchorLeaveSeat](#onanchorleaveseat) | 사용자 마이크 꺼짐(직접 마이크 끔/방 주인이 특정 사용자 마이크 끔). |
| [onSeatMute](#onseatmute)               | 방 주인 마이크 음소거.                            |
| [onUserMicrophoneMute](#onusermicrophonemute)               | 사용자 마이크 음소거 여부.                          |
| [onSeatClose](#onseatclose)             | 방 주인 마이크 차단.                            |

### 청취자 입장/퇴장 이벤트 콜백

| API                                | 설명                 |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | 청취자 입장 알림 수신. |
| [onAudienceExit](#onaudienceexit)   | 청취자 퇴장 알림 수신. |

### 메시지 이벤트 콜백

| API                                 | 설명                |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | 텍스트 메시지 수신.   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신.|

### 신호 이벤트 콜백

| API                                               | 설명               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 새로운 초대 요청 수신.   |
| [onInviteeAccepted](#oninviteeaccepted)           | 초대된 사용자가 초대 수락.   |
| [onInviteeRejected](#oninviteerejected)           | 초대된 사용자가 초대 거절.   |
| [onInvitationCancelled](#oninvitationcancelled)   | 초대한 사용자가 초대 취소.   |

## SDK 기본 함수

[](id:sharedInstance)

### sharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286) 싱글톤 객체를 가져옵니다.

```Objective-C
/**
* TRTCVoiceRoom 싱글톤 객체 획득
*
* - returns: TRTCVoiceRoom 인스턴스
* - note: {@link TRTCVoiceRoom#destroySharedInstance()}를 호출하여 싱글톤 객체 폐기
*/
+ (instancetype)sharedInstance NS_SWIFT_NAME(shared());
```


### destroySharedInstance

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) 싱글톤 객체를 폐기합니다.

>?인스턴스 폐기 후에는 외부에 캐시된 TRTCVoiceRoom 인스턴스를 다시 사용할 수 없으며, 다시 [sharedInstance](#sharedInstance)를 호출해 새로운 인스턴스를 획득해야 합니다.

```Objective-C
/**
* TRTCVoiceRoom 싱글톤 객체 폐기
*
* - note: 인스턴스 폐기 후에는 외부에 캐시된 TRTCVoiceRoom 인스턴스를 다시 사용할 수 없으며, 다시 {@link TRTCVoiceRoom#sharedInstance()}를 호출해 새로운 인스턴스 획득
*/
+ (void)destroySharedInstance NS_SWIFT_NAME(destroyShared());
```

### setDelegate

[TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37287) 이벤트 콜백은 TRTCVoiceRoomDelegate를 통해 [TRTCVoiceRoom](https://intl.cloud.tencent.com/document/product/647/37286)의 다양한 상태 알림을 받아볼 수 있습니다.

```Objective-C
/**
* 컴포넌트 콜백 인터페이스 설정
* 
* TRTCVoiceRoomDelegate를 통해 TRTCVoiceRoom의 다양한 상태 알림 가져오기
*
* - parameter delegate 콜백 인터페이스
* - note: TRTCVoiceRoom의 이벤트 콜백은 기본적으로 Main Queue에서 귀하에게 콜백합니다. 이벤트 콜백이 존재하는 큐를 지정할 경우 {@link TRTCVoiceRoom#setDelegateQueue(queue)} 이용 가능
*/
- (void)setDelegate:(id<TRTCVoiceRoomDelegate>)delegate NS_SWIFT_NAME(setDelegate(delegate:));
```

>?setDelegate는 TRTCVoiceRoom의 프록시의 콜백입니다.   

### setDelegateQueue

이벤트 콜백이 존재하는 스레드 큐를 설정합니다. 기본적으로 메인 스레드 MainQueue로 발송합니다.

```Objective-C
/**
* 이벤트 콜백이 있는 큐 설정
*
* - parameter queue 큐입니다. TRTCVoiceRoom의 각종 상태 알림을 콜백하며 지정한 queue로 배포합니다.
*/
- (void)setDelegateQueue:(dispatch_queue_t)queue NS_SWIFT_NAME(setDelegateQueue(queue:));

```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형             | 의미                                                         |
| ----- | ---------------- | ------------------------------------------------------------ |
| queue | dispatch_queue_t | TRTCVoiceRoom의 각종 상태를 통지하며, 지정한 스레드 큐로 배포합니다. |

   

### login

로그인합니다.

```Objective-C
- (void)login:(int)sdkAppID
       userId:(NSString *)userId
      userSig:(NSString *)userSig
     callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(login(sdkAppID:userId:userSig:callback:));

```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int            | **TRTC 콘솔 >[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)**> 애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | NSString            | 현재 사용자 ID, 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시부호(-), 언더바(\_)만 허용됩니다. |
| userSig  | NSString         | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |
| callback | ActionCallback | 로그인 콜백이며, 성공 시 code는 0입니다. |

   

### logout

로그아웃합니다.

```Objective-C
- (void)logout:(ActionCallback _Nullable)callback NS_SWIFT_NAME(logout(callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미                       |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | 로그아웃 콜백이며, 성공 시 code는 0입니다. |

   

### setSelfProfile

개인 정보를 수정합니다.

```Objective-C
- (void)setSelfProfile:(NSString *)userName avatarURL:(NSString *)avatarURL callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(setSelfProfile(userName:avatarURL:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형              | 의미                                |
| --------- | -------------- | ----------------------------------- |
| userName  | NSString            | 대화명.                                |
| avatarURL | NSString         | 프로필 사진 주소.                          |
| callback  | ActionCallback | 개인 프로필 정보 설정 콜백이며, 성공 시 code는 0입니다. |

   


## 방 관련 API

### createRoom

방 생성(방 주인 호출).

```Objective-C
- (void)createRoom:(int)roomID roomParam:(VoiceRoomParam *)roomParam callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(createRoom(roomID:roomParam:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형                | 의미                                                         |
| --------- | ------------------- | ------------------------------------------------------------ |
| roomId    | int                 | 방 식별 번호이며, 귀하가 할당하고 통합 관리합니다. 여러 개의 roomID를 1개의 음성 채팅방 리스트로 통합할 수 있으며, Tencent Cloud는 현재 음성 채팅방 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | VoiceRoomParam | 방 정보입니다. 방 이름, 마이크 위치 정보, 썸네일 정보 등과 같이 방을 설명하는 데 사용됩니다. 마이크 위치 관리가 필요한 경우 방의 마이크 위치 개수를 설정해야 합니다. |
| callback  | ActionCallback      | 방 생성 결과 콜백이며, 성공 시 code는 0입니다.                        |

방 주인의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 
1. 방 주인이 `createRoom`을 호출하여 새로운 음성 채팅방을 생성합니다. 이 때 방 ID, 마이크 연결 시 방 주인 확인 필요 여부, 마이크 위치 개수 등 방 속성 정보를 전송합니다.
2. 방 주인이 방 생성 후 `enterSeat`을 호출하여 자리에 입장합니다.
3. 방 주인이 컴포넌트의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
4. 방 주인은 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 알림 또한 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

   

### destroyRoom

방 폐기(방 주인 호출). 방 주인은 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```Objective-C
- (void)destroyRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(destroyRoom(callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형          | 의미                               |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |


### enterRoom

방 입장(청취자 호출).

```Objective-C
- (void)enterRoom:(NSInteger)roomID callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterRoom(roomID:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형            | 의미                               |
| -------- | -------------- | ------------------------------------- |
| roomId   | NSInteger            | 방 식별 번호.                            |
| callback | ActionCallback | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |


청취자가 방에 입장하여 청취하는 정상적인 호출 프로세스는 다음과 같습니다. 

1. 청취자가 귀하의 서버에서 최신 음성 채팅방 리스트를 획득하며, 여기에는 여러 음성 채팅방의 roomId 및 방 정보가 포함될 수 있습니다.
2. 청취자가 음성 채팅방 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
3. 방 입장 후 컴포넌트의 `onRoomInfoChange` 방 속성 변경 이벤트 공지를 수신합니다. 이 때 UI에 방 이름 표시, 마이크를 켤 때 방 주인에게 동의 요청 필요 여부 기록 등 방의 속성을 기록할 수 있으며 그에 해당하는 변경이 가능합니다.
4. 방 입장 후 컴포넌트의 `onSeatListChange` 마이크 위치 리스트 변경 이벤트 알림을 수신합니다. 이 때 마이크 위치 리스트의 변경 내용을 UI 인터페이스에 새로고침할 수 있습니다.
5. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 공지도 수신합니다.

### exitRoom

방 퇴장.

```Objective-C
- (void)exitRoom:(ActionCallback _Nullable)callback NS_SWIFT_NAME(exitRoom(callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미                            |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |

   

### getRoomInfoList

방 리스트의 세부 정보를 획득합니다. 방 이름, 방 썸네일은 방 주인이 `createRoom()` 생성 시 roomInfo를 통해 설정할 수 있습니다.

>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```Objective-C
- (void)getRoomInfoList:(NSArray<NSNumber *> *)roomIdList callback:(VoiceRoomInfoCallback _Nullable)callback NS_SWIFT_NAME(getRoomInfoList(roomIdList:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수       | 유형                  | 의미                 |
| ---------- | ------------------- | ------------------ |
| roomIdList | NSArray&lt;NSNumber&gt; | 방 번호 리스트.       |
| callback   | RoomInfoCallback    | 방 세부 정보 콜백. |


### getUserInfoList

지정 userId의 사용자 정보 획득.

```Objective-C
- (void)getUserInfoList:(NSArray<NSString *> * _Nullable)userIDList callback:(VoiceRoomUserListCallback _Nullable)callback NS_SWIFT_NAME(getUserInfoList(userIDList:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수             | 유형               | 의미                                                         |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList | NSArray&lt;NSString&gt; | 획득할 사용자 ID 리스트입니다. null인 경우 방 안에 있는 모든 사용자 정보를 획득합니다. |
| userlistcallback | UserListCallback   | 사용자 세부 정보 콜백.                                           |


## 마이크 위치 관리 API

### enterSeat

직접 마이크 켜기(청취자 및 방 주인 모두 호출 가능).

>?마이크 연결 완료 후, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.

```Objective-C
- (void)enterSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(enterSeat(seatIndex:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형           | 의미                 |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger    | 마이크를 연결할 마이크 위치 번호. |
| callback  | ActionCallback | 작업 콜백.           |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 청취자의 마이크 연결에 방 주인의 동의가 필요한 시나리오의 경우, 먼저 `sendInvitation`을 호출하여 방 주인에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.

### moveSeat
마이크 위치 이동 (마이크 연결된 호스트 호출 가능).
>? 마이크 위치 이동 완료 후 방 안의 모든 구성원은 'onSeatListChange', 'onAnchorLeaveSeat' 및 'onAnchorEnterSeat'의 이벤트 알림을 받게 됩니다.(호스트 호출 후 마이크 좌석 번호 정보만 수정되며, 사용자의 호스트 신분은 변경되지 않습니다.)

```Objective-C
- (NSInteger)moveSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback
NS_SWIFT_NAME(moveSeat(seatIndex:callback:))
```
매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형           | 의미                   |
| --------- | -------------- | -------------------- |
| seatIndex | NSInteger      | 이동할 마이크 위치 번호. |
| callback  | ActionCallback | 작업 콜백.           |

반환값:

| 반환값   | 유형   | 의미                  |
| -------- | --------- | --------------------- |
| code     | NSInteger | 마이크 위치 이동 결과(0은 성공, 그 외는 실패, 10001은 인터페이스 호출 빈도 제한). |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 청취자의 마이크 연결에 방 주인의 동의가 필요한 시나리오의 경우, 먼저 `sendInvitation`을 호출하여 방 주인에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.

### leaveSeat

직접 마이크 끔(호스트 호출).

>? 마이크 연결 해제 완료 후, 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

```Objective-C
- (void)leaveSeat:(ActionCallback _Nullable)callback NS_SWIFT_NAME(leaveSeat(callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형           | 의미        |
| -------- | -------------- | ---------- |
| callback  | ActionCallback | 작업 콜백.|

### pickSeat

특정 사용자 마이크 켜기(방 주인 호출).

>? 방 주인이 마이크를 연결할 사용자를 지정하면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorEnterSeat` 이벤트 알림을 수신합니다.

```Objective-C
- (void)pickSeat:(NSInteger)seatIndex userId:(NSString *)userId callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(pickSeat(seatIndex:userId:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형           | 의미                     |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger    | 마이크를 연결할 마이크 위치 번호. |
| userId    | NSString      | 사용자 ID.              |
| callback  | ActionCallback | 작업 콜백.             |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 방 주인이 청취자의 동의를 얻어야만 청취자가 마이크를 연결할 수 있는 시나리오의 경우 먼저 `sendInvitation`을 호출하여 청취자에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.


### kickSeat

특정 사용자 마이크 끄기(방 주인 호출).

>? 방 주인이 특정 사용자의 마이크를 끄면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onAnchorLeaveSeat` 이벤트 알림을 수신합니다.

```Objective-C
- (void)kickSeat:(NSInteger)seatIndex callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(kickSeat(seatIndex:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형           | 의미                     |
| --------- | -------------- | ---------------------- |
| seatIndex | NSInteger       | 마이크 연결을 해제할 마이크 위치 번호. |
| callback  | ActionCallback | 작업 콜백.             |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다.

### muteSeat

특정 마이크 위치 음소거/음소거 해제(방 주인 호출).

>? 특정 마이크 위치를 음소거/음소거 해제하면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onSeatMute` 이벤트 알림을 수신합니다.

```Objective-C
- (void)muteSeat:(NSInteger)seatIndex isMute:(BOOL)isMute callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(muteSeat(seatIndex:isMute:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미                                    |
| --------- | -------------- | --------------------------------------------- |
| seatIndex | NSInteger            | 작업 진행할 마이크 위치 번호.                          |
| isMute    | BOOL           | YES: 음소거, NO: 음소거 해제. |
| callback  | ActionCallback | 작업 콜백.                                    |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 해당 seatIndex 자리에 있는 호스트는 자동으로 muteAudio가 호출되어 음소거/음소거 해제됩니다.

### closeSeat

특정 마이크 위치 차단/차단 해제(방 주인 호출).

>? 방 주인이 해당 마이크 위치를 차단/차단 해제하면 방 안에 있는 모든 사용자가 `onSeatListChange` 및 `onSeatClose` 이벤트 알림을 수신합니다.

```Objective-C
- (void)closeSeat:(NSInteger)seatIndex isClose:(BOOL)isClose callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(closeSeat(seatIndex:isClose:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형            | 의미                                   |
| --------- | -------------- | ------------------------------------------ |
| seatIndex | NSInteger            | 작업 진행할 마이크 위치 번호.                          |
| isClose   | BOOL           | YES: 차단, NO: 해제. |
| callback  | ActionCallback | 작업 콜백.                                 |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 해당 seatIndex 자리가 차단되고 자동으로 마이크 연결이 해제됩니다.


## 로컬 오디오 작업 API

### startMicrophone

마이크 수집을 시작합니다.

```Objective-C
- (void)startMicrophone;
```

### stopMicrophone

마이크 수집을 중지합니다.

```Objective-C
- (void)stopMicrophone;
```

### setAudioQuality

오디오 품질을 설정합니다.

```Objective-C
- (void)setAuidoQuality:(NSInteger)quality NS_SWIFT_NAME(setAuidoQuality(quality:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형             | 의미                                                         |
| ------- | ---------- | ------------------------------------------------------------ |
| quality | NSInteger  | 오디오의 품질입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참고하십시오. |


### muteLocalAudio

로컬 오디오를 음소거/음소거 취소합니다.

```Objective-C
- (void)muteLocalAudio:(BOOL)mute NS_SWIFT_NAME(muteLocalAudio(mute:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수          | 유형    | 의미                                                    |
| ---- | ------- | ------------------------------------------------------------ |
| mute | BOOL    | 오디오를 음소거/음소거 취소합니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)를 참고하십시오. |



### setSpeaker

스피커를 활성화합니다.

```Objective-C
- (void)setSpeaker:(BOOL)userSpeaker NS_SWIFT_NAME(setSpeaker(userSpeaker:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미                           |
| ---------- | ------- | --------------------------- |
| useSpeaker | BOOL    | YES: 스피커, NO: 헤드셋. |



### setAudioCaptureVolume

마이크 수집 볼륨을 설정합니다.

```Objective-C
- (void)setAudioCaptureVolume:(NSInteger)voluem NS_SWIFT_NAME(setAudioCaptureVolume(volume:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | NSInteger | 수집 볼륨, 0 - 100으로 설정할 수 있으며 기본 값은 100입니다. |


### setAudioPlayoutVolume

재생 볼륨을 설정합니다.

```Objective-C
- (void)setAudioPlayoutVolume:(NSInteger)volume NS_SWIFT_NAME(setAudioPlayoutVolume(volume:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형 | 의미                          |
| ------ | ---------- | ----------------------------- |
| volume | NSInteger | 재생 볼륨, 0 - 100으로 설정할 수 있으며 기본 값은 100입니다. |

### muteRemoteAudio

지정 사용자 음소거/음소거 해제.

```Objective-C
- (void)muteRemoteAudio:(NSString *)userId mute:(BOOL)mute NS_SWIFT_NAME(muteRemoteAudio(userId:mute:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미                                |
| ------ | ------- | --------------------------------- |
| userId   | NSString  | 지정된 사용자 ID.                       |
| mute   | BOOL      | YES: 음소거, NO: 음소거 해제. |

### muteAllRemoteAudio

모든 사용자 음소거/음소거 해제.

```Objective-C
- (void)muteAllRemoteAudio:(BOOL)isMute NS_SWIFT_NAME(muteAllRemoteAudio(isMute:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형    | 의미                               |
| ---- | ------- | --------------------------------- |
| mute | BOOL | YES: 음소거, NO: 음소거 해제. |

### setVoiceEarMonitorEnable

인이어 모니터링 활성화/비활성화.

```Objective-C
- (void)setVoiceEarMonitorEnable:(BOOL)enable NS_SWIFT_NAME(setVoiceEarMonitor(enable:));
```
매개변수 리스트는 다음과 같습니다.

| 매개변수 | 유형    | 의미                                |
| ---- | ------- | --------------------------------- |
| enable | BOOL | YES: 인이어 모니터링 활성화, NO: 인이어 모니터링 비활성화. |


## 배경 음악 음향 효과 관련 API

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득.

```Objective-C
- (TXAudioEffectManager * _Nullable)getAudioEffectManager;
```


## 메시지 발송 관련 API

### sendRoomTextMsg

방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용.

```Objective-C
- (void)sendRoomTextMsg:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomTextMsg(message:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미            |
| -------- | -------------- | -------------- |
| message  | NSString            | 텍스트 메시지.     |
| callback | ActionCallback | 발송 결과 콜백.|

   

### sendRoomCustomMsg

사용자 정의 텍스트 메시지를 발송합니다.

```Objective-C
- (void)sendRoomCustomMsg:(NSString *)cmd message:(NSString *)message callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendRoomCustomMsg(cmd:message:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                           |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | NSString            | 명령어, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는데 사용합니다. |
| message  | NSString            | 텍스트 메시지.                                         |
| callback | ActionCallback | 발송 결과 콜백.                                     |

   

## 초대 신호 관련 API

### sendInvitation

사용자에게 초대 발송.

```Objective-C
- (NSString *)sendInvitation:(NSString *)cmd
                      userId:(NSString *)userId
                     content:(NSString *)content
                    callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(sendInvitation(cmd:userId:content:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미             |
| -------- | -------------- | ---------------- |
| cmd      | NSString         | 서비스의 사용자 정의 명령. |
| userId   | NSString         | 초대한 사용자 ID.   |
| content  | NSString         | 초대 내용.     |
| callback | ActionCallback | 발송 결과 콜백.   |

반환값:

| 반환값   | 유형   | 의미                  |
| -------- | ------ | --------------------- |
| inviteId | NSString | 해당 초대 ID를 식별하는 데 사용. |

### acceptInvitation

초대 수락.

```Objective-C
- (void)acceptInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(acceptInvitation(id:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미           |
| -------- | -------------- | -------------- |
| id       | NSString       | 초대 ID.      |
| callback | ActionCallback | 발송 결과 콜백.|

### rejectInvitation

초대 거부.

```Objective-C
- (void)rejectInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(rejectInvitation(id:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미             |
| -------- | -------------- | -------------- |
| id       | NSString       | 초대 ID.      |
| callback | ActionCallback | 발송 결과 콜백.|


### cancelInvitation

초대 취소.

```Objective-C
- (void)cancelInvitation:(NSString *)identifier callback:(ActionCallback _Nullable)callback NS_SWIFT_NAME(cancelInvitation(id:callback:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형             | 의미             |
| -------- | -------------- | -------------- |
| id       | NSString       | 초대 ID.      |
| callback | ActionCallback | 발송 결과 콜백.|

[](id:TRTCVoiceRoomDelegate)
## TRTCVoiceRoomDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백.

>? SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 적절한 인터페이스로 사용자에게 안내해야 합니다.

```Objective-C
- (void)onError:(int)code
                message:(NSString*)message
NS_SWIFT_NAME(onError(code:message:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수       | 유형   | 의미       |
| ------- | ------ | ---------- |
| code    | int    | 오류 코드.   |
| message | NSString  | 오류 정보. |


### onWarning

경고 콜백.

```Objective-C
- (void)onWarning:(int)code
                  message:(NSString *)message
NS_SWIFT_NAME(onWarning(code:message:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미        |
| ------- | ------ | ---------- |
| code    | int    | 오류 코드.   |
| message | NSString | 경고 정보. |

   

### onDebugLog

Log 콜백.

```Objective-C
- (void)onDebugLog:(NSString *)message
NS_SWIFT_NAME(onDebugLog(message:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미        |
| ------- | ------ | ---------- |
| message | NSString | 로그 정보. |

   


## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백. 방 주인이 방을 종료하면 방 안에 있는 모든 사용자는 해당 알림을 받게 됩니다.

```Objective-C
- (void)onRoomDestroy:(NSString *)roomId
NS_SWIFT_NAME(onRoomDestroy(roomId:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미      |
| ------ | ------ | --------- |
| roomId | NSString | 방 ID. |


### onRoomInfoChange

방 입장 후 해당 인터페이스를 콜백합니다. roomInfo의 정보는 방 주인이 방 생성 시 입력한 정보입니다.

```Objective-C
- (void)onRoomInfoChange:(VoiceRoomInfo *)roomInfo
NS_SWIFT_NAME(onRoomInfoChange(roomInfo:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형     | 의미       |
| -------- | -------- | ---------- |
| roomInfo | VoiceRoomInfo | 방 정보. |


### onUserMicrophoneMute

사용자 마이크의 음소거 여부 콜백으로 사용자가 muteLocalAudio 호출하면 방의 모든 사용자는 해당 알림을 받게 됩니다.

```Objective-C
- (void)onUserMicrophoneMute:(NSString *)userId mute:(BOOL)mute
NS_SWIFT_NAME(onUserMicrophoneMute(userId:mute:));

```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미                        |
| ------ | ------ | ------------------------- |
| userId | NSString  | 사용자 ID.            |
| mute | BOOL    | YES: 음소거, NO: 음소거 해제. |


### onUserVolumeUpdate

음량 크기 알림을 활성화하여 모든 참석자의 음량 크기를 통지합니다.

```Objective-C
- (void)onUserVolumeUpdate:(NSArray<TRTCVolumeInfo *> *)userVolumes totalVolume:(NSInteger)totalVolume
NS_SWIFT_NAME(onUserVolumeUpdate(userVolumes:totalVolume:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수   | 유형   | 의미                        |
| ------ | ------ | ------------------------- |
| userVolumes | NSArray | 사용자 리스트.                 |
| totalVolume | NSInteger | 볼륨 크기, 값: 0 - 100. |


## 마이크 위치 콜백

### onSeatListChange

모든 마이크 위치 리스트를 포함한 전체 마이크 위치 리스트를 변경합니다.

```Objective-C
- (void)onSeatInfoChange:(NSArray<VoiceRoomSeatInfo *> *)seatInfolist
NS_SWIFT_NAME(onSeatListChange(seatInfoList:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수         | 유형             | 의미            |
| ------------ | -------------------- | ---------------- |
| seatInfoList | NSArray&lt;VoiceRoomSeatInfo&gt; | 전체 마이크 위치 리스트. |

### onAnchorEnterSeat

사용자 마이크 켜짐(직접 마이크 켬/방 주인이 특정 사용자 마이크 켬).

```Objective-C
- (void)onAnchorEnterSeat:(NSInteger)index
                              user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorEnterSeat(index:user:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형     | 의미                  |
| ----- | -------- | -------------------- |
| index | NSInteger      | 마이크가 연결된 마이크 위치.     |
| user  | VoiceRoomUserInfo | 마이크가 연결된 사용자의 세부 정보. |

### onAnchorLeaveSeat

사용자 마이크 꺼짐(직접 마이크 끔/방 주인이 특정 사용자 마이크 끔).

```Objective-C
- (void)onAnchorLeaveSeat:(NSInteger)index
                     user:(VoiceRoomUserInfo *)user
NS_SWIFT_NAME(onAnchorLeaveSeat(index:user:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수  | 유형     | 의미                 |
| ----- | -------- | -------------------- |
| index | NSInteger      | 연결을 해제할 마이크 위치.         |
| user  | VoiceRoomUserInfo |  마이크가 연결된 사용자의 세부 정보. |

### onSeatMute

방 주인 마이크 비활성화.

```Objective-C
- (void)onSeatMute:(NSInteger)index
            isMute:(BOOL)isMute
NS_SWIFT_NAME(onSeatMute(index:isMute:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미                              |
| ------ | ------- | ---------------------------------- |
| index  | NSInteger     | 작업 진행할 마이크 위치.                       |
| isMute | BOOL | YES: 음소거, NO: 음소거 해제. |

### onSeatClose

방 주인 마이크 차단.

```Objective-C
- (void)onSeatClose:(NSInteger)index
            isClose:(BOOL)isClose
NS_SWIFT_NAME(onSeatClose(index:isClose:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형    | 의미                                |
| ------- | ------- | ----------------------------------- |
| index   | NSInteger     | 작업 진행할 마이크 위치.                        |
| isClose | BOOL | YES: 차단, NO: 차단 해제. |

## 청취자 입장/퇴장 이벤트 콜백

### onAudienceEnter

청취자 방 입장 알림 수신.

```Objective-C
- (void)onAudienceEnter:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceEnter(userInfo:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형     | 의미            |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | 입장한 청취자 정보. |

### onAudienceExit

청취자 방 퇴장 알림 수신.

```Objective-C
- (void)onAudienceExit:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onAudienceExit(userInfo:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형     | 의미             |
| -------- | -------- | -------------- |
| userInfo | VoiceRoomUserInfo | 퇴장한 청취자 정보. |

   

## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지를 수신합니다.

```Objective-C
- (void)onRecvRoomTextMsg:(NSString *)message
                 userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomTextMsg(message:userInfo:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형     | 의미               |
| -------- | -------- | ---------------- |
| message  | NSString    | 텍스트 메시지.       |
| userInfo | VoiceRoomUserInfo | 발신자 정보. |

   

### onRecvRoomCustomMsg

사용자 정의 메시지를 수신합니다.

```Objective-C
- (void)onRecvRoomCustomMsg:(NSString *)command
                    message:(NSString *)message
                   userInfo:(VoiceRoomUserInfo *)userInfo
NS_SWIFT_NAME(onRecvRoomCustomMsg(command:message:userInfo:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형     | 의미                                          |
| -------- | -------- | -------------------------------------------------- |
| command  | NSString   | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는데 사용합니다. |
| message  | NSString   | 텍스트 메시지.                                     |
| userInfo | VoiceRoomUserInfo | 발신자 정보.                                   |

## 초대 신호 이벤트 콜백

### onReceiveNewInvitation

새로운 초대 요청 수신.

```Objective-C
- (void)onReceiveNewInvitation:(NSString *)identifier
                       inviter:(NSString *)inviter
                           cmd:(NSString *)cmd
                       content:(NSString *)content
NS_SWIFT_NAME(onReceiveNewInvitation(id:inviter:cmd:content:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형    | 의미                                |
| ------- | -------- | ---------------------------------- |
| id      | NSString   | 초대 ID.                          |
| inviter | NSString   | 초대한 사용자 ID.                  |
| cmd     | NSString   | 서비스 지정 명령어. 개발자가 사용자 정의함. |
| content | NSString | 서비스에서 지정한 내용.                   |

### onInviteeAccepted

초대된 사용자가 초대 수락.

```Objective-C
- (void)onInviteeAccepted:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeAccepted(id:invitee:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미                 |
| ------- | ------ | ------------------- |
| id      | NSString | 초대 ID.           |
| invitee | NSString | 초대된 사용자 ID. |

### onInviteeRejected

초대된 사용자가 초대 거부.

```Objective-C
- (void)onInviteeRejected:(NSString *)identifier
                  invitee:(NSString *)invitee
NS_SWIFT_NAME(onInviteeRejected(id:invitee:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미                 |
| ------- | ------ | ------------------- |
| id      | NSString | 초대 ID.           |
| invitee | NSString | 초대된 사용자 ID. |

### onInvitationCancelled

초대한 사용자가 초대 취소.

```Objective-C
- (void)onInvitationCancelled:(NSString *)identifier
                      invitee:(NSString *)invitee NS_SWIFT_NAME(onInvitationCancelled(id:invitee:));
```

매개변수 리스트는 다음과 같습니다.

| 매개변수    | 유형   | 의미                |
| ------- | ------ | ----------------- |
| id      | NSString | 초대 ID.         |
| inviter | NSString | 초대한 사용자 ID.|
