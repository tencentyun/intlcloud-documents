## 올바른 반환 결과

CVM의 인스턴스 상태 리스트 조회(DescribeInstancesStatus) API 2017-03-12 버전이 예로 사용되며, 호출이 성공하면 가능한 반환은 다음과 같습니다.

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response 및 그 내부의 RequestId는 고정 필드이며 API가 처리되는 한 요청의 성공 여부에 상관없이 반드시 반환됩니다.
* RequestId는 API 요청을 식별하는 데 사용되는 유일한 표시이며, API에 이상이 생긴 경우 당사에 문의하고 문제 해결을 위해 ID를 제공하십시오.
* 고정 필드를 제외하고 나머지는 모두 특정 API에 의해 정의된 필드입니다. 서로 다른 API가 반환하는 필드는 API 문서 내의 정의를 참조하십시오. 이 예에서 TotalCount 및 InstanceStatusSet은 모두 DescribeInstancesStatus API 정의 필드이고, 요청을 호출한 사용자가 아직 CVM 인스턴스가 없으므로, TotalCount는 이 상황에서 반환 값이 0이며, InstanceStatusSet 리스트는 비어있습니다.

## 잘못된 반환 결과

호출이 실패하면, 그 반환값의 예는 다음과 같습니다.

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Error가 표시되면 해당 요청 호출이 실패했음을 나타냅니다. Error 필드는 내부의 Code 및 Message 필드와 함께 호출 실패 시 반드시 반환되어야 합니다.
* Code는 특정 오류의 오류 코드를 나타내며, 요청에 오류가 발생하면 먼저 해당 오류 코드에 따라 공통 오류 코드 및 현재 API에 대응하는 오류 코드 리스트에서 해당하는 원인과 해결 방안을 찾을 수 있습니다.
* Message는 이 오류가 발생한 구체적인 원인을 표시하며, 비즈니스가 발전하거나 환경이 최적화됨에 따라 이 텍스트는 자주 변경 또는 업데이트될 수 있으므로, 사용자는 이 반환값에 의존해서는 안 됩니다.
* RequestId는 API 요청을 식별하는 데 사용되는 유일한 표시이며, API에 이상이 생긴 경우 당사에 문의하고 문제 해결을 위해 ID를 제공하십시오.


## 공통 오류 코드


반환 결과 중에 Error 필드가 있으면 API 호출이 실패했음을 의미합니다. Error 중의 Code 필드는 오류 코드를 나타내며 모든 서비스에 나타날 수 있는 오류 코드는 공통 오류 코드입니다. 다음 리스트에 공통 오류 코드가 나와 있습니다.


| 오류 코드 | 오류 설명 |
|----------|----------|
| AuthFailure.InvalidSecretId | 잘못된 키(Cloud API 키 유형이 아님). |
| AuthFailure.MFAFailure | MFA 오류. |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않음 |
| AuthFailure.SignatureExpire | 서명 만료됨. |
| AuthFailure.SignatureFailure | 서명 오류. |
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
| UnauthorizedOperation | 권한이 없는 작업. |
| UnknownParameter | 알 수 없는 매개변수 오류. |
| UnsupportedOperation | 지원되지 않는 조작. |
| UnsupportedProtocol | http(s) 요청 프로토콜 오류, GET 및 POST 요청만 지원. |
| UnsupportedRegion | API는 전달 지역을 지원하지 않음. |

