TRTCVideoCall은 Tencent Cloud의 Tencent Real-Time Communication(TRTC)과 인스턴트 메시지 IM 서비스를 결합한 것으로, 1v1 및 다중 사용자 영상 통화를 지원합니다. TRTCVideoCall은 오픈 소스 Class이며 Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 과정은 [실시간 영상 통화(iOS)](https://intl.cloud.tencent.com/document/product/647/36065)를 참조하십시오.
- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저딜레이 멀티미디어 통화 모듈로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 정보를 발송 및 처리합니다.


<h2 id="TRTCVideoCall">TRTCVideoCall API 개요</h2>

### SDK 기본 함수

| API | 설명 |
|-----|-----|
| [shared](#shared) | 모듈 단일 항목|
| [delegate](#delegate) | 이벤트 콜백 설정|
| [setup](#setup) | 초기화 함수입니다. 모든 기능을 사용하기 전 이 함수로 필요한 초기화를 진행합니다. |
| [destroy](#destroy) | 폐기 함수입니다. 해당 인스턴스를 다시 실행할 필요가 없을 경우, 해당 인터페이스를 호출합니다.|
| [login](#login) | 모듈 인터페이스에 로그인합니다. 모든 기능은 먼저 로그인 한 후 사용할 수 있습니다.|
| [logout](#logout) | 모듈 인터페이스에서 로그아웃합니다. 로그아웃한 후에는 발신 기능을 사용할 수 없습니다.|


### 통화 작업 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [call](#call) | 1명에게 통화 초대|
| [groupCall](#groupcall) | 그룹통화 초대|
| [accept](#accept) | 현재 통화를 수신합니다.|
| [reject](#reject) | 통화 거절|
| [hangup](#hangup) | 현재 통화 종료 |

### 스트리밍 관련 인터페이스 함수
| API | 설명 |
|-----|-----|
| [startRemoteView](#startremoteview) | 원격 사용자의 카메라 데이터를 지정한 UIView로 렌더링합니다. |
| [stopRemoteView](#stopremoteview) | 원격 데이터 렌더링을 종료합니다.|

### 멀티미디어 제어 관련 인터페이스 함수

| API | 설명 |
|-----|-----|
| [openCamera](#opencamera) | 카메라를 활성화해 지정한 UIView로 렌더링합니다. |
| [switchCamera](#switchcamera) | 전후면 카메라를 전환합니다.|
| [closeCamara](#closecamara) | 카메라를 끕니다. |
| [setMicMute](#setmicmute) | 원격으로 오디오를 음소거합니다. |
| [setHandsFree](#sethandsfree) | 핸즈프리를 설정합니다. |

<h2 id="TRTCVideoCallDelegate">TRTCVideoCallDelegate API 개요</h2>

### 범용 이벤트 콜백

| API | 설명 |
|-----|-----|
| [onError](#onerror) | 오류 콜백입니다.|

### 초대 발신자 콜백

| API | 설명 |
|-----|-----|
| [onReject](#onreject) | 통화 거절 콜백입니다. |
| [onNoResp](#onnoresp) | 상대방 응답 없음 콜백입니다.|
| [onLineBusy](#onlinebusy) | 통화 중 콜백입니다.|

### 초대 수신자 콜백

| API | 설명 |
|-----|-----|
| [onInvited](#oninvited) | 통화에 초대됨 콜백입니다.|
| [onCallingCancel](#oncallingcancel) | 현재 통화 취소됨 콜백입니다.|
| [onCallingTimeOut](#oncallingtimeout) | 현재 통화 시간 초과 콜백입니다.|

### 범용 콜백

| API | 설명 |
|-----|-----|
| [onGroupCallInviteeListUpdate](#ongroupcallinviteelistupdate) | 그룹 채팅 초대 리스트 업데이트 콜백입니다.|
| [onUserEnter](#onuserenter) | 사용자 통화 입장 콜백입니다.|
| [onUserLeave](#onuserleave) | 사용자 통화 종료 콜백입니다.|
| [onUserAudioAvailable](#onuseraudioavailable) | 사용자의 오디오 업스트림 활성화 여부 콜백입니다.|
| [onUserVideoAvailable](#onuservideoavailable) | 사용자의 비디오 업스트림 활성화 여부 콜백입니다.|
| [onUserVoiceVolume](#onuservoicevolume) | 사용자 통화 음량 콜백입니다.|
| [onCallEnd](#oncallend) | 통화 종료 콜백입니다.|

## SDK 기본 함수
### shared
shared는 TRTCVideoCall의 모듈 단일 항목입니다.
```swift
@objc public static let shared = TRTCVideoCall()
```


### delegate

[TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36065) 이벤트 콜백입니다. TRTCVideoCallDelegate를 통해 [TRTCVideoCall](https://intl.cloud.tencent.com/document/product/647/36065) 의 각종 상태 공지를 받을 수 있습니다.
```swift
@objc public weak var delegate: TRTCVideoCallDelegate?
```

>?delegate는 TRTCVideoCall의 프록시 콜백입니다.

### setup

초기화 함수입니다. 모든 기능을 사용하기 전 이 함수로 필요한 초기화를 진행합니다.
```swift
@objc public func setup()
```
### destroy

함수 폐기. 해당 인스턴스를 실행할 필요가 없을 경우 본 인터페이스를 호출하십시오.
```swift
@objc func destroy()
```

### login

모듈에 로그인합니다.
```swift
@objc func login(sdkAppID: UInt32,
                 user: String,
                 userSig: String,
                 success: @escaping (() -> Void),
                 failed: @escaping ((_ code: Int, _ message: String) -> Void))
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| sdkAppID | UInt32 | TRTC 콘솔 > [애플리케이션 관리](https://console.cloud.tencent.com/trtc/app) > 애플리케이션 정보에서 SDKAppID를 조회할 수 있습니다. |
| user | String | 현재 사용자 ID, 문자열 유형은 영어 알파벳(a~z, A~Z), 숫자(0~9), 대시부호(-), 언더바(\_)만 허용됩니다. |
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명으로, 취득 방법은 [UserSig 컴퓨팅 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참조하십시오. |
| success | (() -> Void) | 로그인 성공 콜백입니다. |
| failed | ((_ code: Int, _ message: String) -> Void) | 로그인 실패 콜백입니다. |

### logout

모듈에서 로그아웃하였습니다.
```swift
@objc func logout(success: @escaping (() -> Void),
           failed: @escaping ((_ code: Int, _ message: String) -> Void))
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| success | (() -> Void) | 로그아웃 성공 콜백입니다. |
| failed | ((_ code: Int, _ message: String) -> Void) | 로그아웃 실패 콜백입니다. |


## 통화 작업 관련 인터페이스 함수
### call

1인 통화 초대는 현재 통화 중이더라도 계속 다른 사람을 초대할 수 있습니다.

```swift
@objc func call(userID: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userID | String | 사용자ID를 호출합니다. |

### groupCall

IM 그룹 통화 초대. 초대된 사용자는 `onInvited()` 콜백을 받습니다. 현재 통화 중일 경우에는 해당 함수를 호출해 계속 통화에 초대할 수 있으며, 통화 중인 사용자는 `onGroupCallInviteeListUpdate()` 콜백을 받습니다.
```swift
@objc func groupCall(userIDs: [String], groupID: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userIDs | [String] | 초대 ID 리스트 |
| groupID | String | 그룹 ID |



### accept

현재 통화를 수락합니다. 초대된 사용자가 `onInvited()` 콜백을 받으면 해당 함수를 호출해 통화를 수신할 수 있습니다.
```swift
@objc func accept()
```



### reject

현재 통화를 거절했습니다. 초대된 사용자로서 `onInvited()` 콜백을 수신하면 해당 함수로 통화를 거절할 수 있습니다.
```swift
@objc func reject()
```



### hangup

통화를 종료합니다. 통화 중이었다면 해당 함수로 통화를 종료할 수 있습니다.

```swift
@objc func hangup()
```


## 스트리밍 관련 인터페이스 함수
### startRemoteView

원격 사용자의 카메라 데이터를 지정한 UIView로 렌더링합니다.
```swift
@objc func startRemoteView(userId: String, view: UIView)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 원격 사용자 ID |
| view | UIView | 비디오 모니터를 탑재한 컨트롤러 |


### stopRemoteView

원격 데이터 렌더링을 종료합니다.
```swift
@objc func stopRemoteView(userId: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userId | String | 원격 사용자 ID |

## 멀티미디어 제어 관련 인터페이스 함수
### openCamera

카메라를 열고 지정한 UIView로 렌더링합니다.
```swift
@objc func openCamera(frontCamera: Bool, view: UIView)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| frontCamera | Bool | true: 전면 카메라를 켭니다. false: 후면 카메라를 켭니다. |
| view | UIView | 비디오 모니터를 탑재한 컨트롤러 |

### switchCamera

전후면 카메라를 전환합니다.
```swift
@objc func switchCamera(frontCamera: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| frontCamera | Bool | true: 전면 카메라로 전환합니다. false: 후면 카메라로 전환합니다. |

### closeCamara

카메라를 끕니다.
```swift
@objc func closeCamara()
```

### setMicMute

원격 오디오를 음소거합니다.
```swift
@objc func setMicMute(isMute: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| isMute | Bool | true: 마이크 끔, false: 마이크 켬 |

### setHandsFree

원격 오디오를 음소거합니다.
```swift
@objc func setHandsFree(isHandsFree: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| isHandsFree | Bool | true: 핸즈프리 활성화, false: 핸즈프리 비활성화입니다. |

## TRTCVideoCallDelegate 이벤트 콜백

## 범용 이벤트 콜백
### onError

오류 콜백입니다.
>?SDK 복구할 수 없는 오류입니다. 반드시 리슨하고 상황에 따라 사용자에게 적합한 인터페이스 안내를 해야 합니다.

```swift
@objc optional func onError(code: Int32, msg: String?)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| code | Int | 에러 코드 |
| msg | String? | 오류 정보 |


## 초대 발신자 콜백
### onReject

통화 거절 콜백입니다.
```swift
@objc optional func onReject(uid: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 거부된 사용자 ID |

### onNoResp

상대방이 콜백에 응답이 없습니다.
```swift
@objc optional func onNoResp(uid: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 응답하지 않는 사용자 ID |

### onLineBusy

통화 중 콜백입니다.
```swift
@objc optional func onLineBusy(uid: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 중인 사용자 ID |

## 초대 수신자 콜백
### onInvited

초대된 사용자 통화 콜백입니다.
```swift
@objc optional func onInvited(sponsor: String, userIds: [String], isFromGroup: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| sponsor | String | 발신자 ID |
| userIds | [String] | 초대 ID 리스트 |
| isFromGroup | Bool | 다중 사용자 통화 초대 여부|

### onCallingCancel

현재 통화의 콜백이 취소되었습니다. 수신자가 요청을 처리하지 않고 요청 측이 취소한 후 이 콜백을 받을 수 있습니다.
```swift
@objc optional func onCallingCancel()
```



### onCallingTimeOut

현재 통화 시간 초과 콜백입니다.
```swift
@objc optional func onCallingTimeOut()
```

## 범용 콜백
### onGroupCallInviteeListUpdate

그룹통화 초대 리스트를 업데이트하였습니다.
```swift
@objc optional func onGroupCallInviteeListUpdate(userIds: [String])
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| userIds | [String] | 초대 ID 리스트 |

### onUserEnter

사용자 통화 입장 콜백입니다.
```swift
@objc optional func onUserEnter(uid: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 입장 사용자 ID |

### onUserLeave

사용자 통화 종료 콜백입니다.
```swift
@objc optional func onUserLeave(uid: String)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 종료 사용자 ID |

### onUserAudioAvailable

사용자 오디오 업스트림 활성화 여부 콜백입니다.
```swift
@objc optional func onUserAudioAvailable(uid: String, available: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 사용자 ID |
| available | Bool | 사용자의 오디오 사용 가능 여부|

### onUserVideoAvailable

사용자 비디오 업스트림 활성화 여부 콜백입니다. 공지를 받은 후, 사용자는 `startRemoteView` 렌더링 원격 비디오를 불러올 수 있습니다.
```swift
@objc optional func onUserVideoAvailable(uid: String, available: Bool)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 사용자 ID |
| available | Bool | 사용자의 비디오 사용 가능 여부|


### onUserVoiceVolume

사용자 통화 음량 콜백입니다.
```swift
@objc optional func onUserVoiceVolume(uid: String, volume: UInt32)
```

매개변수는 다음과 같습니다.

| 매개변수 | 유형 | 의미 |
|-----|-----|-----|
| uid | String | 통화 사용자 ID |
| volume | UInt32 | 통화 사용자의 음량 범위는 0~100입니다. |

### onCallEnd

통화 종료 콜백입니다.
```swift
@objc optional func onCallEnd()
```
