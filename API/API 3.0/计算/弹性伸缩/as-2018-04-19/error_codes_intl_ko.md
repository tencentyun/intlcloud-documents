
## 기능 설명

반환된 결과에 Error 필드가 존재하는 경우, API 호출 실패를 나타냅니다. 예:

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

Error 필드의 Code는 오류 코드를 나타내고 Message는 해당 오류의 구체적인 정보를 표시합니다.

## 오류 코드 리스트

### 공통 오류 코드

| 오류 코드 | 설명 |
|--------|------|
| AuthFailure.InvalidSecretId | 잘못된 키(클라우드 API 키 유형이 아님). |
| AuthFailure.MFAFailure | MFA 오류. |
| AuthFailure.SecretIdNotFound | 키가 존재하지 않습니다. 콘솔에서 키가 이미 삭제되었거나 사용이 금지되었는지 확인하십시오. 이상이 없으면 키를 정확하게 입력했는지 확인하십시오. 앞뒤 빈칸이 없어야 합니다. |
| AuthFailure.SignatureExpire | 서명이 만료되었습니다. Timestamp와 서버 시간 차이는 5분을 초과할 수 없습니다. 현지 시간이 표준 시간과 동기화되었는지 확인하십시오. |
| AuthFailure.SignatureFailure | 서명 오류. 서명 컴퓨팅 오류, 호출 방식의 API 인증 문서를 참조하여 서명 컴퓨팅 과정을 확인하십시오. |
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

### 비즈니스 오류 코드

| 오류 코드 | 설명 |
|:-------|:-----|
| AccountQualificationRestrictions | 해당 요청 계정은 자격 심사를 통과하지 못했습니다. |
| CallCvmError | CVM API 호출 실패. |
| InternalError | 내부 오류 |
| InvalidFilter | 잘못된 필터. |
| InvalidImageId.NotFound | 해당 이미지를 찾지 못했습니다. |
| InvalidLaunchConfiguration | 잘못된 시동 구성. |
| InvalidLaunchConfiguration.NameDuplicate | 시동 구성 이름 중복. |
| InvalidLaunchConfigurationId | 잘못된 시동 구성 ID. |
| InvalidLaunchConfigurationId.InUse | 사용 중인 시동 구성. |
| InvalidLaunchConfigurationId.NotFound | 해당 시동 구성을 찾지 못했습니다. |
| InvalidParameter.Conflict | 매개변수 충돌. 지정한 여러 매개변수가 충돌해 동시에 존재할 수 없습니다. |
| InvalidParameter.InScenario | 특정 시나리오에서의 잘못된 매개변수. |
| InvalidParameter.MustOneParameter | 매개변수 결함. 두 개의 매개변수 중 반드시 하나를 지정해야 합니다. |
| InvalidParameterConflict | 지정한 두 개의 매개변수가 충돌해 동시에 존재할 수 없습니다. |
| InvalidParameterValue.CronExpressionIllegal | 시간 제한 태스크에 지정된 Cron 식이 잘못되었습니다. |
| InvalidParameterValue.CvmConfigurationError | CVM 매개변수 검사에 이상이 생겼습니다. |
| InvalidParameterValue.CvmError | CVM 매개변수 검사에 이상이 생겼습니다. |
| InvalidParameterValue.EndTimeBeforeStartTime | 시간 제한 태스크의 설정한 종료 시간이 시작 시간 이전입니다. |
| InvalidParameterValue.Filter | 잘못된 필터입니다. |
| InvalidParameterValue.ForwardLb | 하나의 응용형 로드밸런서를 잘못 지정했습니다. |
| InvalidParameterValue.GroupNameDuplicate | 조정 그룹 이름 중복. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | 시간 제한 태스크 이름에 잘못된 문자부호가 포함되어 있습니다. |
| InvalidParameterValue.LaunchConfigurationNotFound | 지정한 시동 구성을 찾지 못했습니다. |
| InvalidParameterValue.LbProjectInconsistent | 로드밸런서 항목이 일치하지 않습니다. |
| InvalidParameterValue.LbVpcInconsistent | 로드밸런서와 조정 그룹의 VPC가 일치하지 않습니다. |
| InvalidParameterValue.LimitExceeded | 값이 제한을 초과했습니다. |
| InvalidParameterValue.OnlyVpc | 계정은 VPC 네트워크만 지원합니다. |
| InvalidParameterValue.Range | 값이 지정한 범위를 초과했습니다. |
| InvalidParameterValue.ScheduledActionNameDuplicate | 시간 제한 태스크 이름이 중복됩니다. |
| InvalidParameterValue.Size | 조정 그룹 최대 수량, 최소 수량, 에상 인스턴스 수의 값이 잘못되었습니다. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | 시간 제한 태스크의 설정한 시작 시간이 현재 시간 이전입니다. |
| InvalidParameterValue.SubnetIds | 서브넷 정보가 잘못되었습니다. |
| InvalidParameterValue.TimeFormat | 시간 형식 오류. |
| InvalidParameterValue.TooLong | 값이 너무 많습니다. |
| InvalidPermission | 계정이 해당 작업을 지원하지 않습니다. |
| LaunchConfigurationQuotaLimitExceeded | 시동 구성 할당량이 한도를 초과했습니다. |
| LimitExceeded | 할당량 한도를 초과했습니다. |
| LimitExceeded.AutoScalingGroupLimitExceeded | 조정 그룹 수량이 한도를 초과했습니다. |
| LimitExceeded.DesiredCapacityLimitExceeded | 에상 인스턴스 수가 한도를 초과했습니다. |
| LimitExceeded.MaxSizeLimitExceeded | 최대 인스턴스 수가 한도보다 큽니다. |
| LimitExceeded.MinSizeLimitExceeded | 최소 인스턴스 수가 한도보다 작습니다. |
| LimitExceeded.ScheduledActionLimitExceeded | 시간 제한 태스크 수량이 한도를 초과했습니다. |
| MissingParameter | 매개변수 결함 오류. |
| MissingParameter.InScenario | 특정 시나리오에서의 매개변수 결함. |
| ResourceInUse.ActivityInProgress | 조정 그룹이 조정 활동 실행 중입니다. |
| ResourceInUse.InstanceInGroup | 조정 그룹 내 아직 정상 인스턴스가 있습니다. |
| ResourceInsufficient.AutoScalingGroupAboveMaxSize | 조정 그룹 최대 인스턴스 수를 초과했습니다. |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | 조정 그룹 최소 인스턴스 수보다 적습니다. |
| ResourceNotFound.AutoScalingGroupIdNotFound | 조정 그룹이 존재하지 않습니다. |
| ResourceNotFound.InstancesNotFound | 지정한 인스턴스가 존재하지 않습니다. |
| ResourceNotFound.InstancesNotInAutoScalingGroup | 목표 인스턴스가 조정 그룹 내에 존재하지 않습니다. |
| ResourceNotFound.LoadBalancerNotFound | 지정한 로드밸런서를 찾지 못했습니다. |
| ResourceNotFound.ScheduledActionNotFound | 지정한 시간 제한 태스크가 존재하지 않습니다. |
| ResourceUnavailable.AutoScalingGroupAbnormalStatus | 조정 그룹 상태 이상. |
| ResourceUnavailable.AutoScalingGroupDisabled | 조정 그룹이 사용 중지되었습니다. |
| ResourceUnavailable.AutoScalingGroupInActivity | 조정 그룹이 활동 중입니다. |
| ResourceUnavailable.CvmVpcInconsistent | 인스턴스와 조정 그룹 VPC가 일치하지 않습니다. |
| ResourceUnavailable.InstancesAlreadyInAutoScalingGroup | 인스턴스가 이미 조정 그룹 내 존재합니다. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | 시동 구성 상태 이상. |
| ResourceUnavailable.ProjectInconsistent | 프로젝트가 일치하지 않습니다. |

