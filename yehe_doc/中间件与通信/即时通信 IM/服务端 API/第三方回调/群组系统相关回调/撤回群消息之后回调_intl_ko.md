## 기능 설명

이 API는 App 백엔드에서 실시간으로 그룹 메시지 회수를 보는 데 사용됩니다.

## 주의 사항

- 이 콜백을 활성화하려면 콜백 URL을 구성하고 이 콜백에 해당하는 스위치를 활성화해야 합니다. 설정 방법에 대한 자세한 내용은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [타사 콜백 개요](https://intl.cloud.tencent.com/document/product/1047/34354)의 보안 고려 사항 섹션을 참고하십시오.

## 콜백 트리거 시나리오

- App 사용자는 클라이언트에서 그룹 메시지를 회수합니다.
- App 관리자는 REST API를 호출하여 그룹 메시지를 회수합니다.

## 콜백 트리거 타이밍

그룹 메시지가 성공적으로 회수된 후.

## API 설명

### 요청 예시 URL

다음 예시에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | 요청 프로토콜은 HTTPS, 요청 방식은 POST                      |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션 생성 시 IM 콘솔에서 할당한 SDKAppID             |
| CallbackCommand | 값은 Group.CallbackAfterRecallMsg로 고정                     |
| contenttype     | 값은 JSON으로 고정                                           |
| ClientIP        | 클라이언트 IP 주소(예: 127.0.0.1)                            |
| OptPlatform     | 클라이언트 플랫폼, 유효한 값은 [타사 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)의 콜백 프로토콜 섹션에서 OptPlatform 설명 참고 |

### 요청 예시

```
{
    "CallbackCommand":"Group.CallbackAfterRecallMsg", // 콜백 명령
    "Operator_Account":"admin", // 운영자
    "Type":"Community", // 그룹 유형
    "GroupId":"1213456", // 그룹 ID
    "MsgSeqList":[ // 회수된 메시지의 MsgSeq 목록           
        {"MsgSeq":130}
    ],
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// 주제의 ID, 이 옵션은 주제 기능을 지원하는 커뮤니티에서만 사용 가능
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프		
}
```

### 요청 필드

| 객체             | 유형    | 설명                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | 콜백 명령                                                    |
| Operator_Account | String  | 그룹 메시지를 회수한 운영자의 UserID                         |
| Type             | String  | Public과 같이 그룹 메시지를 생성하는 그룹의 유형, 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529)의 그룹 유형 섹션 참고 |
| GroupId          | String  | 그룹 ID                                                      |
| MsgSeqList       | Array   | 회수된 메시지의 MsgSeq 목록                                  |
| TopicId          | String  | 주제의 ID, 이 옵션은 주제 기능을 지원하는 커뮤니티에서만 사용 가능 |
| EventTime        | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프                       |

### 응답 예시

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 0 값은 콜백 결과가 무시됨을 나타냅니다
}
```

### 응답 필드

| 필드         | 유형    | 필수 | 설명                                      |
| ------------ | ------- | ---- | ----------------------------------------- |
| ActionStatus | String  | Yes  | 요청 결과, OK: 성공, FAIL: 실패           |
| ErrorCode    | Integer | Yes  | 에러 코드, 값 0은 콜백 결과가 무시됨 표시 |
| ErrorInfo    | String  | Yes  | 오류 정보                                 |

## 참고

- [3rd party 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [그룹 메시지 회수](https://intl.cloud.tencent.com/document/product/1047/34965)
