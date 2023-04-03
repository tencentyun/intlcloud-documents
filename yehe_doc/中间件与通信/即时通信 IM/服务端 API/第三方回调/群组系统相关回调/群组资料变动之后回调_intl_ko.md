## 기능 설명
App 백엔드는 이 콜백을 사용하여 그룹 정보(그룹 이름, 그룹 소개, 그룹 알림 및 프로필 사진 포함)의 변경 사항을 실시간으로 확인하고, 여기에는 그룹 정보의 변경 사항을 실시간으로 기록하는 것(예: 로그 기록 또는 변경 사항을 다른 시스템과 동기화)이 포함됩니다.

## 주의 사항

- 이 콜백을 활성화하려면 콜백 URL을 구성하고 해당 프로토콜을 토글해야 합니다. 구성 방법에 대한 자세한 내용은 [Third-Party 콜백 구성](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 콜백 방향은 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 자체 SDKAppID와 일치하는지 확인해야 합니다.
- 기타 보안 관련 문제는 [3rd party 콜백 개요: 보안 고려 사항](https://intl.cloud.tencent.com/document/product/1047/34354)을 참고하십시오.

## 콜백 트리거 시나리오

### 콜백을 트리거할 수 있는 콘텐츠

콜백 트리거 시나리오콜백을 트리거할 수 있는 콘텐츠 그룹 정보에는 [기본 그룹 정보](https://intl.cloud.tencent.com/document/product/1047/33529)와 [그룹별 사용자 정의 필드](https://intl.cloud.tencent.com/document/product/1047/33529)가 있습니다.
현재 이 콜백은 그룹 이름, 그룹 소개, 그룹 알림 또는 프로필 사진 URL이 수정될 때 트리거될 수 있습니다. 이 콜백은 다른 기본 그룹 정보가 수정되면 트리거되지 않습니다.

### 콜백 트리거 시나리오

- App 사용자는 클라이언트를 통해 그룹 정보를 수정합니다.
- App 관리자는 REST API를 통해 그룹 정보를 수정합니다.

## 콜백 트리거 시간

콜백은 기본 그룹 정보가 수정된 후에 트리거됩니다.

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
| CallbackCommand | 값은 Group.CallbackAfterGroupInfoChanged로 고정              |
| contenttype     | 값은 JSON으로 고정                                           |
| ClientIP        | 클라이언트 IP 주소, 형식: 127.0.0.1                          |
| OptPlatform     | 클라이언트 플랫폼. 가능한 값에 대한 자세한 내용은 [3rd party 콜백 개요: 콜백 프로토콜](https://intl.cloud.tencent.com/document/product/1047/34354)의 OptPlatform 매개변수를 참고하십시오. |

### 요청 패킷 예시

```
{
    "CallbackCommand": "Group.CallbackAfterGroupInfoChanged", // 콜백 명령
    "GroupId" : "@TGS#2J4SZEAEL",
    "Type": "Public", // 그룹 유형
    "Operator_Account": "leckie", // 운영자
    "Notification": "NewNotification", // 수정된 그룹 공지
    "EventTime":"1670574414123"//밀리초 수준, 이벤트 트리거 타임스탬프		
}
```



### 요청 패킷 필드

| 필드             | 유형    | 설명                                                         |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | 콜백 명령                                                    |
| GroupId          | String  | 정보가 수정된 그룹의 ID                                      |
| Type             | String  | Public과 같이 정보가 수정된 그룹의 유형입니다. 자세한 내용은 [그룹 유형](https://intl.cloud.tencent.com/document/product/1047/33529)을 참고하십시오. |
| Operator_Account | String  | 운영자의 UserID                                              |
| Name             | String  | 변경된 그룹 이름                                             |
| Introduction     | String  | 변경된 그룹 소개                                             |
| Notification     | String  | 변경된 그룹 공지                                             |
| FaceUrl          | String  | 변경된 단체 프로필 사진 URL                                  |
| EventTime        | Integer | 이벤트 트리거의 밀리초 수준 타임스탬프                       |

### 응답 패킷 예시

그룹 정보 변경 사항을 기록한 후 App 백엔드는 콜백 응답 패킷을 보냅니다.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0  // 응답에서 결과 무시
}
```

### 응답 패킷 필드

| 필드         | 유형    | 속성 | 설명                                                |
| ------------ | ------- | ---- | --------------------------------------------------- |
| ActionStatus | String  | 필수 | 요청 처리 결과, OK: 성공, FAIL: 실패.               |
| ErrorCode    | Integer | 필수 | 에러 코드, 0 값은 응답의 결과가 무시됨을 나타냅니다 |
| ErrorInfo    | String  | 필수 | 오류 정보                                           |

## 참고

- [3rd party 콜백 소개](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [그룹 기본 정보 변경](https://intl.cloud.tencent.com/document/product/1047/34962)
