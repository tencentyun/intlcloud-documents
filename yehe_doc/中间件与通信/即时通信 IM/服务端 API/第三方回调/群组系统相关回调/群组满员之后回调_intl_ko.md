## 기능 설명

App 백엔드는 이 콜백을 사용하여 그룹의 구성원 수가 그룹의 한도에 도달했는지 확인할 수 있습니다. 이 콜백은 비활성 그룹 구성원을 삭제하여 새 구성원을 수락하는 데에도 사용할 수 있습니다.

## 주의 사항

- 이 콜백을 활성화하려면 콜백 URL을 구성하고 해당 프로토콜을 토글해야 합니다. 구성 방법에 대한 자세한 내용은 [Third-Party 콜백 구성](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 콜백 방향은 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 자체 SDKAppID와 일치하는지 확인해야 합니다.
- 기타 보안 관련 문제는 [3rd party 콜백 개요: 보안 고려 사항](https://intl.cloud.tencent.com/document/product/1047/34354)을 참고하십시오.

## 콜백 트리거링 시나리오

- App 사용자가 클라이언트를 통해 그룹 가입을 요청합니다.
- App 사용자는 클라이언트를 통해 그룹에 가입하도록 초대됩니다.
- App 관리자는 REST API를 통해 그룹에 구성원을 추가합니다.

## 콜백 트리거 시간

콜백은 새 구성원이 추가된 후 그룹 구성원 수가 그룹에 대한 제한에 도달하거나 그룹 구성원 수가 제한에 도달하여 그룹에 새 구성원을 추가하지 못한 경우 트리거됩니다.

## API 설명

### 요청 URL 예시

다음 예에서 App에 구성된 콜백 URL은 `https://www.example.com`입니다.
**예시:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 547 / 5,000번역 결과번역 결과요청 매개변수

| 매개변수        | 설명                                                         |
| --------------- | ------------------------------------------------------------ |
| https           | https 요청 프로토콜은 HTTPS이고 요청 방법은 POST             |
| www.example.com | 콜백 URL                                                     |
| SdkAppid        | 애플리케이션 생성 시 IM 콘솔에서 할당한 SDKAppID             |
| CallbackCommand | 값은 Group.CallbackAfterGroupFull로 고정                     |
| contenttype     | 값은 JSON으로 고정                                           |
| ClientIP        | 클라이언트 IP 주소, 형식: 127.0.0.1                          |
| OptPlatform     | 클라이언트 플랫폼. 가능한 값에 대한 자세한 내용은 [3rd party 콜백 개요: 콜백 프로토콜](https://intl.cloud.tencent.com/document/product/1047/34354)의 OptPlatform 매개변수를 참고하십시오. |

### 요청 패킷 예시

```
{
    "CallbackCommand": "Group.CallbackAfterGroupFull", // 콜백 명령
    "GroupId": "@TGS#2J4SZEAEL", // 그룹 ID
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프		
}
```

### 요청 패킷 필드

| 필드            | 유형    | 설명                                   |
| --------------- | ------- | -------------------------------------- |
| CallbackCommand | String  | 콜백 명령                              |
| GroupId         | String  | 만원 그룹의 ID                         |
| EventTime       | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프 |

### 응답 패킷 예시

그룹 구성원 수가 한도에 도달했음을 감지한 후 App 백엔드는 콜백 응답 패킷을 보냅니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 응답의 결과는 무시됩니다
}
```

### 응답 패킷 필드

| 필드         | 유형    | 속성 | 설명                                     |
| ------------ | ------- | ---- | ---------------------------------------- |
| ActionStatus | String  | 필수 | 요청 처리 결과, OK: 성공, FAIL: 실패     |
| ErrorCode    | Integer | 필수 | 에러 코드, 0: 응답에서 결과를 무시합니다 |
| ErrorInfo    | String  | 필수 | 오류 정보                                |


## 참고

- [3rd party 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [그룹 구성원 삭제](https://intl.cloud.tencent.com/document/product/1047/34949)
- REST API: [그룹 구성원 추가](https://intl.cloud.tencent.com/document/product/1047/34921)
