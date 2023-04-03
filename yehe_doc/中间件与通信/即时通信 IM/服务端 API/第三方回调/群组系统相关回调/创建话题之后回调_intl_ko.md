## 기능 설명

이 콜백을 통해 App 백엔드에서 사용자가 생성한 토픽의 정보를 실시간으로 볼 수 있습니다. 특히 백엔드가 데이터를 동기화할 수 있도록 App 백엔드에 성공적인 토픽 생성을 알립니다.

## 주의 사항

- 이 콜백을 활성화하려면 콜백 URL을 구성해야 합니다. 이 콜백과 그룹 생성 후 콜백은 동일한 스위치를 사용합니다. 자세한 지침은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [Webhook Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션을 참고하십시오.
- 토픽 기능은 [기능 설정](https://intl.cloud.tencent.com/document/product/1047/34419) 이후에만 사용 가능합니다.

## 콜백 트리거링 시나리오

- App 사용자가 클라이언트에서 토픽 생성 성공
- App 관리자가 RESTful API를 통해 토픽 생성 성공

## 콜백 트리거링 타이밍

토픽가 성공적으로 생성된 후 트리거됩니다.

## API 설명

### 요청 URL 예시

다음 예시에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | 요청 프로토콜은 HTTPS이고 요청 방법은 POST                   |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션 생성 시 IM 콘솔에서 할당한 SDKAppID             |
| CallbackCommand | 고정 값: Group.CallbackAfterCreateTopic                      |
| contenttype     | 고정 값: JSON                                                |
| ClientIP        | 클라이언트 IP，형식: 127.0.0.1                               |
| OptPlatform     | 클라이언트 플랫폼, 유효한 값은 [Webhook Overview: Callback Protocol](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션에서 OptPlatform에 대한 설명 참고 |

### 요청 예시

```json
 {
    "CallbackCommand": "Group.CallbackAfterCreateTopic", // 콜백 명령
    "GroupId" : "@TGS#2J4SZEAEL",
    "TopicId"	: "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5",
    "Operator_Account": "group_root", // 운영자
    "Owner_Account": "leckie", // 그룹 소유자
    "Type": "Community", // 그룹 유형
    "Name": "MyFirstTopic", // 토픽 이름
    "UserDefinedDataList": [ //사용자가 토픽을 생성할 때 사용할 사용자 정의 필드
        {
            "Key": "UserDefined1",
            "Value": "hello"
        },
        {
            "Key": "UserDefined2",
            "Value": "world"
        }
    ]
}
```

### 요청 필드

| 필드                | 유형   | 설명                                                         |
| ------------------- | ------ | ------------------------------------------------------------ |
| CallbackCommand     | String | 콜백 명령                                                    |
| GroupId             | String | 토픽의 그룹 ID                                               |
| TopicId             | string | 토픽 ID                                                      |
| Operator_Account    | String | 토픽 생성 요청을 시작한 운영자의 UserID                      |
| Owner_Account       | String | 그룹 소유자의 사용자 ID                                      |
| Type                | String | 토픽의 그룹 유형, 여기는 Community                           |
| Name                | String | 생성을 요청한 토픽의 이름                                    |
| UserDefinedDataList | Array  | 사용자가 토픽을 만들 때 사용할 사용자 정의 필드, 이 필드는 기본적으로 사용할 수 없으며 [그룹 시스템](https://www.tencentcloud.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5)의 지침에 따라 활성화해야 합니다 |

### 응답 예시

App 백엔드가 데이터를 동기화한 후 응답이 전송됩니다.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 값 0은 콜백 결과가 무시됨 표시
}
```

### 응답 필드

| 필드         | 유형    | 속성 | 설명                                      |
| ------------ | ------- | ---- | ----------------------------------------- |
| ActionStatus | String  | 필수 | 요청 결과, OK: 성공 표시, FAIL: 실패 표시 |
| ErrorCode    | Integer | 필수 | 에러 코드, 값 0은 콜백 결과가 무시됨 표시 |
| ErrorInfo    | String  | 필수 | 에러 메시지                               |

## 참고
- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [Creating Topic](https://intl.cloud.tencent.com/document/product/1047/49471)
