
## 기능 설명

반환 결과에 Error 필드가 존재하는 경우 API 포트 호출에 실패한 것입니다. 예:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Error 중의 Code는 오류 코드를 나타내며 Message는 해당 오류의 세부적인 정보를 나타냅니다.

## 오류 코드 리스트

### 공통 오류 코드

| 오류 코드 | 설명 |
|--------|------|
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님). |
| AuthFailure.MFAFailure | MFA 오류. |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않습니다. 콘솔에서 키가 삭제되었거나 사용이 금지되었는지 확인하십시오. 상태가 정상이라면 키를 제대로 입력하였는지 확인하십시오. 키의 앞뒤에 빈칸이 있으면 안됩니다.|
| AuthFailure.SignatureExpire | 서명 유효기간이 만료되었습니다. Timestamp와 서버의 시간 차이는 5분을 초과해서는 안됩니다. 현지 시간이 표준 시간과 동기화되었는지 확인하십시오.|
| AuthFailure.SignatureFailure | 서명 오류. 서명 컴퓨팅 오류, 호출 방식 중 API 인증 문서를 참조하여 서명 컴퓨팅 과정을 확인하십시오.|
| AuthFailure.TokenFailure | token 오류. |
| AuthFailure.UnauthorizedOperation | CAM 권한이 없는 요청. |
| DryRunOperation | DryRun 작업. 요청이 성공하겠지만 여분의 DryRun 매개변수를 전달했음을 의미합니다. |
| FailedOperation | 작업 실패. |
| InternalError | 내부 오류. |
| InvalidAction | API가 존재하지 않음. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameterValue | 매개변수 값 오류. |
| LimitExceeded | 할당량 제한 초과. |
| MissingParameter | 매개변수 결여. |
| NoSuchVersion | API 버전이 존재하지 않음. |
| RequestLimitExceeded | 요청 횟수가 빈도 제한 초과. |
| ResourceInUse | 리소스 사용 중임. |
| ResourceInsufficient | 리소스 부족. |
| ResourceNotFound | 리소스 존재하지 않음. |
| ResourceUnavailable | 리소스 사용 불가. |
| UnauthorizedOperation | 권한이 없는 작업. |
| UnknownParameter | 알 수 없는 매개변수 오류. |
| UnsupportedOperation | 지원되지 않는 작업. |
| UnsupportedProtocol | http(s) 요청 프로토콜 오류, GET와 POST 요청만 지원. |
| UnsupportedRegion | API에 전달한 지역을 지원하지 않음. |

### 비즈니스 오류 코드

| 오류 코드 | 설명 |
|:-------|:-----|
| InternalError.AsyncRequestError | 비동기 태스크 조회 오류. |
| InvalidParameter | 매개변수 오류 |

