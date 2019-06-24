
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
| RequestLimitExceeded | 요청 횟수가 빈도 한도 초과. |
| ResourceInUse | 리소스 사용 중. |
| ResourceInsufficient | 리소스 부족. |
| ResourceNotFound | 리소스 존재하지 않음. |
| ResourceUnavailable | 리소스 사용 불가. |
| UnauthorizedOperation | 권한이 없는 작업. |
| UnknownParameter | 알 수 없는 매개변수 오류. |
| UnsupportedOperation | 지원하지 않는 작업 |
| UnsupportedProtocol | http(s) 요청 프로토콜 오류, GET 및 POST 요청만 지원. |
| UnsupportedRegion | API는 전달 지역을 지원하지 않음. |

### 비즈니스 오류 코드



| 오류 코드 | 설명 |
|:-------|:-----|
| FailedOperation.SystemError | 내부 시스템 오류, 비즈니스와 관련이 없습니다. |
| FailedOperation.Unknown | weekday에 잘못된 데이터를 입력했습니다. |
| InternalError.DbOperationFailed | 시스템 DB 작업 오류, 가능한 값: update insert select.. |
| InvalidParameter | 매개변수 오류 |
| InvalidParameter.EmptyParam | 매개변수가 비어 있습니다. |
| InvalidParameter.InvalidParameter | 비즈니스 매개변수가 잘못되었습니다. |
| InvalidParameter.OnlyVPCOnSpecZoneId | 상하이 금융은 VPC만 제공합니다. |
| InvalidParameterValue.InvalidInstanceTypeId | 구매한 인스턴스 유형 오류(TypeId 1: 클러스터 버전, 2: 마스터/슬레이브 버전, 즉, 기존 마스터/슬레이브 버전). |
| InvalidParameterValue.InvalidSubnetId | VPC에서 서브넷 ID가 잘못되었습니다. |
| InvalidParameterValue.MemSizeNotInRange | 요청 요량은 판매 범위 내에 있지 않습니다. |
| InvalidParameterValue.PasswordEmpty | 비밀번호가 비어 있습니다. |
| InvalidParameterValue.PasswordError | 비밀번호 검증 오류, 비밀번호가 잘못되었습니다. |
| InvalidParameterValue.PasswordRuleError | 비밀번호 리셋 시, MC가 가져온 old password와 이전에 설정한 암호과 같지 않습니다. |
| InvalidParameterValue.ReduceCapacityNotAllowed | 요청 용량이 작아서 용량 줄임을 지원하지 않습니다. |
| InvalidParameterValue.WeekDaysIsInvalid | weekday에 잘못된 데이터를 입력했습니다. |
| LimitExceeded.InvalidMemSize | 요청 용량이 판매 사양에 있지 않습니다(memSize는 1024의 정수 배수여야 하며, 단위는 MB입니다). |
| LimitExceeded.InvalidParameterGoodsNumNotInRange | 한 번 구매한 인스턴스 수는 판매 수량 한도 범위 내에 있지 않습니다. |
| LimitExceeded.PeriodExceedMaxLimit | 구매 시간이 3년을 초과하고, 요청 시간이 최대 시간을 초과합니다. |
| LimitExceeded.PeriodLessThanMinLimit | 구매 시간이 잘못되었으며, 시간은 최소 1개월입니다. |
| ResourceInUse.InstanceBeenLocked | 인스턴스가 기타 프로세스에 잠겼습니다. |
| ResourceNotFound.AccountDoesNotExists | uin 값이 비어 있습니다. |
| ResourceNotFound.InstanceNotExists | serialId에 따라 해당 Redis를 찾지 못했습니다. |
| ResourceUnavailable.AccountBalanceNotEnough | 요청 주문 번호가 존재하지 않습니다. |
| ResourceUnavailable.InstanceDeleted | 인스턴스가 회수되었습니다. |
| ResourceUnavailable.InstanceLockedError | Redis는 이미 기타 프로세스에 잠겼습니다. |
| ResourceUnavailable.InstanceStatusAbnormal | Redis 상태 이상으로 해당 프로세스를 실행할 수 없습니다. |
| ResourceUnavailable.NoRedisService | 요청한 지역은 현재 요청 유형의 Redis 서비스를 제공하지 않습니다. |
| ResourceUnavailable.NoTypeIdRedisService | 요청한 지역은 현재 요청 유형의 Redis 서비스를 제공하지 않습니다. |
| UnauthorizedOperation | 권한이 없는 작업. |
| UnauthorizedOperation.NoCAMAuthed | cam 권한이 없습니다. |
| UnauthorizedOperation.UserNotInWhiteList | 사용자가 화이트리스트에 없습니다. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | Redis 클러스터 버전은 보안 그룹 액세스를 허용하지 않습니다. |
| UnsupportedOperation.IsAutoRenewError | 자동 갱신 식별 오류. |
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | 클러스터 버전 인스턴스만 백업 내보내기 지원합니다. |
