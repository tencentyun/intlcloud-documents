## 기능 설명

이 API는 App 백엔드에서 사용자의 그룹 메시지를 실시간으로 보는 데 사용됩니다. App 백엔드는 그룹 메시지가 성공적으로 전송되면 알림을 받을 수 있으며 필요에 따라 데이터를 동기화할 수 있습니다.

## 주의 사항

-  이 콜백을 활성화하려면 콜백 URL을 구성하고 이 콜백에 해당하는 스위치를 활성화해야 합니다. 설정 방법에 대한 자세한 내용은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
-  이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [타사 콜백 개요](https://intl.cloud.tencent.com/document/product/1047/34354)의 보안 고려 사항 섹션을 참고하십시오.

## 콜백 트리거 시나리오

-  App 사용자는 클라이언트에서 그룹 메시지를 보냅니다.
-  App 관리자는 REST API 호출을 통해 그룹 메시지를 보냅니다.

## 콜백 트리거 시간

콜백은 그룹 메시지가 성공적으로 전송된 후 트리거됩니다.

## API 호출 설명

### 요청 예시 URL

다음 샘플에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | 요청 프로토콜은 HTTPS이고 요청 방법은 POST                   |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션 생성 시 IM 콘솔에서 할당된 SDKAppID             |
| CallbackCommand | 값은 항상 Group.CallbackAfterSendMsg                         |
| contenttype     | 값은 항상 JSON                                               |
| ClientIP        | 클라이언트의 IP 주소(예: 127.0.0.1)                          |
| OptPlatform     | 클라이언트의 플랫폼. 유효한 값에 대한 자세한 내용은 [타사 콜백 개요](https://intl.cloud.tencent.com/document/product/1047/34354)의 콜백 프로토콜 섹션에서 OptPlatform 설명 참고 |

### 요청 예시

```
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // 콜백 명령
    "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
    "Type": "Public", // 그룹 유형
    "From_Account": "jared", // 발신자
    "Operator_Account":"admin", // 요청자
    "Random": 123456, // 랜덤 숫자
    "MsgSeq": 123, // 메시지의 시퀀스 번호
    "MsgTime": 1490686222, // 메시지 시간
    "OnlineOnlyFlag": 1, // 값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다.
    "MsgBody": [ // 메시지 본문, 자세한 내용은 TIMMessage 메시지 객체 참고
        {
            "MsgType": "TIMTextElem", // 텍스트
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data",
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프		
}
```

### 요청 필드

| 필드             | 유형    | 설명                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | 콜백 명령                                                    |
| GroupId          | String  | 그룹 메시지를 생성하는 그룹의 ID                             |
| Type             | String  | Public과 같이 그룹 메시지를 생성하는 그룹의 유형입니다. 자세한 내용은 [그룹 유형](https://intl.cloud.tencent.com/document/product/1047/33529) 참고 |
| From_Account     | String  | 메시지 발신자의 UserID                                       |
| Operator_Account | String  | 관리자가 요청을 시작했는지 여부를 시스템에서 식별할 수 있는 요청 개시자의 UserID |
| Random           | Integer | 임의 정수 요청의 32비트 임의 숫자                            |
| MsgSeq           | Integer | 메시지를 고유하게 식별하는 메시지 시퀀스 번호 <br>그룹 메시지는 MsgSeq별로 정렬되며, MsgSeq 값이 클수록 메시지 순위가 낮아집니다 |
| MsgTime          | Integer | 백엔드 Server 시간에 해당하는 메시지 전송 타임스탬프         |
| OnlineOnlyFlag   | Integer | 값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다. |
| MsgBody          | Array   | 메시지 본문, 자세한 내용은 [메시지 형식](https://intl.cloud.tencent.com/document/product/1047/33527) 참고 |
| CloudCustomData  | String  | 메시지 사용자 지정 데이터(클라우드에 저장되고 피어 측으로 전송되며 프로그램을 언로드하고 다시 설치한 후에도 데이터를 가져올 수 있음) |
| TopicId          | String  | 주제의 ID, 이 옵션이 있으면 해당 주제로 발언한다는 의미이며, 주제 기능을 지원하는 커뮤니티에서만 사용 |
| EventTime        | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프                       |

### 응답 예시

App 백엔드가 데이터를 동기화한 후 응답이 전송됩니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //콜백 결과 무시
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
- REST API: [그룹에서 일반 메시지 보내기](https://intl.cloud.tencent.com/document/product/1047/34959)
