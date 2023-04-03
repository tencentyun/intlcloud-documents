## 기능 설명

이 콜백을 통해 App 백엔드는 사용자의 그룹 생성 요청을 실시간으로 볼 수 있습니다. 백엔드는 사용자의 그룹 생성 요청을 거부할 수 있습니다.

## 주의 사항

- 콜백을 활성화하려면 콜백 URL을 구성하고 콜백 프로토콜을 토글해야 합니다. 구성 방법에 대한 자세한 내용은 [타사 콜백 구성] (https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 콜백 방향은 IM 백엔드가 App 백엔드에 대한 HTTP POST 요청을 시작하는 것입니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL의 SDKAppID가 자체 SDKAppID와 일치하는지 확인해야 합니다.
- 기타 보안 관련 사항은 [타사 콜백 소개: 보안 고려 사항](https://intl.cloud.tencent.com/document/product/1047/34354)을 참고하십시오.

## 콜백 트리거 시나리오

- App 사용자는 클라이언트를 사용하여 그룹을 만듭니다
- App 관리자는 REST API를 통해 그룹을 생성합니다

## 콜백 트리거 시간

IM 백엔드가 그룹 생성을 준비하기 전에 콜백을 수행하십시오.

## API 설명

### 요청 URL 예시

다음 예시에서 App이 구성한 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | 요청 프로토콜은 HTTPS, 요청 방법은 POST                      |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션 생성 시 IM 콘솔에서 할당한 SDKAppID             |
| CallbackCommand | 값은 Group.CallbackBeforeCreateGroup으로 고정                |
| contenttype     | 값은 JSON으로 고정                                           |
| ClientIP        | 클라이언트 IP 주소(예: 127.0.0.1)                            |
| OptPlatform     | 클라이언트 플랫폼, 가능한 값에 대한 정보는 [타사 콜백 소개: 콜백 프로토콜](https://intl.cloud.tencent.com/document/product/1047/34354)에서 OptPlatform에 대한 매개변수 설명 참고 |

### 요청 패킷 예시

```
{
    "CallbackCommand": "Group.CallbackBeforeCreateGroup", // 콜백 명령
    "Operator_Account": "leckie", // 운영자
    "Owner_Account": "leckie", // 그룹 소유자
    "Type": "Public", // 그룹 유형
    "Name": "MyFirstGroup", // 그룹 이름
    "CreateGroupNum": 123, //사용자가 이미 생성한 동일한 유형의 그룹 수
    "MemberList": [ // 초기 구성원 목록
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프
}
```

### 요청 패킷 필드

| 필드             | 유형    | 기능                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | 콜백 명령                                                    |
| Operator_Account | String  | 그룹 생성 요청을 시작한 운영자의 UserID                      |
| Owner_Account    | String  | 요청을 통해 생성할 그룹 소유자의 UserID                      |
| Type             | String  | Public과 같이 그룹 메시지를 생성하는 그룹의 유형, 자세한 내용은 [그룹 시스템](https://intl.cloud.tencent.com/document/product/1047/33529) 참고 |
| Name             | String  | 요청을 통해 생성할 그룹의 이름                               |
| CreateGroupNum   | Integer | 사용자가 이미 생성한 동일한 유형의 그룹 수                   |
| MemberList       | Array   | 배열 요청을 통해 생성될 그룹의 초기 구성원 목록              |
| EventTime        | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프                       |

### 응답 패킷 예시

#### 생성 허용

사용자가 그룹을 만들 수 있도록 허용합니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 생성 허용
}
```

#### 생성 거부

사용자의 그룹 생성 요청을 거부합니다. 이 경우 그룹이 생성되지 않고 오류 코드 `10016`이 호출자에게 반환됩니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 생성 거부
}
```

### 응답 패킷 필드

| 필드         | 유형    | 속성 | 설명                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 필수 | 요청 처리 결과, OK: 성공, FAIL: 실패                         |
| ErrorCode    | Integer | 필수 | 에러 코드, 0: 생성 허용 1: 생성 거부, 비즈니스 측에서 사용자의 요청을 금지하는 에러 코드를 지정하고 클라이언트에게 ErrorCode 및 ErrorInfo를 보내려면 ErrorCode 값이 [10100, 10200] 범위 내로 설정되어 있는지 확인하십시오 |
| ErrorInfo    | String  | 필수 | 오류 정보                                                    |

## 참고

- [3rd party 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [그룹 생성](https://intl.cloud.tencent.com/document/product/1047/34895)
