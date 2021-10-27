TRTCCalling은 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 결합한 것으로, 1v1 멀티미디어 통화를 지원합니다. TRTCCalling은 오픈 소스 Class로 Tencent Cloud의 2개의 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 방법은 [실시간 음성 통화(Flutter)](https://intl.cloud.tencent.com/document/product/647/41692)를 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저지연 멀티미디어 통화 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 정보를 발송 및 처리합니다.


<h2 id="TRTCCalling">TRTCCalling API 개요</h2>

### SDK 기본 함수

| API                                             | 설명                                          |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | 컴포넌트 싱글톤입니다.                                       |
| [destroySharedInstance](#destroysharedinstance) | 컴포넌트 싱글톤을 폐기합니다.                                   |
| [registerListener](#registerlistener)                     | 이벤트 콜백을 추가합니다.                                   |
| [unRegisterListener](#unregisterlistener)               | 콜백 인터페이스를 삭제합니다.                                   |
| [destroy](#destroy)                             | 함수를 폐기합니다. 해당 인스턴스를 다시 실행할 필요가 없을 경우, 해당 인터페이스를 호출합니다.   |
| [login](#login)                                 | 컴포넌트 인터페이스에 로그인합니다. 모든 기능은 먼저 로그인 한 후 사용할 수 있습니다. |
| [logout](#logout)                               | 컴포넌트 인터페이스에서 로그아웃합니다. 로그아웃한 후에는 발신 기능을 사용할 수 없습니다.         |


### 통화 작업 관련 인터페이스 함수

| API                     | 설명           |
| ----------------------- | -------------- |
| [call](#call)           | 1:1 통화에 초대합니다. |
| [accept](#accept)       | 현재 통화를 수신합니다. |
| [reject](#reject)       | 현재 통화를 거절합니다. |
| [hangup](#hangup)       | 현재 통화를 종료합니다. |


### 오디오 제어 관련 인터페이스 함수

| API                           | 설명                                             |
| ----------------------------- | ------------------------------------------------ |
| [setMicMute](#setmicmute)     | 로컬 오디오 수집을 음소거합니다.                     |
| [setHandsFree](#sethandsfree) | 핸즈프리를 설정합니다.                             |

<h2 id="TRTCCallingDelegate">TRTCCallingDelegate API 개요</h2>

### 일반적인 이벤트 콜백

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
| [onUserEnter](#onuserenter)                                  | 사용자 통화 입장 콜백입니다.         |
| [onUserLeave](#onuserleave)                                  | 사용자 통화 퇴장 콜백입니다.         |
| [onUserAudioAvailable](#onuseraudioavailable)                | 사용자의 오디오 업스트림 활성화 여부 콜백입니다. |
| [onUserVoiceVolume](#onuservoicevolume)                      | 사용자 통화 음량 콜백입니다.         |
| [onCallEnd](#oncallend)                                      | 통화 종료 콜백입니다.             |

## SDK 기본 함수

### sharedInstance

sharedInstance는 TRTCCalling의 컴포넌트 싱글톤입니다.

```java
static Future<TRTCCalling> sharedInstance();
```

### destroySharedInstance

컴포넌트 싱글톤을 폐기합니다.

```java
static void destroySharedInstance();
```

### destroy

함수 폐기. 해당 인스턴스를 실행할 필요가 없을 경우 본 인터페이스를 호출하십시오.

```java
void destroy();
```

### registerListener

[TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066) 이벤트 콜백. TRTCCallingDelegate에서 [TRTCCalling](https://intl.cloud.tencent.com/document/product/647/36066)의 각종 상태 알림을 확인할 수 있습니다.

```java
void registerListener(VoiceListenerFunc func);
```


### unRegisterListener

콜백 인터페이스를 삭제합니다.

```java
void unRegisterListener(VoiceListenerFunc func);
```

### login

컴포넌트에 로그인합니다.

```java
Future<ActionCallback> login(int sdkAppId, String userId, String userSig);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형           | 의미                                                         |
| -------- | -------------- | ------------------------------------------------------------ |
| sdkAppID | int            | TRTC 콘솔>[[애플리케이션 관리](https://console.cloud.tencent.com/trtc/app)]>애플리케이션 정보에서 SDKAppID를 확인할 수 있습니다. |
| userId     | String         | 현재 사용자의 ID입니다. 문자열 유형은 영어 알파벳(a-z, A-Z), 숫자(0-9), 대시 부호(-), 언더바(\_)만 허용됩니다. |
| userSig | String | Tencent Cloud가 설계한 일종의 보안 서명입니다. 획득 방식은 [UserSig 계산 방법](https://intl.cloud.tencent.com/document/product/647/35166)을 참고하십시오. |

### logout

컴포넌트에서 로그아웃하였습니다.

```java
Future<ActionCallback> logout();
```

## 통화 작업 관련 인터페이스 함수

### call

1인 통화 초대는 현재 통화 중이더라도 계속 다른 사람을 초대할 수 있습니다.

```java
Future<ActionCallback> call(String userId, int type);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미                             |
| ------ | ------ | -------------------------------- |
| userId | String | 호출 사용자 ID입니다.                    |
| type   | int    | 1은 음성 통화를, 2는 영상 통화를 뜻합니다. |

### accept

현재 통화를 수락합니다. 초대된 사용자가 `onInvited()` 콜백을 받으면 해당 함수를 호출해 통화를 수신할 수 있습니다.

```java
Future<ActionCallback> accept();
```

### reject

현재 통화를 거절했습니다. 초대된 사용자로서 `onInvited()` 콜백을 수신하면 해당 함수로 통화를 거절할 수 있습니다.

```java
Future<ActionCallback> reject();
```

### hangup

통화를 종료합니다. 통화 중이었다면 해당 함수로 통화를 종료할 수 있습니다.

```java
void hangup();
```


## 오디오 제어 관련 인터페이스 함수

### setMicMute

로컬 오디오 수집을 음소거합니다.

```java
void setMicMute(bool isMute);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미                                        |
| ------ | ------- | ------------------------------------------- |
| isMute | bool | true는 마이크 비활성화, false는 마이크 활성화를 의미합니다. |

### setHandsFree

원격 오디오를 음소거합니다.

```java
void setHandsFree(bool isHandsFree);
```

매개변수는 다음과 같습니다.

| 매개변수        | 유형    | 의미                                    |
| ----------- | ------- | --------------------------------------- |
| isHandsFree | bool | true는 핸즈프리 활성화, false는 핸즈프리 비활성화를 의미합니다. |

## TRTCCallingDelegate 이벤트 콜백

## 일반적인 이벤트 콜백

### onError

오류 콜백.

>?SDK가 복구할 수 없는 오류는 반드시 모니터링하고 상황에 따라 적절한 인터페이스를 사용자에게 제시해야 합니다.

매개변수는 다음과 같습니다.

| 매개변수 | 유형   | 의미       |
| ---- | ------ | ---------- |
| code | int    | 에러 코드입니다.   |
| msg  | String | 오류 정보입니다. |


## 초대 발신자 콜백

### onReject

통화 거절 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId | String | 거절한 사용자 ID입니다. |

### onNoResp

상대방 응답 없음 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId | String | 응답이 없는 사용자 ID입니다. |

### onLineBusy

통화 중 콜백입니다.


매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미            |
| ------ | ------ | --------------- |
| userId    | String  | 통화 중인 사용자 ID입니다.      |

## 초대 수신자 콜백

### onInvited

초대된 사용자 통화 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수        | 유형               | 의미                             |
| ----------- | ------------------ | -------------------------------- |
| sponsor     | String             | 발신자 ID입니다.                    |
| userIds     | List&lt;String&gt; | 본인 이외의 초대된 ID 리스트입니다.         |
| isFromGroup | bool          | 다중 사용자 통화 초대 여부               |
| type        | int                | 1은 음성 통화, 2는 영상 통화를 뜻합니다. |

### onCallingCancel

현재 통화의 콜백이 취소되었습니다. 수신자가 요청을 처리하지 않고 요청 측이 취소한 후 이 콜백을 받을 수 있습니다.


### onCallingTimeOut

현재 통화 시간 초과 콜백입니다.


## 범용 콜백

### onUserEnter

사용자 통화 입장 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId | String | 통화 입장 사용자 ID입니다. |

### onUserLeave

사용자 통화 종료 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수   | 유형   | 의미              |
| ------ | ------ | ----------------- |
| userId    | String  | 통화 퇴장 사용자 ID입니다.      |

### onUserAudioAvailable

사용자 오디오 업스트림 활성화 여부 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| userId    | String  | 통화 사용자 ID입니다.      |
| available | boolean | 사용자의 오디오 사용 가능 여부 |


### onUserVoiceVolume

사용자 통화 음량 콜백입니다.

매개변수는 다음과 같습니다.

| 매개변수      | 유형                       | 의미                                                         |
| --------- | -------------------------- | ------------------------------------------------------------ |
| userVolumes | List | 현재 대화 중인 모든 방 참석자 음량 범위: 0-100 |
| totalVolume | int| 모든 원격 참석자의 총 음량 범위: 0-100|

### onCallEnd

통화 종료 콜백입니다.
