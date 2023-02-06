## 기능 설명

이 API는 App 백엔드에서 다음을 포함하여 사용자의 그룹 메시지를 실시간으로 보는 데 사용됩니다.
-  예를 들어 로그를 기록하거나 다른 시스템에 메시지를 동기화하여 실시간으로 그룹 메시지를 기록합니다.
-  그룹에서 메시지를 보내려는 사용자의 요청을 차단합니다.
>! 메시지 전 콜백은 기본적으로 2s의 시간 초과로 설정되며 조정하지 않는 것이 좋습니다. 콘텐츠 조정은 이전 콜백을 사용하여 처리되며 이로 인해 전체 이전 콜백이 시간 초과될 수 있습니다. 콘텐츠 조정이 필요한 경우 콘텐츠 콜백을 사용하십시오. 자세한 내용은 [콘텐츠 보안 시나리오](https://www.tencentcloud.com/document/product/1047/52498)를 참고하십시오.

## 주의 사항

-  이 콜백을 활성화하려면 콜백 URL을 구성하고 이 콜백에 해당하는 스위치를 활성화해야 합니다. 설정 방법에 대한 자세한 내용은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
-  이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [타사 콜백 개요](https://intl.cloud.tencent.com/document/product/1047/34354)의 보안 고려 사항 섹션을 참고하십시오.

## 콜백 트리거 시나리오

-  App 사용자는 클라이언트에서 그룹 메시지를 보냅니다.
-  App 관리자는 REST API 호출을 통해 그룹 메시지를 보냅니다.

## 콜백 트리거 시간

콜백은 IM 백엔드가 그룹 구성원에게 그룹 메시지를 보내기 전에 트리거됩니다.

## API 설명

### 요청 예시 URL

다음 예시에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수     | 설명 |
| --- | --- |
| https | 요청 프로토콜은 HTTPS이고 요청 방법은 POST |
| www.example.com | 콜백 URL |
| SdkAppid | 애플리케이션 생성 시 IM 콘솔에서 할당된 SDKAppID |
| CallbackCommand | 값은 항상 Group.CallbackBeforeSendMsg |
| contenttype | 값은 항상 JSON |
| ClientIP | 클라이언트의 IP 주소(예: 127.0.0.1) |
| OptPlatform | 클라이언트의 플랫폼. 유효한 값에 대한 자세한 내용은 [타사 콜백 개요](https://intl.cloud.tencent.com/document/product/1047/34354)의 콜백 프로토콜 섹션에서 OptPlatform 설명 참고 |

### 요청 예시

```
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // 콜백 명령
    "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
    "Type": "Community", // 그룹 유형
    "From_Account": "jared", // 발신자
    "Operator_Account":"admin", // 요청 개시자
    "Random": 123456, // 랜덤 숫자
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
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// 주제의 ID, 이 옵션은 주제 기능을 지원하는 커뮤니티에서만 사용할 수 있습니다
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프		
}
```

### 응답 필드

| 필드 | 유형 | 설명|
| --- | --- | --- |
| CallbackCommand | String | 콜백 명령 |
| GroupId | String | 그룹 메시지를 생성하는 그룹의 ID |
| Type | String | Public과 같이 그룹 메시지를 생성하는 그룹의 유형이며, 자세한 내용은 [그룹 유형](https://intl.cloud.tencent.com/document/product/1047/33529) 참고 |
| From_Account | String | 메시지 발신자의 UserID |
| Operator_Account | String | 관리자가 요청을 시작했는지 여부를 시스템에서 식별할 수 있는 요청 개시자의 UserID |
| Random | Integer | 요청의 32비트 난수 |
|OnlineOnlyFlag|Integer|값은 온라인 메시지인 경우 1이고 그렇지 않은 경우 0(기본값)입니다. 오디오/비디오 그룹의 경우 값은 0입니다.|
| MsgBody | Array | 메시지 본문, 자세한 내용은 [메시지 형식](https://intl.cloud.tencent.com/document/product/1047/33527) 참고 |
| CloudCustomData | String | 메시지 사용자 지정 데이터(클라우드에 저장되고 피어 측으로 전송되며 프로그램을 언로드하고 다시 설치한 후에도 데이터를 가져올 수 있음) |
|TopicId|String|주제의 ID, 이 옵션은 주제 기능을 지원하는 커뮤니티에서만 사용|
| EventTime | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프 |

### 응답 예시

#### 그룹 메시지 전송 허용

사용자는 그룹 메시지를 보낼 수 있으며 메시지 내용은 수정되지 않습니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 0은 사용자가 그룹 메시지를 보낼 수 있음을 나타냅니다
}
```

#### 그룹 메시지 전송 금지

사용자는 그룹 메시지를 보낼 수 없습니다. 이 경우 메시지가 전송되지 않고 호출자에게 에러 코드 `10016`이 반환됩니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 1은 사용자가 그룹 메시지를 보낼 수 없음을 나타냅니다
}
```

#### 자동으로 메시지 삭제

사용자는 그룹 메시지를 보낼 수 없습니다. 이 경우 메시지가 전송되지 않지만 호출자에게 성공 메시지가 반환됩니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 2 // 2는 메시지가 자동으로 삭제됨을 나타냅니다
}
```

#### 메시지 내용 수정

다음 응답 예시에서는 사용자가 보낸 그룹 메시지가 수정되고(사용자 지정 메시지가 추가됨) IM 백엔드가 수정된 메시지를 보냅니다. 이 기능을 통해 App 백엔드는 사용자가 보낸 메시지에 사용자 수준 및 제목과 같은 특수 콘텐츠를 추가할 수 있습니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // 이 필드는 0으로 설정해야 수정된 메시지가 정상적으로 전송될 수 있습니다
    "MsgBody": [ // App 백엔드에서 수정한 메시지, App 백엔드가 메시지를 수정하지 않으면 기본적으로 사용자가 보낸 메시지가 사용됩니다
        {
            "MsgType": "TIMTextElem", // 텍스트
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // 사용자 지정 메시지
            "MsgContent": {
                "Desc": "CustomElement.MemberLevel", // 설명
                "Data": "LV1" // 데이터
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

### 응답 필드

| 필드 | 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | 요청 처리 결과. OK: 성공, FAIL: 실패 |
| ErrorCode | Integer | Yes | 오류 코드가 반환되었습니다. 0: 그룹 메시지 전송 허용; 1: 그룹 메시지 전송 금지; 2: 메시지를 조용히 버립니다. 비즈니스 측에서 사용자가 그룹 메시지를 보내고 클라이언트에 ErrorCode 및 ErrorInfo를 보내는 것을 금지하려면 ErrorCode 값이 [10100, 10200] 범위 내로 설정되었는지 확인하십시오. |
| ErrorInfo | String | Yes | 오류 정보 |
| MsgBody | Array | No | App 백엔드에서 수정한 메시지 본문입니다. IM 백엔드는 수정된 메시지를 그룹에 보냅니다. 형식에 대한 자세한 내용은 [메시지 형식](https://intl.cloud.tencent.com/document/product/1047/33527)을 참고하십시오. |
| CloudCustomData | String |  No | 메시지 사용자 지정 데이터(클라우드에 저장되고 피어 측으로 전송되며 프로그램을 언로드하고 다시 설치한 후에도 데이터를 가져올 수 있음) |


## 참고

- [3rd party 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [그룹에서 일반 메시지 보내기](https://intl.cloud.tencent.com/document/product/1047/34959)

