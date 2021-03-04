TRTCCalling은 Tencent Cloud TRTC와 IM 서비스를 기반으로 조합하여 구성되며, 1대1 및 다중 사용자 음성 통화를 지원합니다. TRTCCalling은 오픈 소스 Class로 Tencent Cloud의 2개의 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [실시간 음성 통화(iOS)](https://intl.cloud.tencent.com/document/product/647/36067)를 참조하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저딜레이 멀티미디어 통화 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 정보를 발송 및 처리합니다.


<h2 id="TRTCCalling">TRTCCalling API 개요</h2>

### SDK 기본 함수

| API                             | 설명                                             |
| ------------------------------- | ------------------------------------------------ |
| [shareInstance](#shareinstance) | 컴포넌트 단일 항목                                       |
| [addDelegate](#adddelegate)     | 이벤트 콜백을 추가합니다.                                   |
| [login](#login)                 | 컴포넌트 인터페이스에 로그인합니다. 모든 기능은 먼저 로그인 한 후 사용할 수 있습니다. |
| [logout](#logout)               | 컴포넌트 인터페이스에 로그아웃합니다. 로그아웃 후 다시 발신 작업을 할 수 없습니다.         |


### 통화 작업 관련 인터페이스 함수

| API                     | 설명         |
| ----------------------- | -------------- |
| [call](#call)           | 1명을 통화에 초대합니다. |
| [groupCall](#groupcall) | 그룹을 통화에 초대합니다. |
| [accept](#accept)       | 현재 통화를 수신합니다. |
| [reject](#reject)       | 현재 통화를 거절합니다. |
| [hangup](#hangup)       | 현재 통화를 종료합니다. |

### 오디오 제어 관련 인터페이스 함수

| API                           | 설명                                   |
| ----------------------------- | -------------------------------------- |
| [setMicMute](#setmicmute)     | 로컬 오디오 샘플링을 음소거합니다.                     |
| [setHandsFree](#sethandsfree) | 핸즈프리를 설정합니다.                             |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API 개요</h2>

### 범용 이벤트 콜백

| API                 | 설명       |
| ------------------- | ---------- |
| [onError](#onerror) | 오류 콜백입니다. |

### 초대 발신자 콜백

| API                       | 설명             |
| ------------------------- | ---------------- |
| [onReject](#onreject)     | 통화 거절 콜백입니다.   |
| [onNoResp](#onnoresp)     | 상대방 응답 없음 콜백입니다. |
| [onLineBusy](#onlinebusy) | 통화 중 콜백입니다.   |

### 초대 수신자 콜백

| API                                   | 설명                 |
| ------------------------------------- | -------------------- |
| [onInvited](#oninvited)               | 통화에 초대됨 콜백입니다.     |
| [onCallingCancel](#oncallingcancel)   | 현재 통화 취소됨 콜백입니다. |
| [onCallingTimeOut](#oncallingtimeout) | 현재 통화 시간 초과 콜백입니다.   |

### 범용 콜백

| API                                                          | 설명                       |
| ------------------------------------------------------------ | -------------------------- |
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | 그룹 채팅 초대 리스트 업데이트 콜백입니다.     |
| [onUserEnter](#onuserenter)                                  | 사용자 통화 입장 콜백입니다.         |
| [onUserLeave](#onuserleave)                                  | 사용자 통화 종료 콜백입니다.         |
| [onUserAudioAvailable](#onuseraudioavailable)                | 사용자의 오디오 업스트림 활성화 여부 콜백입니다. |
| [onUserVoiceVolume](#onuservoicevolume)                      | 사용자 통화 음량 콜백입니다.         |
| [onCallEnd](#oncallend)                                      | 통화 종료 콜백입니다.             |

## SDK 기본 함수

### shareInstance

shareInstance는 TRTCCalling의 컴포넌트 단일 항목입니다.

```Objective-C
/// 단일 항목 객체
+ (TRTCCalling *)shareInstance;
```


### addDelegate

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065) 이벤트 콜백, TRTCCallingDelegate에서 [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36065)의 각종 상태 알림을 확인할 수 있습니다.

```Objective-C
/// TRTCCallingDelegate 콜백 설정
/// @param delegate 콜백 인스턴스
- (void)addDelegate:(id<TRTCCallingDelegate>)delegate;
```

### login

모듈에 로그인합니다.

```Objective-C
typedef void(^CallingActionCallback)(void);
typedef void(^ErrorCallback)(int code, NSString *des);

/// 로그인 인터페이스
/// @param sdkAppID SDK ID, Tencent Cloud 콘솔에서 획득할 수 있습니다.
/// @param userID 사용자 ID
/// @param userSig 사용자 서명
/// @param success 콜백 성공
/// @param failed 콜백 실패
- (void)login:(UInt32)sdkAppID
         user:(NSString *)userID
      userSig:(NSString *)userSig
      success:(CallingActionCallback)success
       failed:(ErrorCallback)failed
NS_SWIFT_NAME(login(sdkAppID:user:userSig:success:failed:));
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형                  | 의미                                                         |
| -------- | --------------------- | ------------------------------------------------------------ |
| sdkAppID | UInt32                | TRTC 콘솔>[어플리케이션 관리](https://console.cloud.tencent.com/trtc/app)>어플리케이션 정보에서 SDKAppID를 조회할 수 있습니다. |
| user     | String                | 현재 사용자 ID, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(\_)만 허용됩니다.|
| userSig  | String                | Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |
| success  | CallingActionCallback | 로그인 성공 콜백입니다.                                               |
| failed   | ErrorCallback         | 로그인 실패 콜백입니다.                                               |

### logout

모듈에서 로그아웃하였습니다.

```Objective-C
/// 로그아웃 인터페이스
/// @param success 콜백 성공
/// @param failed 콜백 실패
- (void)logout:(CallingActionCallback)success
        failed:(ErrorCallback)failed
NS_SWIFT_NAME(logout(success:failed:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형                  | 의미           |
| ------- | --------------------- | -------------- |
| success | CallingActionCallback | 로그아웃 성공 콜백입니다. |
| failed  | ErrorCallback         | 로그아웃 실패 콜백입니다. |


## 통화 작업 관련 인터페이스 함수

### call

1인 통화 초대는 현재 통화 중이더라도 계속 다른 사람을 초대할 수 있습니다.

```Objective-C
/// 1v1통화 요청 인터페이스
/// @param userID 초대된 사용자 ID
/// @param type 통화 유형: 영상/음성
- (void)call:(NSString *)userID
        type:(CallType)type
NS_SWIFT_NAME(call(userID:type:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형     | 의미                  |
| ------ | -------- | --------------------- |
| userID | String   | 호출 사용자 ID입니다.         |
| type   | CallType | 통화 유형: 영상/음성 |

### groupCall

IM 그룹 통화 초대. 초대된 사용자는 `onInvited` 콜백을 받습니다. 현재 통화 중일 경우에는 해당 함수를 호출해 계속 통화에 초대할 수 있으며, 통화 중인 사용자는 `onGroupCallInviteeListUpdate` 콜백을 받습니다.

```Objective-C
/// 다중 사용자 통화 요청
/// @param userIDs 초대된 사용자 ID 리스트
/// @param type 통화유형: 영상/음성
/// @param groupID 그룹ID, 매개변수 선택 가능
- (void)groupCall:(NSArray *)userIDs
             type:(CallType)type
          groupID:(NSString * _Nullable)groupID
NS_SWIFT_NAME(groupCall(userIDs:type:groupID:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형     | 의미                  |
| ------- | -------- | --------------------- |
| userIDs | [String] | 초대 ID 리스트        |
| type    | CallType | 통화 유형: 영상/음성 |
| groupID | String   | 그룹 ID                |



### accept

현재 통화를 수락합니다. 초대된 사용자가 `onInvited` 콜백을 받으면 해당 함수를 호출해 통화를 수신할 수 있습니다.

```Objective-C
/// 현재 통화 받기
- (void)accept;
```



### reject

현재 통화를 거절했습니다. 초대된 사용자가 `onInvited` 콜백을 수신하면 해당 함수를 호출해 통화를 거절할 수 있습니다.

```Objective-C
/// 현재 통화 거절
- (void)reject;
```



### hangup

통화를 종료합니다. 통화 중이었다면 해당 함수로 통화를 종료할 수 있습니다.

```Objective-C
/// 현재 통화 끊기
- (void)hangup;
```

## 오디오 제어 관련 인터페이스 함수

### setMicMute

로컬 오디오 샘플링을 음소거합니다.

```Objective-C
///음소거 작업
- (void)setMicMute:(BOOL)isMute;
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형 | 의미                                  |
| ------ | ---- | ------------------------------------- |
| isMute | Bool | true: 마이크 끔, false: 마이크 켬 |

### setHandsFree

핸즈프리 활성화입니다.

```Objective-C
///핸즈프리 작업
- (void)setHandsFree:(BOOL)isHandsFree;
```

매개변수는 다음과 같습니다.

| 매개변수        | 유형 | 의미                              |
| ----------- | ---- | --------------------------------- |
| isHandsFree | Bool | true: 핸즈프리 활성화, false: 핸즈프리 비활성화입니다. |

## TRTCCallingDelegate 이벤트 콜백

## 범용 이벤트 콜백

### onError

오류 콜백입니다.

>?SDK 복구할 수 없는 오류입니다. 반드시 리슨하고 상황에 따라 사용자에게 적합한 인터페이스 안내를 해야 합니다.

```Objective-C
/// sdk 내부에 오류 발생 | sdk error
/// - Parameters:
///   - code: 에러 코드
///   - msg: 에러 메시지
-(void)onError:(int)code msg:(NSString * _Nullable)msg
NS_SWIFT_NAME(onError(code:msg:));

```

매개변수는 다음과 같습니다.

| 매개변수 | 유형    | 의미       |
| ---- | ------- | ---------- |
| code | Int     | 에러 코드입니다.   |
| msg  | String? | 오류 정보입니다. |


## 초대 발신자 콜백

### onReject

통화 거절 콜백입니다.

```Objective-C
/// 통화 거절 콜백-초대된 사용자만 공지 수신, 다른 사용자는 onUserEnter 사용 필요 |
/// reject callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onReject:(NSString *)uid
NS_SWIFT_NAME(onReject(uid:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미            |
| ---- | ------ | --------------- |
| uid  | String | 거절한 사용자 ID입니다. |

### onNoResp

상대방이 콜백에 응답이 없습니다.

```Objective-C
/// 응답 없음 콜백-초대된 사용자만 공지 수신, 다른 사용자는 onUserEnter 사용 필요 |
/// no response callback only worked for Sponsor, others should use onUserEnter)
/// - Parameter uid: userid
-(void)onNoResp:(NSString *)uid
NS_SWIFT_NAME(onNoResp(uid:));

```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미              |
| ---- | ------ | ----------------- |
| uid  | String | 응답이 없는 사용자 ID입니다. |

### onLineBusy

통화 중 콜백입니다.

```Objective-C
/// 통화 중 콜백-초대된 사용자만 공지 수신, 다른 사용자는 onUserEnter 사용 필요 |
/// linebusy callback only worked for Sponsor, others should use onUserEnter
/// - Parameter uid: userid
-(void)onLineBusy:(NSString *)uid
NS_SWIFT_NAME(onLineBusy(uid:));

```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미            |
| ---- | ------ | --------------- |
| uid  | String | 통화 중인 사용자 ID입니다. |

## 초대 수신자 콜백

### onInvited

초대된 사용자 통화 콜백입니다.

```Objective-C
/// 초대된 사용자 통화 콜백  invitee callback
/// - Parameter userIds: 초대 리스트 (invited list)
-(void)onInvited:(NSString *)sponsor
         userIds:(NSArray<NSString *> *)userIds
     isFromGroup:(BOOL)isFromGroup
        callType:(CallType)callType
NS_SWIFT_NAME(onInvited(sponsor:userIds:isFromGroup:callType:));
```

매개변수는 다음과 같습니다.

| 매개변수        | 유형     | 의미                  |
| ----------- | -------- | --------------------- |
| sponsor     | String   | 발신자 ID입니다.         |
| userIds     | [String] | 초대 ID 리스트입니다.        |
| isFromGroup | Bool     | 다중 사용자 통화 초대 여부    |
| callType    | CallType | 통화 유형: 영상/음성 |

### onCallingCancel

현재 통화의 콜백이 취소되었습니다. 수신자가 요청을 처리하지 않고 요청 측이 취소한 후 이 콜백을 받을 수 있습니다.

```Objective-C
/// 현재 통화 취소됨 콜백 | current call had been canceled callback
-(void)onCallingCancel:(NSString *)uid
NS_SWIFT_NAME(onCallingCancel(uid:));
```



### onCallingTimeOut

현재 통화 시간 초과 콜백입니다.

```Objective-C
/// 통화 시간 초과 콜백 | timeout callback
-(void)onCallingTimeOut;
```

## 범용 콜백

### onGroupCallInviteeListUpdate

그룹 채팅 초대 리스트 업데이트 콜백입니다.

```Objective-C
/// 그룹 채팅 초대 리스트 업데이트 콜백 | update current inviteeList in group calling
/// - Parameter userIds: 초대 리스트 | inviteeList
-(void)onGroupCallInviteeListUpdate:(NSArray *)userIds
NS_SWIFT_NAME(onGroupCallInviteeListUpdate(userIds:));
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형     | 의미           |
| ------- | -------- | -------------- |
| userIds | [String] | 초대 ID 리스트입니다. |

### onUserEnter

사용자 통화 입장 콜백입니다.

```Objective-C
/// 통화 입장 콜백 | user enter room callback
/// - Parameter uid: userid
-(void)onUserEnter:(NSString *)uid
NS_SWIFT_NAME(onUserEnter(uid:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미              |
| ---- | ------ | ----------------- |
| uid  | String | 통화 입장 사용자 ID입니다. |

### onUserLeave

사용자 통화 종료 콜백입니다.

```Objective-C
/// 통화 퇴장 콜백 | user leave room callback
/// - Parameter uid: userid
-(void)onUserLeave:(NSString *)uid
NS_SWIFT_NAME(onUserLeave(uid:));
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미              |
| ---- | ------ | ----------------- |
| uid  | String | 통화 종료 사용자 ID입니다. |

### onUserAudioAvailable

사용자 오디오 업스트림 활성화 여부 콜백입니다.

```Objective-C
/// 사용자의 음성 업스트림 콜백 활성화 여부 | is user audio available callback
/// - Parameters:
///   - uid: 사용자 ID | userID
///   - available: 유효 여부 | available
-(void)onUserAudioAvailable:(NSString *)uid available:(BOOL)available
NS_SWIFT_NAME(onUserAudioAvailable(uid:available:));

```

매개변수는 다음과 같습니다.

| 매개변수      | 유형   | 의미               |
| --------- | ------ | ------------------ |
| uid       | String | 통화 사용자 ID입니다.      |
| available | Bool   | 사용자의 오디오 사용 가능 여부 |

### onUserVoiceVolume

사용자 통화 음량 콜백입니다.

```Objective-C
/// 사용자 음량 콜백
/// - Parameter uid: 사용자 ID | userID
/// - Parameter volume: 발화자의 음량, 값 범위 0 - 100
-(void)onUserVoiceVolume:(NSString *)uid volume:(UInt32)volume
NS_SWIFT_NAME(onUserVoiceVolume(uid:volume:));
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                            |
| ------ | ------ | ------------------------------- |
| uid    | String | 통화 사용자 ID입니다.                   |
| volume | UInt32 | 통화자의 음량, 값 범위는 0 - 100입니다. |

### onCallEnd

통화 종료 콜백입니다.

```Objective-C
/// 통화 종료 | end callback
-(void)onCallEnd;
```
