## 올바른 반환 결과

CVM API인 인스턴스 상태 리스트 보기(DescribeInstancesStatus) 2017-03-12 버전을 예로, 호출이 성공하면 가능한 반환값은 다음과 같습니다.

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response 및 해당 내부의 RequestId는 고정 필드로 요청 성공 여부에 관계없이 API에서 처리하는 한 반드시 반환됩니다.
* RequestId는 하나의 API 요청의 유일한 식별자입니다. API 에 이상이 발생하면 당사에게 연락하고 해당 ID를 제공하십시오
* 고정 필드 이외에 나머지는 모두 구체적인 API로 정의된 필드입니다. 서로 다른 API에서 반환하는 필드는 API 문서 중의 정의를 참고하십시오. 본 예시 중 TotalCount와 InstanceStatusSet은 모두 DescribeInstancesStatus API로 정의된 필드입니다. 요청을 보낸 사용자는 아직 CVM 인스턴스가 없기 때문에 여기 TotalCount의 반환값이 0이고 InstanceStatusSet 리스트는 비어있습니다.

## 반환 결과 오류

호출이 실패하면 해당 반환값 예시는 다음과 같습니다.

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Error는 해당 요청 호출 실패를 의미합니다. Error 필드는 내부의 Code와 Message 필드와 함께 호출 실패 시 반드시 반환됩니다.
* Code는 구체적인 오류 코드를 나타냅니다. 요청에 오류가 발생하면 오류 코드에 따라 공통 오류 코드와 현재 API에 대응하는 오류 코드 리스트에서 해당하는 원인과 해결 방법을 찾을 수 있습니다.
* Message는 해당 오류의 구체적인 발생 원인을 나타냅니다. 비즈니스 확장 또는 체험 최적화에 따라 해당 텍스트는 자주 변경 또는 업데이트하여 사용자는 해당 반환값에 의존해서는 안 됩니다.
* RequestId는 하나의 API 요청의 유일한 식별자입니다. API 에 이상이 발생하면 당사에게 연락하고 해당 ID를 제공하십시오


## 공통 오류 코드


반환 결과 중 Error 필드가 존재하면 API 호출 실패를 표시합니다. Error의 Code 필드는 오류 코드를 표시하고 모든 비즈니스에서 발생 가능한 오류 코드가 공통 오류 코드입니다. 다음 표에 공통 오류 코드가 나열됩니다.


| 오류 코드 | 오류 설명 |
|----------|----------|
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님). |
| AuthFailure.MFAFailure | MFA 오류. |
| AuthFailure.SecretIdNotFound | 키 존재하지 않음. |
| AuthFailure.SignatureExpire | 서명 만료됨. |
| AuthFailure.SignatureFailure | 서명 오류. |
| AuthFailure.TokenFailure | token 오류. |
| AuthFailure.UnauthorizedOperation | CAM 권한이 없는 요청. |
| DryRunOperation | DryRun 작업. 요청이 성공하겠지만 여분의 DryRun 매개변수를 전달했음을 나타냅니다. |
| FailedOperation | 조작 실패. |
| InternalError | 내부 오류. |
| InvalidAction | API가 존재하지 않음. |
| InvalidParameter | 매개변수 오류. |
| InvalidParameterValue | 매개변수 값 오류. |
| LimitExceeded | 할당량 한도 초과. |
| MissingParameter | 매개변수 누락됨. |
| NoSuchVersion | API 버전이 존재하지 않음. |
| RequestLimitExceeded | 요청의 횟수가 빈도 제한을 초과했습니다. |
| ResourceInUse | 리소스가 이미 사용 중입니다. |
| ResourceInsufficient | 리소스가 부족합니다. |
| ResourceNotFound | 리소스가 존재하지 않습니다. |
| ResourceUnavailable | 리소스를 사용할 수 없습니다. |
| UnauthorizedOperation | 권한이 없는 조작입니다. |
| UnknownParameter | 알 수 없는 매개변수 오류. |
| UnsupportedOperation | 지원되지 않는 조작입니다. |
| UnsupportedProtocol | http(s) 요청 프로토콜 오류. GET과 POST 요청만 지원합니다. |
| UnsupportedRegion | API에 지원되지 않는 전달 지역. |

