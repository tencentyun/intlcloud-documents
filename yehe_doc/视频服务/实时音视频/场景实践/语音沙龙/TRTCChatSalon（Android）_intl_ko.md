TRTCChatSalon은 Tencent Cloud의 TRTC와 IM 서비스를 기반으로 구성된 모듈이며, 다음 기능을 지원합니다.

- 호스트가 신규 음성 살롱을 생성하면 시청자가 음성 살롱에 입장해 시청 및 인터랙션할 수 있습니다.
- 호스트가 시청자에게 마이크 켜기를 초대하거나 마이크가 켜진 사용자의 마이크를 강제로 끌 수 있습니다.
- 시청자가 마이크 켜기를 신청하여 마이크가 켜진 호스트가 될 수 있고, 다른 사람들과 음성으로 인터랙션할 수 있으며, 언제든지 마이크를 끄고 일반 시청자가 될 수 있습니다.
- 다양한 텍스트 메시지 및 사용자 정의 메시지를 지원합니다. 사용자 정의 메시지를 이용해 댓글 자막, 좋아요, 선물 기능 등을 구현할 수 있습니다.

TRTCChatSalon은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [음성 살롱(Android)](https://intl.cloud.tencent.com/document/product/647/53537)을 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)를 저딜레이 음성 채팅 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 AVChatroom을 이용해 채팅방 기능을 구현하며, IM 속성 인터페이스를 통해 마이크 위치 리스트 등 방 정보를 저장하고 초대 신호를 마이크 켜기/끄기 신청에 사용할 수 있습니다.

[](id:TRTCChatSalon)

## TRTCChatSalon API 개요

### SDK 기본 함수

| API                                             | 설명                     |
| ----------------------------------------------- | ------------------------ |
| [sharedInstance](#sharedinstance)               | 단일 항목 객체 획득           |
| [destroySharedInstance](#destroysharedinstance) | 단일 항목 객체 폐기           |
| [setDelegate](#setdelegate)                     | 이벤트 콜백 설정           |
| [setDelegateHandler](#setdelegatehandler)       | 이벤트 콜백이 존재하는 스레드 설정 |
| [login](#login)                                 | 로그인                   |
| [logout](#logout)                               | 로그아웃                   |
| [setSelfProfile](#setselfprofile)               | 개인 정보 수정           |

### 방 관련 인터페이스 함수

| API                                 | 설명                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)           | 방 생성(호스트 호출), 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방 생성 |
| [destroyRoom](#destroyroom)         | 방 폐기(호스트 호출)                                       |
| [enterRoom](#enterroom)             | 방 입장(시청자 호출)                                       |
| [exitRoom](#exitroom)               | 방 퇴장(시청자 호출)                                       |
| [getRoomInfoList](#getroominfolist) | 방 리스트의 세부 정보 획득                                     |
| [getUserInfoList](#getuserinfolist) | 지정 userId의 사용자 정보 획득, null인 경우 방 안에 있는 모든 사용자 정보 획득 |

### 마이크 켜기/끄기 인터페이스

| API                     | 설명                               |
| ----------------------- | ---------------------------------- |
| [enterSeat](#enterseat) | 직접 마이크 켜기(시청자와 호스트 모두 호출 가능) |
| [leaveSeat](#leaveseat) | 직접 마이크 끄기(시청자와 호스트 모두 호출 가능) |
| [pickSeat](#pickseat)   | 특정 사용자 마이크 켜기(호스트 호출)             |
| [kickSeat](#kickseat)   | 특정 사용자 마이크 끄기(호스트 호출)             |

### 로컬 오디오 작업 인터페이스

| API                                             | 설명                 |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | 마이크 수집 시작     |
| [stopMicrophone](#stopmicrophone)               | 마이크 수집 중지     |
| [setAudioQuality](#setaudioquality)             | 오디오 품질 설정           |
| [muteLocalAudio](#mutelocalaudio)               | 로컬 음소거 활성화/비활성화  |
| [setSpeaker](#setspeaker)                       | 스피커 활성화 설정     |
| [setAudioCaptureVolume](#setaudiocapturevolume) | 마이크 수집 음량 설정 |
| [setAudioPlayoutVolume](#setaudioplayoutvolume) | 재생 음량 설정       |


### 원격 사용자 오디오 작업 인터페이스

| API                                       | 설명                    |
| ----------------------------------------- | ----------------------- |
| [muteRemoteAudio](#muteremoteaudio)       | 지정 사용자 음소거/음소거 해제 |
| [muteAllRemoteAudio](#muteallremoteaudio) | 모든 사용자 음소거/음소거 해제 |

### 배경 음악 음향 효과 관련 인터페이스

| API                                             | 설명                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [getAudioEffectManager](#getaudioeffectmanager) | 배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득 |

### 메시지 발송 관련 인터페이스

| API                                     | 설명                                     |
| --------------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg)     | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용 |
| [sendRoomCustomMsg](#sendroomcustommsg) | 사용자 정의 텍스트 메시지 발송                     |

### 초대 신호 관련 인터페이스

| API                                   | 설명             |
| ------------------------------------- | ---------------- |
| [sendInvitation](#sendinvitation)     | 사용자에게 초대 발송 |
| [acceptInvitation](#acceptinvitation) | 초대 수락       |
| [rejectInvitation](#rejectinvitation) | 초대 거부       |
| [cancelInvitation](#cancelinvitation) | 초대 취소       |

[](id:TRTCChatSalonDelegate)
## TRTCChatSalonDelegate API 개요

### 일반적인 이벤트 콜백

| API                       | 설명       |
| ------------------------- | ---------- |
| [onError](#onerror)       | 오류 콜백 |
| [onWarning](#onwarning)   | 경고 콜백 |
| [onDebugLog](#ondebuglog) | Log 콜백 |

### 방 이벤트 콜백

| API                                       | 설명                       |
| ----------------------------------------- | -------------------------- |
| [onRoomDestroy](#onroomdestroy)           | 방 폐기 콜백         |
| [onRoomInfoChange](#onroominfochange)     | 음성 살롱 방 정보 변경 콜백 |
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 음량 콜백         |

### 마이크 위치 변경 콜백

| API                                            | 설명                                   |
| ---------------------------------------------- | -------------------------------------- |
| [onAnchorEnterSeat](#onanchorenterseat)        | 사용자 마이크 켜짐(직접 마이크 켬/호스트가 특정 사용자 마이크 켬)  |
| [onAnchorLeaveSeat](#onanchorleaveseat)        | 사용자 마이크 꺼짐(직접 마이크 끔/호스트가 특정 사용자 마이크 끔)  |
| [onSeatMute](#onseatmute)                      | 호스트 마이크 음소거                             |

### 시청자 입장/퇴장 이벤트 콜백

| API                                 | 설명               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 공지 수신 |
| [onAudienceExit](#onaudienceexit)   | 시청자 퇴장 공지 수신 |

### 메시지 이벤트 콜백

| API                                         | 설명             |
| ------------------------------------------- | ---------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg)     | 텍스트 메시지 수신   |
| [onRecvRoomCustomMsg](#onrecvroomcustommsg) | 사용자 정의 메시지 수신 |

## 신호 이벤트 콜백

| API                                               | 설명               |
| ------------------------------------------------- | ------------------ |
| [onReceiveNewInvitation](#onreceivenewinvitation) | 새로운 초대 요청 수신 |
| [onInviteeAccepted](#oninviteeaccepted)           | 초대된 사용자가 초대 수락 |
| [onInviteeRejected](#oninviteerejected)           | 초대된 사용자가 초대 거부 |
| [onInvitationCancelled](#oninvitationcancelled)   | 초대한 사용자가 초대 취소   |

## SDK 기본 함수

### sharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537) 단일 항목 객체 획득

```java
 public static synchronized TRTCChatSalon sharedInstance(Context context);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형    | 의미                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| context | Context | Android 컨텍스트, 내부가 ApplicationContext로 전환되어 시스템 API 호출에 사용 |


### destroySharedInstance

[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537) 단일 항목 객체 폐기

>?인스턴스 폐기 후에는 외부에 캐시된 TRTCChatSalon 인스턴스를 다시 사용할 수 없으며, [sharedInstance](#sharedinstance)를 재호출해 새로운 인스턴스를 획득해야 합니다.

```java
public static void destroySharedInstance();
```

### setDelegate
[TRTCChatSalon](https://intl.cloud.tencent.com/document/product/647/53537) 이벤트 콜백은 TRTCChatSalonDelegate를 통해 [TRTCChatSalon](https://cloud.tencent.com/document/product/647/53537)의 다양한 상태 공지를 받아볼 수 있습니다.

```java
public abstract void setDelegate(TRTCChatSalonDelegate delegate);
```

>?setDelegate는 TRTCChatSalon의 프록시 콜백입니다.   

### setDelegateHandler
이벤트 콜백이 존재하는 스레드를 설정합니다.

```java
public abstract void setDelegateHandler(Handler handler);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형    | 의미                                                         |
| ------- | ------- | ------------------------------------------------------------ |
| handler | Handler | TRTCChatSalon의 각종 상태 공지를 지정한 handler 스레드에 배포합니다. |

   

### login

로그인

```java
public abstract void login(int sdkAppId,
 String userId, String userSig,
TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppId | int            | TRTC 콘솔>[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | String         | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |
| callback | ActionCallback | 로그인 콜백이며, 성공 시 code는 0입니다.                                  |

   

### logout

로그아웃

```java
public abstract void logout(TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                        |
| -------- | -------------- | --------------------------- |
| callback | ActionCallback | 로그아웃 콜백이며, 성공 시 code는 0입니다. |

   

### setSelfProfile

개인 정보 수정

```java
public abstract void setSelfProfile(String userName, String avatarURL, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형           | 의미                                |
| --------- | -------------- | ----------------------------------- |
| userName  | String         | 닉네임                              |
| avatarURL | String         | 프로필 사진 주소                          |
| callback  | ActionCallback | 개인 정보 설정 콜백이며, 성공 시 code는 0입니다. |

   


## 방 관련 인터페이스 함수

### createRoom

방 생성(호스트 호출)

```java
public abstract void createRoom(int roomId, TRTCChatSalonDef.RoomParam roomParam, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형           | 의미                                                         |
| --------- | -------------- | ------------------------------------------------------------ |
| roomId    | int            | 방 식별 번호입니다. 사용자가 할당하고 통합 관리해야 하며, 여러 개의 roomID를 1개의 음성 살롱 방 리스트로 통합할 수 있습니다. Tencent Cloud는 현재 음성 살롱 방 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | RoomParam      | 방 정보입니다. 방 이름, 마이크 위치 정보, 썸네일 정보 등 방을 설명하는 데 사용됩니다. |
| callback  | ActionCallback | 방 생성 결과 콜백이며, 성공 시 code는 0입니다.                        |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 

1. 호스트가 `createRoom`을 호출하여 새로운 음성 살롱을 생성합니다. 이때 방 ID, 마이크를 켤 때 방장 확인 필요 여부 등 방 속성 정보를 전송합니다.
2. 호스트가 방 생성 후 `enterSeat`를 호출하여 자리에 입장합니다.
3. 호스트는 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterSeat` 이벤트 공지도 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

   

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```java
public abstract void destroyRoom(TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 폐기 결과 콜백이며, 성공 시 code는 0입니다. |


### enterRoom

방 입장(시청자 호출)

```java
public abstract void enterRoom(int roomId, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| roomId   | int            | 방 식별 번호                            |
| callback | ActionCallback | 방 입장 결과 콜백이며, 성공 시 code는 0입니다. |


시청자가 방에 입장하여 시청하는 정상적인 호출 프로세스는 다음과 같습니다. 

1. 시청자는 서버에서 최신 음성 살롱 리스트를 획득하며, 여기에는 여러 음성 살롱 방의 roomId 및 방 정보가 포함될 수 있습니다.
2. 시청자가 음성 살롱 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
3. 방 입장 후 모듈의 `onRoomInfoChange` 방 속성 변경 이벤트 공지를 수신합니다. 이때 UI에 방 이름 표시, 마이크를 켤 때 호스트에게 동의 요청 필요 여부 등 방의 속성을 기록할 수 있으며 그에 해당하는 변경이 가능합니다.
4. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterSeat` 이벤트 공지도 수신합니다.

### exitRoom

방 퇴장

```java
public abstract void exitRoom(TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                  |
| -------- | -------------- | ------------------------------------- |
| callback | ActionCallback | 방 퇴장 결과 콜백이며, 성공 시 code는 0입니다. |

   

### getRoomInfoList

방 리스트 세부 정보 획득. 방 이름, 방 썸네일은 호스트가 `createRoom()` 생성 시 roomInfo를 통해 설정한 정보입니다.

>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```java
public abstract void getRoomInfoList(List<Integer> roomIdList, TRTCChatSalonCallback.RoomInfoCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형                | 의미               |
| ---------- | ------------------- | ------------------ |
| roomIdList | List&lt;Integer&gt; | 방 번호 리스트       |
| callback   | RoomInfoCallback    | 방 세부 정보 콜백 |


### getUserInfoList

지정 userId의 사용자 정보 획득

```java
public abstract void getUserInfoList(List<String> userIdList, TRTCChatSalonCallback.UserListCallback userlistcallback);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형               | 의미                                                         |
| ---------------- | ------------------ | ------------------------------------------------------------ |
| userIdList       | List&lt;String&gt; | 획득해야 할 사용자 ID 리스트입니다. null인 경우 방 안에 있는 모든 사용자 정보를 획득합니다. |
| userlistcallback | UserListCallback   | 사용자 세부 정보 콜백                                           |


## 마이크 켜기/끄기 인터페이스

### enterSeat

직접 마이크 켜기(시청자와 호스트 모두 호출 가능)

>?마이크가 켜진 후, 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 공지를 수신합니다.

```java
public abstract void enterSeat(TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 작업 콜백 |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 시청자가 호스트에게 신청해야 하는 시나리오의 경우, 먼저 `sendInvitation`을 호출해 호스트에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.

### leaveSeat

직접 마이크 끄기(시청자와 호스트 모두 호출 가능)

>? 마이크가 꺼진 후, 방 안에 있는 모든 사용자가 `onAnchorLeaveSeat` 이벤트 공지를 수신합니다.

```java
public abstract void leaveSeat(TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| callback | ActionCallback | 작업 콜백 |

### pickSeat

특정 사용자 마이크 켜기(호스트 호출)

>? 호스트가 특정 사용자의 마이크를 켜면 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 공지를 수신합니다.

```java
public abstract void pickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미       |
| -------- | -------------- | ---------- |
| userId   | String         | 사용자 ID  |
| callback | ActionCallback | 작업 콜백 |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 호스트가 시청자에게 동의를 얻어야만 마이크를 켤 수 있는 시나리오의 경우, 먼저 `sendInvitation`을 호출하여 시청자에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.


### kickSeat

특정 사용자 마이크 끄기(호스트 호출)

>? 호스트가 특정 사용자의 마이크를 끄면 방 안에 있는 모든 사용자가 `onAnchorLeaveSeat` 이벤트 공지를 수신합니다.

```java
public abstract void kickSeat(String userId, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                 |
| -------- | -------------- | -------------------- |
| userId   | String         | 마이크를 끌 사용자 id |
| callback | ActionCallback | 작업 콜백           |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 호스트가 시청자에게 동의를 얻어야만 마이크를 켤 수 있는 시나리오의 경우, 먼저 `sendInvitation`을 호출하여 시청자에게 신청하고 `onInvitationAccept` 수신 후 다시 해당 함수를 호출합니다.


## 로컬 오디오 작업 인터페이스

### startMicrophone

마이크 수집 시작

```java
public abstract void startMicrophone();
```

### stopMicrophone

마이크 수집 중지

```java
public abstract void stopMicrophone();
```

### setAudioQuality

오디오 품질 설정

```java
public abstract void setAudioQuality(int quality);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형 | 의미                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 오디오의 품질입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참조하십시오. |


### muteLocalAudio

로컬 오디오 음소거/음소거 취소

```java
public abstract void muteLocalAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | 오디오를 음소거/음소거 취소합니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)를 참조하십시오. |



### setSpeaker

스피커 활성화 설정

```java
public abstract void setSpeaker(boolean useSpeaker);
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형    | 의미                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true: 스피커, false: 헤드셋 |



### setAudioCaptureVolume

마이크 수집 음량 설정

```java
public abstract void setAudioCaptureVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 수집 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |


### setAudioPlayoutVolume

재생 음량 설정

```java
public abstract void setAudioPlayoutVolume(int volume);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 재생 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |

### muteRemoteAudio

지정 사용자 음소거/음소거 해제

```java
public abstract void muteRemoteAudio(String userId, boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                              |
| ------ | ------- | --------------------------------- |
| userId | String  | 지정 사용자 ID                   |
| mute   | boolean | true: 음소거, false: 음소거 해제 |

### muteAllRemoteAudio

모든 사용자 음소거/음소거 해제

```java
public abstract void muteAllRemoteAudio(boolean mute);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true: 음소거, false: 음소거 해제 |

   

## 배경 음악 음향 효과 관련 인터페이스 함수

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득

```java
public abstract TXAudioEffectManager getAudioEffectManager();
```


## 메시지 발송 관련 인터페이스 함수

### sendRoomTextMsg

방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용

```java
public abstract void sendRoomTextMsg(String message, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미           |
| -------- | -------------- | -------------- |
| message  | String         | 텍스트 메시지     |
| callback | ActionCallback | 발송 결과 콜백 |

   

### sendRoomCustomMsg

사용자 정의 텍스트 메시지 발송

```java
public abstract void sendRoomCustomMsg(String cmd, String message, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                               |
| -------- | -------------- | -------------------------------------------------- |
| cmd      | String         | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String         | 텍스트 메시지                                         |
| callback | ActionCallback | 발송 결과 콜백                                     |

   

## 초대 신호 관련 인터페이스

### sendInvitation

사용자에게 초대 발송

```java
public abstract String sendInvitation(String cmd, String userId, String content, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미             |
| -------- | -------------- | ---------------- |
| cmd      | String         | 서비스의 사용자 정의 명령 |
| userId   | String         | 초대한 사용자 ID  |
| content  | String         | 초대 내용     |
| callback | ActionCallback | 발송 결과 콜백   |

반환값:

| 반환값   | 유형   | 의미                  |
| -------- | ------ | --------------------- |
| inviteId | String | 해당 초대 ID를 식별하는 데 사용 |

### acceptInvitation

초대 수락

```java
public abstract void acceptInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미           |
| -------- | -------------- | -------------- |
| id       | String         | 초대 ID      |
| callback | ActionCallback | 발송 결과 콜백 |

### rejectInvitation

초대 거부

```java
public abstract void rejectInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미           |
| -------- | -------------- | -------------- |
| id       | String         | 초대 ID      |
| callback | ActionCallback | 발송 결과 콜백 |


### cancelInvitation

초대 취소

```java
public abstract void cancelInvitation(String id, TRTCChatSalonCallback.ActionCallback callback);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미           |
| -------- | -------------- | -------------- |
| id       | String         | 초대 ID      |
| callback | ActionCallback | 발송 결과 콜백 |

## TRTCChatSalonDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백

>? SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 적절한 인터페이스로 사용자에게 안내해야 합니다.

```java
void onError(int code, String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| code    | int    | 에러 코드   |
| message | String | 오류 정보 |


### onWarning

경고 콜백

```java
void onWarning(int code, String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| code    | int    | 에러 코드   |
| message | String | 경고 정보 |

   

### onDebugLog

Log 콜백

```java
void onDebugLog(String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| message | String | 로그 정보 |

   


## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백. 호스트가 방을 종료하면 방 안에 있는 모든 사용자는 해당 공지를 받게 됩니다.

```java
void onRoomDestroy(String roomId);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미      |
| ------ | ------ | --------- |
| roomId | String | 방 ID |


### onRoomInfoChange

방 입장 후 해당 인터페이스를 콜백합니다. roomInfo의 정보는 방 생성 시의 정보입니다.

```java
void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미       |
| -------- | -------- | ---------- |
| roomInfo | RoomInfo | 방 정보 |

   

### onUserVolumeUpdate

음량 크기 알림을 활성화하여 모든 참여자의 음량 크기를 공지합니다.

```java
void onUserVolumeUpdate(String userId, int volume);

```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                      |
| ------ | ------ | ------------------------- |
| userId | String | 사용자 ID                 |
| volume | int    | 음량 크기이며, 0~100으로 설정할 수 있습니다. |


## 마이크 위치 콜백

### onAnchorEnterSeat

사용자 마이크 켜짐(직접 마이크 켬/호스트가 특정 사용자 마이크 켬)

```java
void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형     | 의미                 |
| ---- | -------- | -------------------- |
| user | UserInfo | 마이크가 켜진 사용자의 세부 정보 |

### onAnchorLeaveSeat

사용자 마이크 꺼짐(직접 마이크 끔/호스트가 특정 사용자 마이크 끔)

```java
void onAnchorLeaveSeat(TRTCChatSalonDef.UserInfo user);
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형     | 의미                 |
| ---- | -------- | -------------------- |
| user | UserInfo | 마이크가 켜진 사용자의 세부 정보 |


### onSeatMute

호스트 마이크 음소거

```java
void onSeatMute(String userId, boolean isMute);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                               |
| ------ | ------- | ---------------------------------- |
| userId  | String     | 마이크 위치의 사용자 id                       |
| isMute | boolean | true: 음소거, false: 음소거 해제 |



## 시청자 입장/퇴장 이벤트 콜백

### onAudienceEnter

시청자 방 입장 공지 수신

```java
void onAudienceEnter(TRTCChatSalonDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 입장한 시청자 정보 |

### onAudienceExit

시청자 방 퇴장 공지 수신

```java
void onAudienceExit(TRTCChatSalonDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미           |
| -------- | -------- | -------------- |
| userInfo | UserInfo | 퇴장한 시청자 정보 |

   

## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지 수신

```java
void onRecvRoomTextMsg(String message, TRTCChatSalonDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미             |
| -------- | -------- | ---------------- |
| message  | String   | 텍스트 메시지       |
| userInfo | UserInfo | 발신자 정보 |

   

### onRecvRoomCustomMsg

사용자 정의 메시지 수신

```java
void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형     | 의미                                               |
| -------- | -------- | -------------------------------------------------- |
| command  | String   | 명령어로, 개발자가 사용자 정의할 수 있으며 주로 서로 다른 메시지 유형을 구분하는 데 사용합니다. |
| message  | String   | 텍스트 메시지                                         |
| userInfo | UserInfo | 발신자 정보                                   |

## 초대 신호 이벤트 콜백

### onReceiveNewInvitation

새로운 초대 요청 수신

```java
void onReceiveNewInvitation(String id, String inviter, String cmd, String content);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형     | 의미                               |
| ------- | -------- | ---------------------------------- |
| id      | String   | 초대 ID                          |
| inviter | String   | 초대한 사용자 ID                  |
| cmd     | String   | 서비스에서 지정한 명령어, 개발자가 사용자 정의 |
| content | UserInfo | 서비스에서 지정한 내용                   |

### onInviteeAccepted

초대된 사용자가 초대 수락

```java
void onInviteeAccepted(String id, String invitee);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                |
| ------- | ------ | ------------------- |
| id      | String | 초대 ID           |
| invitee | String | 초대된 사용자 ID |

### onInviteeRejected

초대된 사용자가 초대 거부

```java
void onInviteeRejected(String id, String invitee);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                |
| ------- | ------ | ------------------- |
| id      | String | 초대 ID           |
| invitee | String | 초대된 사용자 ID |

### onInvitationCancelled

초대한 사용자가 초대 취소

```java
void onInvitationCancelled(String id, String inviter);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미              |
| ------- | ------ | ----------------- |
| id      | String | 초대 ID         |
| inviter | String | 초대한 사용자 ID |

### onInvitationTimeout

초대 타임아웃

```java
void onInvitationTimeout(String id);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미              |
| ------- | ------ | ----------------- |
| id      | String | 초대 ID         |
