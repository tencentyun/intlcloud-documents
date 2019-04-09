
## 기능 설명

반환 결과 중에 Error 필드가 존재하면, API 호출이 실패했음을 의미합니다. 예:

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

Error 중의 Code는 오류 코드를 의미하며, Message는 해당 오류의 구체적인 정보를 의미합니다.

## 오류 코드 리스트

### 공통 오류 코드

| 오류 코드 | 설명 |
|--------|------|
| AuthFailure.InvalidSecretId | 잘못된 키(Cloud API 키 유형이 아님). |
| AuthFailure.MFAFailure | MFA 오류. |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않습니다. 콘솔에서 키가 이미 삭제되었거나 비활성화되었는지 확인하십시오. 상태가 정상이면 키가 올바르게 입력되었는지 확인하고, 앞뒤에 공백이 없도록 주의하십시오.|
| AuthFailure.SignatureExpire | 서명이 만료되었습니다. Timestamp 및 서버 시간의 차이는 5분을 초과해서는 안 됩니다. 현지 시간이 표준 시간과 동기화되어 있는지 확인하십시오.|
| AuthFailure.SignatureFailure | 서명 오류. 서명 컴퓨팅 오류이므로 호출 방식 중의 API 인증 문서를 참조하여 서명 컴퓨팅 프로세스를 확인하십시오.|
| AuthFailure.TokenFailure | token 오류. |
| AuthFailure.UnauthorizedOperation | CAM 권한이 없는 요청. |
| DryRunOperation | DryRun 조작, 요청이 성공하지만, 여분의 DryRun 매개변수가 전송되었음을 나타냅니다. |
| FailedOperation | 조작 실패. |
| InternalError | 내부 오류. |
| InvalidAction | API가 존재하지 않음. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameterValue | 매개변수 값 오류. |
| LimitExceeded | 할당량 한도 초과. |
| MissingParameter | 매개변수 누락 오류. |
| NoSuchVersion | API 버전이 존재하지 않음. |
| RequestLimitExceeded | 요청의 횟수가 빈도 제한 초과. |
| ResourceInUse | 리소스 사용 중. |
| ResourceInsufficient | 리소스 부족. |
| ResourceNotFound | 리소스 존재하지 않음. |
| ResourceUnavailable | 리소스 사용 불가. |
| UnauthorizedOperation | 권한 부여하지 않은 조작. |
| UnknownParameter | 알 수 없는 매개변수 오류. |
| UnsupportedOperation | 지원되지 않는 조작. |
| UnsupportedProtocol | http(s) 요청 프로토콜 오류, GET 및 POST 요청만 지원. |
| UnsupportedRegion | API는 전달 지역을 지원하지 않음. |

### 비즈니스 오류 코드

| 오류 코드 | 설명 |
|:-------|:-----|
| 9003 | param error. |
| CdbError | 백 엔드 오류 또는 프로세스 오류. |
| CdbError.BackupError | 백업 오류. |
| CdbError.DatabaseError | 백 엔드 데이터베이스 오류. |
| CdbError.ImportError | 가져오기 태스크 오류. |
| CdbError.TaskError | 백 엔드 태스크 오류. |
| FailedOperation.StatusConflict | 태스크 상태 충돌. |
| InternalError.CdbCgwError | 시스템 내부 오류. |
| InternalError.CosError | 파일 정보 획득 실패. |
| InternalError.DatabaseAccessError | 데이터베이스 내부 오류. |
| InternalError.DesError | 시스템 내부 오류. |
| InternalError.DfwError | 보안 그룹 조작 오류. |
| InternalError.ResourceNotMatch | 리소스 불일치. |
| InternalError.ResourceNotUnique | 리소스가 고유하지 않음. |
| InternalError.TaskFrameError | 비동기화 태스크 오류. |
| InternalError.TradeError | 거래 시스템 오류. |
| InternalError.VpcError | VPC 또는 서브넷 오류. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameter.InstanceNameNotFound | 해당 인스턴스를 찾을 수 없습니다. |
| InvalidParameter.InstanceNotFound | 인스턴스가 존재하지 않음. |
| InvalidParameter.InvalidAsyncRequestId | 비동기화 태스크가 존재하지 않습니다. |
| InvalidParameter.InvalidName | 잘못된 이름. |
| InvalidParameter.ResourceExists | 리소스가 이미 존재합니다. |
| InvalidParameter.ResourceNotFound | 관련 리소스를 찾을 수 없습니다. |
| OperationDenied | 작업이 허용되지 않음. |
| OperationDenied.ActionNotSupport | 지원되지 않는 조작. |
| OperationDenied.WrongPassword | 비밀번호 오류 또는 인증을 통과하지 못했습니다. |
| OperationDenied.WrongStatus | 백 엔드 태스크 상태 오류. |
| UnauthorizedOperation.NotEnoughPrivileges | 인증 실패, 충분한 권한이 없습니다. |

