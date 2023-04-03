## 기능 설명
이 콜백을 통해 App 백엔드에서 토픽 프로필(토픽 이름, 토픽 소개, 토픽 공지 및 토픽 프로필 사진)의 변경 사항을 실시간으로 볼 수 있습니다. 특히 변경된 토픽 프로필의 실시간 로그를 보거나 다른 시스템과 정보를 동기화할 수 있습니다.

## 주의 사항

- 이 콜백을 활성화하려면 URL을 구성해야 합니다. 이 콜백과 그룹 프로필 수정 후 콜백의 콘솔은 동일한 스위치를 사용합니다. 자세한 지침은 [콜백 설정](https://intl.cloud.tencent.com/document/product/1047/34520)을 참고하십시오.
- 이 콜백 중에 IM 백엔드는 App 백엔드에 대한 HTTP POST 요청을 시작합니다.
- 콜백 요청을 받은 후 App 백엔드는 요청 URL에 포함된 SDKAppID가 앱의 SDKAppID인지 확인해야 합니다.
- 보안 고려 사항에 대한 자세한 내용은 [Webhook Overview: 보안 고려 사항](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션을 참고하십시오.
- 토픽 기능은 [기능 설정](https://intl.cloud.tencent.com/document/product/1047/34419) 이후에만 사용할 수 있습니다.

## 콜백 트리거링 시나리오

### 콜백 트리거 콘텐츠

토픽 프로필에는 기본 토픽 프로필과 사용자 정의 토픽 필드가 포함됩니다.
현재 이 콜백은 토픽 이름, 토픽 소개, 토픽 공지 또는 토픽 프로필 사진 URL의 변경에 의해 트리거될 수 있으며 다른 기본 토픽 프로필의 변경에 의해 트리거되지 않습니다.

### 콜백 트리거 방법

- App 사용자는 클라이언트에서 토픽 프로필을 수정합니다.
- App 관리자는 REST API를 통해 토픽 프로필을 수정합니다.

## 콜백 트리거링 타이밍

토픽 프로필이 변경된 후에 트리거됩니다.

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
| CallbackCommand | 고정 값: Group.CallbackAfterTopicInfoChanged                 |
| contenttype     | 고정 값: JSON                                                |
| ClientIP        | 클라이언트 IP, 형식: 127.0.0.1                               |
| OptPlatform     | 클라이언트 플랫폼, 유효한 값은 [Webhook Overview: Callback Protocol](https://intl.cloud.tencent.com/document/product/1047/34354) 섹션에서 OptPlatform에 대한 설명 참고 |

### 요청 예시

```json
{
    "CallbackCommand": "Group.CallbackAfterTopicInfoChanged", // 콜백 명령
    "GroupId" : "@TGS#2J4SZEAEL",// 변경된 토픽 프로필의 그룹 ID
    "Type": "Community", // 그룹 유형
    "Operator_Account": "leckie", // 운영자
    "Name":"TestTopic", // 변경된 토픽 이름
    "Introduction": "TestIntroduction", //변경된 토픽 소개
    "Notification": "NewNotification", // 변경된 토픽 알림
    "FaceUrl": "http://this.is.face.url"// 변경된 토픽 프로필 사진 URL
}
```

### 요청 필드

| 필드             | 유형   | 설명                                      |
| ---------------- | ------ | ----------------------------------------- |
| CallbackCommand  | String | 콜백 명령                                 |
| GroupId          | String | 변경된 토픽 프로필의 그룹 ID              |
| Type             | String | 삭제된 토픽의 그룹 유형, 여기는 Community |
| Operator_Account | String | 운영자의 UserID                           |
| Name             | String | 변경된 토픽 이름                          |
| Introduction     | String | 변경된 토픽 소개                          |
| Notification     | String | 변경된 토픽 알림                          |
| FaceUrl          | String | 변경된 토픽 프로필 사진 URL               |

### 응답 예시

App 백엔드는 토픽 프로필 변경 정보를 기록하고 콜백 응답 패킷을 보냅니다.

```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0  // 응답 결과 무시
}
```

### 응답 필드

| 객체         | 유형    | 필수 | 설명                                                         |
| ------------ | ------- | ---- | ------------------------------------------------------------ |
| ActionStatus | String  | 필수 | 결과를 요청합니다. OK: 성공 표시, FAIL: 실패 표시.           |
| ErrorCode    | Integer | 필수 | 에러 코드, 값 0은 응답 결과를 무시하도록 허용함을 나타냅니다 |
| ErrorInfo    | String  | 필수 | 에러 메시지                                                  |

## 참고

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API: [Modifying Topic Profile](https://intl.cloud.tencent.com/document/product/1047/49468)
