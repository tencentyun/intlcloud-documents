## 기능 설명

이 콜백을 통해 App 백엔드에서 실시간으로 사용자의 토픽 생성 요청을 볼 수 있습니다. 또한 App 백엔드는 요청을 거부할 수 있습니다.

## 주의 사항

- 이 콜백을 활성화하려면 콜백 URL을 구성해야 합니다. 이 콜백과 그룹 생성 전 콜백은 동일한 스위치를 사용합니다. 자세한 지침은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [Webhook Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션을 참고하십시오.
- 토픽 기능은 [기능 설정](https://intl.cloud.tencent.com/document/product/1047/34419) 이후에만 사용 가능합니다.

## 콜백 트리거링 시나리오

- App 사용자는 클라이언트에서 토픽을 생성합니다
- App 관리자는 REST API를 통해 토픽을 생성합니다

## 콜백 트리거링 타이밍

IM 백엔드가 토픽을 생성하기 전에 트리거됩니다.

## API 설명

### 요청 URL 예시

다음 예시에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
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
| CallbackCommand | 고정 값: Group.CallbackBeforeCreateTopic                     |
| contenttype     | 고정 값: JSON                                                |
| ClientIP        | 클라이언트 IP, 형식: 127.0.0.1                               |
| OptPlatform     | 클라이언트 플랫폼, 유효한 값은 [Webhook Overview: Callback Protocol](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션에서 OptPlatform에 대한 설명 참고 |

### 요청 예시

```json
{
    "CallbackCommand": "Group.CallbackBeforeCreateTopic", // 콜백 명령
    "Operator_Account": "leckie", // 운영자
    "Type": "Community", // 그룹 유형
    "Name": "MyFirstTopic" // 그룹 이름
}
```

### 요청 필드

| 객체             | 유형   | 설명                                    |
| ---------------- | ------ | --------------------------------------- |
| CallbackCommand  | String | 콜백 명령                               |
| Operator_Account | String | 토픽 생성 요청을 시작한 운영자의 UserID |
| Type             | String | 토픽의 그룹 유형, 여기는 Community      |
| Name             | String | 생성을 요청한 토픽의 이름               |

### 응답 예시

#### 생성 허용됨

사용자는 토픽을 만들 수 있습니다.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 생성 허용됨
}
```

#### 생성 거부됨

사용자는 토픽을 만들 수 없습니다. 토픽가 생성되지 않으며 호출자에게 에러 코드 `10016`이 반환됩니다.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 생성 거부됨
}
```

### 응답 필드

| 필드         | 유형    | 속성 | 설명                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 필수 | 요청 결과, OK: 성공 표시, FAIL: 실패 표시                    |
| ErrorCode    | Integer | 필수 | 에러 코드, 유효한 값: 0: 생성 허용; 1: 생성이 거부됨, 고유한 에러 코드를 사용하여 토픽 생성에 대한 사용자 요청을 거부하려면 [10100,10200] 범위의 ErrorCode와 함께 ErrorCode 및 ErrorInfo를 클라이언트에 전달해야 합니다 |
| ErrorInfo    | String  | 필수 | 에러 메시지                                                  |

## 참고

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [토픽 생성](https://intl.cloud.tencent.com/document/product/1047/49471)
