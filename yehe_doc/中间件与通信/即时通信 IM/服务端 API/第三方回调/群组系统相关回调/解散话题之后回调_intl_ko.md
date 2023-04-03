## 기능 설명

이 콜백을 통해 App 백엔드에서 토픽의 삭제 상태를 실시간으로 볼 수 있습니다. 특히 토픽 삭제에 대한 실시간 로그를 보거나 정보를 다른 시스템과 동기화할 수 있습니다.

## 주의 사항

- 이 콜백을 활성화하려면 URL을 구성해야 합니다. 이 콜백과 그룹 삭제 후 콜백의 콘솔은 동일한 스위치를 사용합니다. 자세한 지침은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [Webhook Overview: 보안 고려 사항](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션을 참고하십시오.
- 토픽 기능은 [기능 설정](https://intl.cloud.tencent.com/document/product/1047/34419) 이후에만 사용할 수 있습니다.

## 콜백 트리거링 시나리오

- App 사용자가 클라이언트에서 토픽을 삭제합니다
- App 관리자는 REST API를 통해 토픽을 삭제합니다

## 콜백 트리거링 타이밍

토픽이 삭제된 후 트리거됩니다

## API 설명

### 요청 URL 예시

다음 샘플에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```json
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | 요청 프로토콜은 HTTPS이고, 요청 방법은 POST                  |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션이 생성될 때 IM 콘솔에서 할당한 SDKAppID         |
| CallbackCommand | 고정값: Group.CallbackAfterTopicDestroyed                    |
| contenttype     | 고정값: JSON                                                 |
| ClientIP        | 클라이언트 IP, 형식: 127.0.0.1                               |
| OptPlatform     | 클라이언트 플랫폼, 유효한 값은 [Webhook Overview: Callback Protocol](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션에서 OptPlatform에 대한 설명 참고 |

### 요청 예시

```json
{
    "CallbackCommand": "Group.CallbackAfterTopicDestroyed", // 콜백 명령
    "GroupId": "@TGS#_@TGS#cQVLVHIM62CJ", // 삭제된 토픽의 그룹 ID
    "Type": "Community", // 그룹 유형
    "TopicIdList":[// 삭제된 토픽 목록
       "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",
       "@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic_1"
    ]
}
```

### 요청 필드

| 객체            | 유형   | 설명                                      |
| --------------- | ------ | ----------------------------------------- |
| CallbackCommand | String | 콜백 명령                                 |
| GroupId         | String | 삭제된 토픽의 그룹                        |
| Type            | String | 삭제된 토픽의 그룹 유형, 여기는 Community |
| TopicIdList     | String | 삭제된 토픽 목록                          |

### 응답 예시
App 백엔드는 토픽 삭제 정보를 기록하고 콜백 응답 패킷을 보냅니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### 응답 필드

| 필드         | 유형    | 속성 | 설명                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 필수 | 요청 결과, OK: 성공 표시, FAIL: 실패 표시                    |
| ErrorCode    | Integer | 필수 | 에러 코드, 0으로 설정하는 것이 좋습니다. 이 콜백은 토픽 삭제를 사용자에게 알리는 데 사용됩니다. 사용자의 오류 코드 값은 삭제 프로세스에 영향을 미치지 않습니다. |
| ErrorInfo    | String  | 필수 | 에러 메시지                                                  |




## 참고

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [토픽 삭제](https://intl.cloud.tencent.com/document/product/1047/49470)
