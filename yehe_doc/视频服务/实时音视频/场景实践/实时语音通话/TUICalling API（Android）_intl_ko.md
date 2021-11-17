TUICalling은 Tencent Cloud의 Tencent Real-Time Communication(TRTC)과 Instant Messaging(IM) 서비스를 결합한 것으로, 1v1 및 다중 사용자 영상 통화를 지원합니다. TUICalling은 오픈 소스 Class이며 Tencent Cloud의 두 가지 클로즈드 소스 SDK에 종속됩니다. 자세한 구현 과정은 [실시간 영상 통화(Android)](https://intl.cloud.tencent.com/document/product/647/36068)를 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저지연 멀티미디어 통화 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 메시지를 발송 및 처리합니다.


## TUICalling API 개요
[](id:TUICalling)

#### SDK 기본 함수

| API                                             | 설명                                          |
| ----------------------------------------------- | ------------------------------------------------ |
| [sharedInstance](#sharedinstance)               | 컴포넌트 싱글톤                                       |
| [call](#call) | C2C 통화 초대                                   |
| [receiveAPNSCalled](#receiveAPNSCalled)                     | 초대된 사용자 통화 수신                                   |
| [setCallingListener](#setCallingListener)               | 리스너 설정.                                   |
| [setCallingBell](#setCallingBell)                             | 벨소리 설정(30초 이내 권장)   |
| [enableMuteMode](#enableMuteMode)                                 | 음소거 모드 활성화 |
| [enableFloatWindow](#enableFloatWindow)                               | 플로팅 창 활성화      |
| [enableCustomViewRoute](#enableCustomViewRoute)                               | 사용자 정의 뷰 활성화       |


## TUICallingListener API 개요
[](id:TUICallingListener)

#### 이벤트 콜백

| API                 | 설명       |
| ------------------- | ---------- |
| [shouldShowOnCallView](#shouldShowOnCallView) | 호출 수신 시 응답 페이지 열기 요청  |
| [onCallStart](#onCallStart) | 호출 시작 콜백. 발신자와 수신자 모두 트리거 |
| [onCallEnd](#onCallEnd) | 통화 콜백. 발신자와 수신자 모두 트리거 |
| [onCallEvent](#onCallEvent) | 통화 이벤트 콜백 |

## Type API 개요
[](id:Type)

#### 통화 유형
| enum                 | 설명       |
| ------------------- | ---------- |
| AUDIO | 음성 통화 |
| VIDEO | 영상 통화 |

## Role API 개요
[](id:Role)

#### 사용자 역할 유형
| enum                 | 설명       |
| ------------------- | ---------- |
| CALL | 통화 발신자 |
| CALLED | 통화 수신자 |

## Event API 개요
[](id:Event)

#### 이벤트 유형
| enum                 | 설명       |
| ------------------- | ---------- |
| CALL_START | 통화 시작 |
| CALL_SUCCEED | 통화 연결 성공 |
| CALL_END | 통화 종료 |
| CALL_FAILED | 통화 실패 |

## SDK 기본 함수

### sharedInstance
[](id:sharedInstance)

sharedInstance는 TUICalling 컴포넌트 싱글톤입니다.

```java
public static TUICallingManager sharedInstance();
```

### call
[](id:call)

C2C 통화 초대.

```java
void call(String[] userIDs, Type type);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수       | 유형    | 의미               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 통화 사용자 ID 리스트      |
| type | TUICalling.Type | 통화 유형: 오디오/비디오 |

### receiveAPNSCalled
[](id:receiveAPNSCalled)

초대 받은 사용자의 통화 수신.

```java
void receiveAPNSCalled(String[] userIDs, Type type);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 통화 사용자 ID 리스트      |
| type | TUICalling.Type | 통화 유형: 오디오/비디오 |

### setCallingListener
[](id:setCallingListener)

리스너 설정.

```java
void setCallingListener(TUICallingListener listener);
```

매개변수 리스트는 다음과 같습니다.

|  매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| listener    | TUICallingListener  | TUIcalling 컴포넌트 리스너   |

### setCallingBell
[](id:setCallingBell)

벨소리 설정(30초 이내 권장).

```java
void setCallingBell(String filePath);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| filePath    | String  | 벨소리 리소스 경로   |

### enableMuteMode
[](id:enableMuteMode)

음소거 모드 활성화.

```java
void enableMuteMode(boolean enable);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| enable    | boolean  | 음소거 모드 활성화 여부   |

### enableFloatWindow
[](id:enableFloatWindow)

플로팅 창 활성화.

```java
void enableFloatWindow(boolean enable);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미               |
| --------- | ------- | ------------------ |
| enable    | boolean  | 플로팅 창 활성화 여부   |

### enableCustomViewRoute
[](id:enableCustomViewRoute)

사용자 정의 뷰 활성화.
활성화 후 발신/수신 시작 콜백 중 CallingView 인스턴스가 수신되며 개발자가 직접 표시 방법을 결정합니다.
>! 전체 화면 표시 또는 비례 화면으로 표시해야 하며, 그렇지 않으면 이상 경고가 표시됩니다.

```java
void enableCustomViewRoute(boolean enable);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수     | 유형    | 의미               |
| --------- | ------- | ------------------ |
| enable    | boolean  | 사용자 정의 뷰 활성화 여부   |


## TUICallingListener 함수 콜백

### shouldShowOnCallView
[](id:shouldShowOnCallView)

호출 수신 시 응답 페이지 열기 요청 동의 여부.

```java
boolean shouldShowOnCallView();
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| 반환 값    | boolean  |  동의 여부   |

### onCallStart
[](id:onCallStart)

호출 시작 콜백. 발신자와 수신자 모두 트리거.

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미                |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 통화 사용자 ID 리스트.      |
| type | TUICalling.Type | 통화 유형: 오디오/비디오 |
| role | TUICalling.Role | 사용자 역할 유형: 발신자/수신자 |
| tuiCallingView | View | 통화 View. enableCustomViewRoute가 false로 설정되면 view는 null |

### onCallEnd
[](id:onCallEnd)

통화 종료 콜백. 발신자와 수신자 모두 트리거.

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

매개변수 리스트는 다음과 같습니다.

|  매개변수      | 유형    | 의미                |
| --------- | ------- | ------------------ |
| userIDs    | String[]  | 통화 사용자 ID 리스트      |
| type | TUICalling.Type | 통화 유형: 오디오/비디오 |
| role | TUICalling.Role | 사용자 역할 유형: 발신자/수신자 |
| totalTime | long | 통화 시간, 단위: 초 |

### onCallEvent
[](id:onCallEvent)

통화 이벤트 콜백.

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

매개변수 리스트는 다음과 같습니다.

| 매개변수      | 유형    | 의미               |
| --------- | ------- | ------------------ |
| event    | TUICalling.Event  | 통화 이벤트 유형      |
| type | TUICalling.Type | 통화 유형: 오디오/비디오 |
| role | TUICalling.Role | 사용자 역할 유형: 발신자/수신자 |
| message | String | 이벤트 설명 정보 |




