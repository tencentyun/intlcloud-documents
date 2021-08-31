TRTCChatSalon은 Tencent Cloud의 TRTC와 IM 서비스를 기반으로 구성된 모듈이며, 다음 기능을 지원합니다.

- 호스트가 신규 음성 살롱을 생성하면 시청자가 음성 살롱에 입장해 시청 및 인터랙션할 수 있습니다.
- 호스트가 시청자의 마이크 켜기에 동의하거나 마이크가 켜진 사용자의 마이크를 강제로 끌 수 있습니다.
- 시청자가 마이크 켜기를 신청하여 마이크가 켜진 호스트가 될 수 있고, 다른 사람들과 음성으로 인터랙션할 수 있으며, 언제든지 마이크를 끄고 일반 시청자가 될 수 있습니다.
- 다양한 텍스트 메시지 발송을 지원합니다.

TRTCChatSalon은 오픈 소스 Class로, Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [음성 살롱(Flutter)](https://cintl.loud.tencent.com/document/product/647/53582)을 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/zh/document/product/647)를 저딜레이 음성 채팅 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)의 AVChatroom을 이용해 채팅방 기능을 구현하며, IM 속성 인터페이스를 통해 마이크 위치 리스트 등 방 정보를 저장하고 초대 신호를 마이크 켜기/끄기 신청에 사용할 수 있습니다.

[](id:TRTCChatSalon)

## TRTCChatSalon API 개요

### SDK 기본 함수

| API                                             | 설명           |
| ----------------------------------------------- | -------------- |
| [sharedInstance](#sharedinstance)               | 단일 항목 객체 획득 |
| [destroySharedInstance](#destroysharedinstance) | 단일 항목 객체 폐기 |
| [registerListener](#registerlistener)           | 이벤트 수신 설정 |
| [unRegisterListener](#unregisterlistener)       | 이벤트 수신 폐기 |
| [login](#login)                                 | 로그인         |
| [logout](#logout)                               | 로그아웃         |
| [setSelfProfile](#setselfprofile)               | 개인 정보 수정 |

### 방 관련 인터페이스 함수

| API                                     | 설명                                                         |
| --------------------------------------- | ------------------------------------------------------------ |
| [createRoom](#createroom)               | 방 생성(호스트 호출), 방이 존재하지 않는 경우 시스템에서 자동으로 새로운 방 생성 |
| [destroyRoom](#destroyroom)             | 방 폐기(호스트 호출)                                       |
| [enterRoom](#enterroom)                 | 방 입장(시청자 호출)                                       |
| [exitRoom](#exitroom)                   | 방 퇴장(시청자 호출)                                       |
| [getRoomInfoList](#getroominfolist)     | 방 리스트의 세부 정보 획득                                     |
| [getRoomMemberList](#getroommemberlist) | 방 안에 있는 모든 사용자 정보 획득                                     |
| [getArchorInfoList](#getarchorInfolist) | 방 호스트 리스트 획득                                           |
| [getUserInfoList](#getuserinfolist)     | 지정 userId의 사용자 정보 획득                                 |

### 마이크 켜기/끄기 인터페이스

| API                   | 설명                                |
| --------------------- | ----------------------------------- |
| [enterMic](#entermic) | 시청자 마이크 켜기                          |
| [leaveMic](#leavemic) | 호스트 마이크 끄기                          |
| [muteMic](#mutemic)   | 특정 마이크 위치 음소거/음소거 해제(호스트 호출) |
| [kickMic](#kickmic)   | 특정 사용자 마이크 끄기(호스트 호출)              |

### 로컬 오디오 작업 인터페이스

| API                                             | 설명                 |
| ----------------------------------------------- | -------------------- |
| [startMicrophone](#startmicrophone)             | 마이크 수집 시작     |
| [stopMicrophone](#stopmicrophone)               | 마이크 수집 중지     |
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

| API                                 | 설명                                     |
| ----------------------------------- | ---------------------------------------- |
| [sendRoomTextMsg](#sendroomtextmsg) | 방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용 |

### 마이크 켜기 신청 신호 관련 인터페이스

| API                             | 설명           |
| ------------------------------- | -------------- |
| [raiseHand](#raisehand)         | 시청자가 마이크 켜기 신청 |
| [agreeToSpeak](#agreetospeak)   | 호스트가 마이크 켜기 동의 |
| [refuseToSpeak](#refusetospeak) | 호스트가 마이크 켜기 거부 |

[](id:TRTCChatSalonDelegate)
## TRTCChatSalonDelegate API 개요

### 일반적인 이벤트 콜백

| API                                 | 설명       |
| ----------------------------------- | ---------- |
| [onError](#onerror)                 | 오류 콜백 |
| [onWarning](#onwarning)             | 경고 콜백 |
| [onKickedOffline](#onkickedoffline) | 경고 콜백 |

### 방 이벤트 콜백

| API                                       | 설명                     |
| ----------------------------------------- | ------------------------ |
| [onRoomDestroy](#onroomdestroy)           | 방 폐기 콜백       |
| [onAnchorListChange](#onanchorlistchange) | 호스트 리스트 정보 변경 콜백 |
| [onUserVolumeUpdate](#onuservolumeupdate) | 사용자 통화 음량 콜백       |

### 마이크 위치 변경 콜백

| API                                   | 설명                                  |
| ------------------------------------- | ------------------------------------- |
| [onAnchorEnterMic](#onanchorentermic) | 사용자 마이크 켜짐(직접 마이크 켬/호스트가 특정 사용자 마이크 켬) |
| [onAnchorLeaveMic](#onanchorleavemic) | 사용자 마이크 꺼짐(직접 마이크 끔/호스트가 특정 사용자 마이크 끔) |
| [onMicMute](#onmicmute)               | 호스트 마이크 음소거                            |

### 시청자 입장/퇴장 이벤트 콜백

| API                                 | 설명               |
| ----------------------------------- | ------------------ |
| [onAudienceEnter](#onaudienceenter) | 시청자 입장 공지 수신 |
| [onAudienceExit](#onaudienceexit)   | 시청자 퇴장 공지 수신 |

### 메시지 이벤트 콜백

| API                                     | 설명           |
| --------------------------------------- | -------------- |
| [onRecvRoomTextMsg](#onrecvroomtextmsg) | 텍스트 메시지 수신 |

## 마이크 켜기 신청 신호 이벤트 콜백

| API                                    | 설명                                     |
| -------------------------------------- | ---------------------------------------- |
| [onRaiseHand](#onraisehand) | 시청자가 손 들기로 마이크 켜기 신청                   |
| [onAgreeToSpeak](#onagreetospeak)   | 시청자가 손 들기 신청 후, 호스트의 동의 콜백 수신 |
| [onRefuseToSpeak](#onrefusetospeak)    | 시청자가 손 들기 신청 후, 호스트의 거부 콜백 수신     |

## SDK 기본 함수

### sharedInstance

TRTCChatSalon 단일 항목 객체 획득

```dart
 static Future<TRTCChatSalon> sharedInstance()
```


### destroySharedInstance

TRTCChatSalon 단일 항목 객체 폐기

>?인스턴스 폐기 후에는 외부에 캐시된 TRTCChatSalon 인스턴스를 다시 사용할 수 없으며, [sharedInstance](#sharedinstance)를 재호출해 새로운 인스턴스를 획득해야 합니다.

```dart
static void destroySharedInstance()
```

### registerListener

이벤트 수신 설정

```
void registerListener(VoiceListenerFunc func)
```

>?setDelegate는 TRTCChatSalon의 프록시 콜백입니다.   

### unRegisterListener

모듈 이벤트 수신 인터페이스 제거

```dart
void unRegisterListener(VoiceListenerFunc func)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형              | 의미                                                      |
| ---- | ----------------- | --------------------------------------------------------- |
| func | VoiceListenerFunc | TRTCChatSalon의 각종 상태 공지를 지정한 func 함수에 배포합니다. |


### login

로그인

```dart
Future<ActionCallback> login(int sdkAppId, String userId, String userSig)
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| sdkAppId | int    | TRTC 콘솔>[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId   | String | 현재 사용자 ID입니다. 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig  | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |


### logout

로그아웃

```dart
Future<ActionCallback> logout()
```

### setSelfProfile

개인 정보 수정

```dart
Future<ActionCallback> setSelfProfile(String userName, String avatarURL)
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미       |
| --------- | ------ | ---------- |
| userName  | String | 닉네임     |
| avatarURL | String | 프로필 사진 주소 |

## 방 관련 인터페이스 함수

### createRoom

방 생성(방 생성 시 호출)

```
Future<ActionCallback> createRoom(int roomId, RoomParam roomParam)
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형      | 의미                                                         |
| --------- | --------- | ------------------------------------------------------------ |
| roomId    | int       | 방 식별 번호입니다. 사용자가 할당하고 통합 관리해야 하며, 여러 개의 roomID를 1개의 음성 살롱 방 리스트로 통합할 수 있습니다. Tencent Cloud는 현재 음성 살롱 방 리스트 관리 서비스를 제공하지 않으므로 직접 관리하시기 바랍니다. |
| roomParam | RoomParam | 방 정보입니다. 방 이름, 썸네일 정보 등 방을 설명하는 데 사용됩니다.     |

호스트의 정상적인 방송 시작 호출 프로세스는 다음과 같습니다. 

1. 호스트가 `createRoom`을 호출하여 새로운 음성 살롱을 생성합니다. 이때 방 ID 등 방 속성 정보를 전송합니다.
2. 호스트는 마이크 위치 리스트에 사용자가 입장할 때 `onAnchorEnterMic` 이벤트 공지도 수신하며, 이때 자동으로 마이크 수집이 활성화됩니다.

### destroyRoom

방 폐기(호스트 호출). 호스트는 방 생성 후 해당 함수를 호출해 방을 폐기할 수 있습니다.

```dart
Future<ActionCallback> destroyRoom()
```


### enterRoom

방 입장(시청자 호출)

```dart
Future<ActionCallback> enterRoom(int roomId)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미       |
| ------ | ---- | ---------- |
| roomId | int  | 방 식별 번호 |


시청자가 방에 입장하여 시청하는 정상적인 호출 프로세스는 다음과 같습니다. 

1. 시청자는 서버에서 최신 음성 살롱 리스트를 획득하며, 여기에는 여러 음성 살롱 방의 roomId 및 방 정보가 포함될 수 있습니다.
2. 시청자가 음성 살롱 1개를 선택하고 `enterRoom`을 호출하여 해당 방으로 입장합니다.
3. 방 입장 후 `getArchorInfoList`를 조회하여 호스트 리스트를 획득할 수 있으며, `getRoomMemberList`에 따라 방 안의 모든 사용자 리스트를 획득하고 호스트 리스트를 제외한 시청자 리스트를 획득할 수 있습니다.
4. 방 입장 후 마이크 위치 리스트에 호스트 입장 `onAnchorEnterMic` 이벤트 공지도 수신합니다.

### exitRoom

방 퇴장

```dart
Future<ActionCallback> exitRoom()
```

### getRoomInfoList

방 리스트 세부 정보 획득. 방 이름, 방 썸네일은 호스트가 `createRoom()` 생성 시 roomInfo를 통해 설정한 정보입니다.

>?방 리스트 및 방 정보를 모두 직접 관리하는 경우 해당 함수는 생략할 수 있습니다.


```dart
Future<RoomInfoCallback> getRoomInfoList(List<String> roomIdList)
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형                | 의미         |
| ---------- | ------------------- | ------------ |
| roomIdList | List&lt;Integer&gt; | 방 번호 리스트 |


### getRoomMemberList

방 안의 모든 참여자 리스트를 획득합니다.

>?IM 라이브 방송 채팅 그룹은 기본적으로 최근 31명의 참여자 리스트만 풀링할 수 있습니다.


```dart
Future<MemberListCallback> getRoomMemberList(double nextSeq)
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미                                                         |
| ------- | ------ | ------------------------------------------------------------ |
| nextSeq | double | 페이징 풀링 식별 값입니다. 최초 풀링 시 0을 입력하고 콜백 성공 후의 nextSeq가 0이 아닌 경우, 0이 될 때까지 페이징 후 풀링해야 합니다. |

### getArchorInfoList

방 호스트 리스트 획득

```dart
Future<UserListCallback> getArchorInfoList()
```


### getUserInfoList

지정 userId의 사용자 정보 획득

```dart
Future<UserListCallback> getUserInfoList(List<String> userIdList)
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형               | 의미                                                         |
| ---------- | ------------------ | ------------------------------------------------------------ |
| userIdList | List&lt;String&gt; | 획득해야 할 사용자 ID 리스트입니다. null인 경우 방 안에 있는 모든 사용자 정보를 획득합니다. |


## 마이크 켜기/끄기 인터페이스

### enterMic

마이크 켜기(시청자와 호스트 모두 호출 가능)

>?마이크가 켜진 후, 방 안에 있는 모든 사용자가 `onAnchorEnterSeat` 이벤트 공지를 수신합니다.

```
Future<ActionCallback> enterMic();
```

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다. 시청자가 먼저 `raiseHand`를 호출해 호스트에게 신청해야 하며, `onAgreeToSpeak` 수신 후 다시 해당 함수를 호출합니다.

### leaveMic

직접 마이크 끄기

>? 마이크가 꺼진 후, 방 안에 있는 모든 사용자가 `onAnchorLeaveMic` 이벤트 공지를 수신합니다.

```dart
Future<ActionCallback> leaveMic()
```

### muteMic

특정 마이크 위치 음소거/음소거 해제(호스트 호출)

>? 마이크 위치의 상태가 변경된 후, 방 안에 있는 모든 사용자가 `onAnchorListChange` 및 `onMicMute` 이벤트 공지를 수신합니다.

```dart
Future<ActionCallback> muteMic(bool mute)
```

### kickMic

특정 사용자 마이크 끄기(호스트 호출)

>? 호스트가 특정 사용자의 마이크를 끄면 방 안에 있는 모든 사용자가 `onAnchorLeaveMic` 이벤트 공지를 수신합니다.

```dart
Future<ActionCallback> kickMic(String userId)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                 |
| ------ | ------ | -------------------- |
| userId | String | 마이크를 끌 사용자 ID |

해당 인터페이스를 호출하면 마이크 위치 리스트가 즉시 수정됩니다.


## 로컬 오디오 작업 인터페이스

### startMicrophone

마이크 수집 시작

```dart
void startMicrophone(int quality)
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형 | 의미                                                         |
| ------- | ---- | ------------------------------------------------------------ |
| quality | int  | 오디오의 품질입니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a955cccaddccb0c993351c656067bee55)를 참조하십시오. |

### stopMicrophone

마이크 수집 중지

```dart
void stopMicrophone()
```

### muteLocalAudio

로컬 오디오 음소거/음소거 취소

```dart
void muteLocalAudio(bool mute)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                                                         |
| ---- | ------- | ------------------------------------------------------------ |
| mute | boolean | 오디오를 음소거/음소거 취소합니다. 자세한 내용은 [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a37f52481d24fa0f50842d3d8cc380d86)를 참조하십시오. |


### setSpeaker

스피커 활성화 설정

```dart
void setSpeaker(bool useSpeaker)
```

매개변수는 다음과 같습니다.

| 매개변수       | 유형    | 의미                        |
| ---------- | ------- | --------------------------- |
| useSpeaker | boolean | true: 스피커, false: 헤드셋 |



### setAudioCaptureVolume

마이크 수집 음량 설정

```dart
void setAudioCaptureVolume(int volume)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 수집 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |


### setAudioPlayoutVolume

재생 음량 설정

```dart
void setAudioPlayoutVolume(int volume)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                          |
| ------ | ---- | ----------------------------- |
| volume | int  | 재생 음량으로, 0~100으로 설정할 수 있으며 기본값은 100입니다. |

### muteRemoteAudio

지정 사용자 음소거/음소거 해제

```dart
void muteRemoteAudio(String userId, bool mute)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                              |
| ------ | ------- | --------------------------------- |
| userId | String  | 지정 사용자 ID                   |
| mute   | boolean | true: 음소거, false: 음소거 해제 |

### muteAllRemoteAudio

모든 사용자 음소거/음소거 해제

```dart
void muteAllRemoteAudio(bool mute)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미                              |
| ---- | ------- | --------------------------------- |
| mute | boolean | true: 음소거, false: 음소거 해제 |


## 배경 음악 음향 효과 관련 인터페이스 함수

### getAudioEffectManager

배경 음악 음향 효과 관리 객체 [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a3646dad993287c3a1a38a5bc0e6e33aa) 획득

```dart
TXAudioEffectManager getAudioEffectManager()
```


## 메시지 발송 관련 인터페이스 함수

### sendRoomTextMsg

방 안에서 텍스트 메시지 발송, 일반적으로 댓글 자막 채팅에 사용

```dart
Future<ActionCallback> sendRoomTextMsg(String message)
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형   | 의미       |
| ------- | ------ | ---------- |
| message | String | 텍스트 메시지 |

   

## 마이크 켜기 신청 신호 관련 인터페이스

### raiseHand

시청자가 마이크 켜기 신청

```dart
void raiseHand()
```

### agreeToSpeak

호스트가 마이크 켜기 동의

```dart
Future<ActionCallback> agreeToSpeak(String userId)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미     |
| ------ | ------ | -------- |
| userId | String | 사용자 ID |

### refuseToSpeak

호스트가 사용자의 마이크 켜기 거부

```dart
Future<ActionCallback> refuseToSpeak(String userId)
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미     |
| ------ | ------ | -------- |
| userId | String | 사용자 ID |


## TRTCChatSalonDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백

>? SDK가 복구할 수 없는 오류는 반드시 수신하고 상황에 따라 적절한 인터페이스로 사용자에게 안내해야 합니다.


매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미                                                     |
| --------- | ------ | -------------------------------------------------------- |
| errCode   | int    | 에러 코드                                                 |
| errMsg    | String | 오류 정보                                               |
| extraInfo | String | 확장 정보 필드. 각각의 에러 코드에 포함된 추가 정보로 문제를 파악할 수 있습니다.  |

### onWarning

경고 콜백

매개변수는 다음과 같습니다.

| 매개변수        | 유형   | 의미                                                     |
| ----------- | ------ | -------------------------------------------------------- |
| warningCode | int    | 에러 코드                                                 |
| warningMsg  | String | 경고 정보                                               |
| extraInfo   | String | 확장 정보 필드. 각각의 에러 코드에 포함된 추가 정보로 문제를 파악할 수 있습니다. |


### onKickedOffline

다른 사용자가 동일한 계정으로 로그인 시 강제 로그아웃


## 방 이벤트 콜백

### onRoomDestroy

방 폐기 콜백. 호스트가 방을 종료하면 방 안에 있는 모든 사용자는 해당 공지를 받게 됩니다.

### onAnchorListChange

호스트 리스트 변경 공지입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미       |
| ------ | ------ | ---------- |
| userId | String | 사용자 ID  |
| mute   | bool   | 음소거 상태 |


### onUserVolumeUpdate

음량 크기 알림을 활성화하여 모든 참여자의 음량 크기를 공지합니다.


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                      |
| ------ | ------ | ------------------------- |
| userId | String | 사용자 ID                 |
| volume | int    | 음량 크기이며, 0~100으로 설정할 수 있습니다. |


## 마이크 위치 콜백


### onAnchorEnterMic

사용자 마이크 켜짐

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미                 |
| ---------- | ------ | -------------------- |
| userId     | String | 마이크가 켜진 사용자 ID       |
| userName   | String | 사용자 닉네임           |
| userAvatar | String | 프로필 사진 주소           |
| mute       | bool   | 마이크 위치 상태, 기본값: 켜짐 |

### onAnchorLeaveMic

사용자 마이크 꺼짐

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | -------------- |
| userId | String | 마이크가 꺼진 사용자 ID |

### onMicMute

호스트 마이크 음소거 여부

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | -------------- |
| userId | String | 마이크가 꺼진 사용자 ID |
| mute   | bool   | 마이크 위치 상태     |


## 시청자 입장/퇴장 이벤트 콜백

### onAudienceEnter

시청자 방 입장 공지 수신


매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미           |
| ---------- | ------ | -------------- |
| userId     | String | 마이크가 켜진 사용자 ID |
| userName   | String | 사용자 닉네임     |
| userAvatar | String | 프로필 사진 주소     |

### onAudienceExit

시청자 방 퇴장 공지 수신

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | -------------- |
| userId | String | 마이크가 꺼진 사용자 ID |


## 메시지 이벤트 콜백

### onRecvRoomTextMsg

텍스트 메시지 수신

매개변수는 다음과 같습니다.

| 매개변수       | 유형   | 의미             |
| ---------- | ------ | ---------------- |
| message    | String | 텍스트 메시지       |
| sendId     | String | 발신자 ID   |
| userAvatar | String | 발신자 프로필 사진 |
| userName   | String | 발신자 닉네임 |


## 손 들기 신청 신호 이벤트 콜백

### onRaiseHand

새로운 마이크 켜기 요청 수신


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미               |
| ------ | ------ | ------------------ |
| userId | String | 손 들기를 신청한 사용자 ID |


### onAgreeToSpeak

호스트가 마이크 켜기 동의 시 콜백


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | -------------- |
| userId | String | 호스트의 사용자 ID |

### onRefuseToSpeak

호스트가 마이크 켜기 거부 시 콜백


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미           |
| ------ | ------ | -------------- |
| userId | String | 호스트의 사용자 ID |
