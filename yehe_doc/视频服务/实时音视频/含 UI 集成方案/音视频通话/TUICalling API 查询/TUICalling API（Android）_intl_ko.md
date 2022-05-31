TUICalling은 두 개의 폐쇄 소스 SDK인 Tencent Cloud Real-Time Communication(TRTC) 및 Instant Messaging(IM)을 기반으로 하는 오픈 소스 Class입니다. 1v1 및 그룹 화상 통화를 지원합니다. 구현 방법에 대한 자세한 지침은 [영상 통화(Android)](https://intl.cloud.tencent.com/document/product/647/36066)를 참고하십시오.

- TRTC SDK: [TRTC SDK](https://intl.cloud.tencent.com/document/product/647)를 저지연 멀티미디어 통화 컴포넌트로 사용합니다.
- IM SDK: [IM SDK](https://intl.cloud.tencent.com/document/product/1047)를 사용하여 신호 메시지를 발송 및 처리합니다.

## TUICalling API 개요

#### SDK 기본 API

| API                                                          | 설명                  |
| :----------------------------------------------------------- | :------------------------ |
| [sharedInstance](https://intl.cloud.tencent.com/document/product/647/43140) | 컴포넌트 싱글톤                  |
| [call](https://intl.cloud.tencent.com/document/product/647/43140) | C2C 통화 초대 보내기              |
| [setCallingListener](https://intl.cloud.tencent.com/document/product/647/43140) | 리스너 설정.              |
| [setCallingBell](https://intl.cloud.tencent.com/document/product/647/43140) | 벨소리 설정(30초 이내 권장) |
| [enableMuteMode](https://intl.cloud.tencent.com/document/product/647/43140) | 음소거 모드 활성화/비활성화              |
| [enableCustomViewRoute](https://intl.cloud.tencent.com/document/product/647/43140) | 사용자 정의 뷰 활성화            |

## TUICallingListener API 개요

#### 이벤트 콜백

| API                                             | 설명                                                         |
| :----------------------------------------------------------- | :------------------------------- |
| [shouldShowOnCallView](https://intl.cloud.tencent.com/document/product/647/43140) | 전화 수신 시 응답 페이지 표시           |
| [onCallStart](https://intl.cloud.tencent.com/document/product/647/43140) | 발신자와 수신자 모두에 대해 트리거되는 호출 시작 콜백 |
| [onCallEnd](https://intl.cloud.tencent.com/document/product/647/43140) | 발신자와 수신자 모두에 대해 트리거되는 통화 종료 콜백     |
| [onCallEvent](https://intl.cloud.tencent.com/document/product/647/43140) | 이벤트 콜백 호출                     |

## Type API 개요

#### 통화 유형

| enum  | 설명     |
| :---- | :------- |
| AUDIO | 음성 통화 |
| VIDEO | 영상 통화 |

## Role API 개요

#### 사용자 역할 유형

| enum   | 설명               |
| :----- | :----------------- |
| CALL   | 통화 발신자 |
| CALLED | 통화 수신자 |

## Event API 개요

#### 이벤트 유형

| enum         | 설명         |
| :----------- | :----------- |
| CALL_START   | 통화 시작     |
| CALL_SUCCEED | 통화 연결 성공 |
| CALL_END     | 통화 종료     |
| CALL_FAILED  | 통화 실패     |

## 기본 SDK API

### sharedInstance

sharedInstance는 TUICalling 컴포넌트 싱글톤입니다.

```java
public static TUICallingImpl sharedInstance();
```

### call

C2C 통화 초대.


```java
void call(String[] userIDs, Type type);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형            | 의미                |
| :------ | :-------------- | :------------------ |
| userIDs | String[]        | 통화 참가자의 사용자 ID 리스트    |
| type    | TUICalling.Type | 통화 유형: 오디오/비디오 |

### setCallingListener
리스너 설정.


```java
void setCallingListener(TUICallingListener listener);
```

매개변수는 다음과 같습니다.

| 매개변수     | 유형               | 의미                  |
| :------- | :----------------- | :-------------------- |
| listener    | TUICallingListener  | TUIcalling 컴포넌트 리스너  |

### setCallingBell

벨소리 설정(30초 이내 권장).

```java
void setCallingBell(String filePath);
```



매개변수는 다음과 같습니다.

| 매개변수     | 유형   | 의미         |
| :------- | :----- | :----------- |
| filePath    | String  | 벨소리 파일의 경로   |

### enableMuteMode

음소거 모드 활성화.

```java
void enableMuteMode(boolean enable);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미             |
| :----- | :------ | :--------------- |
| enable    | boolean  | 음소거 모드 활성화 여부   |

### enableCustomViewRoute

사용자 정의 뷰 활성화.
활성화 후 발신/수신 시작 콜백 중 CallingView 인스턴스가 수신되며 개발자가 직접 표시 방법을 결정합니다.

>! 보기는 전체 화면으로 표시되거나 화면 크기에 비례하여 표시되어야 합니다. 그렇지 않으면 오류가 발생할 수 있습니다.

```java
void enableCustomViewRoute(boolean enable);
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미             |
| :----- | :------ | :----------------- |
| enable    | boolean  | 사용자 정의 뷰 활성화 여부   |

## TUICallingListener 콜백 API

### shouldShowOnCallView

수신 전화가 있을 때 응답 페이지 표시 여부에 대한 콜백입니다.

```java
boolean shouldShowOnCallView();
```

매개변수는 다음과 같습니다.

| 매개변수   | 유형    | 의미     |
| :----- | :------ | :------- |
| 반환 값    | boolean  |  동의 여부   |

### onCallStart

호출자와 수신자 모두에 대해 트리거되는 호출 시작 콜백입니다.

```java
 void onCallStart(String[] userIDs, TUICalling.Type type, TUICalling.Role role, View tuiCallingView);
```

매개변수는 다음과 같습니다.

| 매개변수             | 유형               | 의미                               |
| :------------- | :-------------- | :----------------------------------------------------------- |
| userIDs        | String[]        | 통화 참가자의 사용자 ID 목록.                                           |
| type           | TUICalling.Type | 통화 유형: 음성/영상                                          |
| role           | TUICalling.Role | 역할 유형: 발신자/수신자                                      |
| tuiCallingView | View | 통화 View. enableCustomViewRoute가 false일 때 view는 null |

### onCallEnd

발신자와 수신자 모두에 대해 트리거되는 통화 종료 콜백입니다.

```java
 void onCallEnd(String[] userIDs, TUICalling.Type type, TUICalling.Role role, long totalTime);
```

매개변수는 다음과 같습니다.

| 매개변수      | 유형           | 의미                    |
| :-------- | :-------------- | :---------------------- |
| userIDs    | String[]  | 통화 참가자의 사용자 ID 목록      |
| type      | TUICalling.Type | 통화 유형: 음성/영상     |
| role      | TUICalling.Role | 역할 유형: 발신자/수신자 |
| totalTime | long            | 통화 시간, 단위: 초      |

### onCallEvent

통화 이벤트 콜백입니다.

```java
void onCallEvent(TUICalling.Event event, TUICalling.Type type, TUICalling.Role role, String message);
```

매개변수는 다음과 같습니다.

| 매개변수    | 유형             | 의미                    |
| :------ | :--------------- | :---------------------- |
| event   | TUICalling.Event | 통화 이벤트 유형            |
| type    | TUICalling.Type  | 통화 유형: 음성/영상     |
| role    | TUICalling.Role  | 역할 유형: 발신자/수신자 |
| message | String           | 이벤트 설명          |