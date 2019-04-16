## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(CreateAutoScalingGroup)는 조정 그룹 생성에 사용됩니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 본 API 값: CreateAutoScalingGroup |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| AutoScalingGroupName | 예 | String | 조정 그룹 이름, 사용자 계정에 유일해야 합니다. 이름은 중문, 영문, 숫자, 밑줄, 구분 기호 "-", 소수점만 지원하고 길이는 55바이트를 초과할 수 없습니다. |
| LaunchConfigurationId | 예 | String | 시동 구성 ID |
| MaxSize | 예 | Integer | 최대 인스턴스 수, 값 범위는 0-2000입니다. |
| MinSize | 예 | Integer | 최소 인스턴스 수, 값 범위는 0-2000입니다. |
| VpcId | 예 | String | VPC ID, 기본 네트워크는 빈 문자열을 입력합니다. |
| DefaultCooldown | 아니요 | Integer | 기본 쿨타임, 단위는 초, 기본값은 300입니다. |
| DesiredCapacity | 아니요 | Integer | 에상 인스턴스 수, 크기는 최소 에상 인스턴스 수와 최대 에상 인스턴스 수 사이입니다. |
| LoadBalancerIds.N | 아니요 | Array of String | 기존 로드밸런서 ID 리스트, 현재 길이 상한은 1, LoadBalancerIds와 ForwardLoadBalancers 2가지는 한 번에 1개만 지정 가능 |
| ProjectId | 아니요 | Integer | 프로젝트 ID |
| ForwardLoadBalancers.N | 아니요 | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | 응용형 로드밸런서 리스트, 현재 길이 상한은 1, LoadBalancerIds와 ForwardLoadBalancers 2가지는 한 번에 1개만 지정 가능 |
| SubnetIds.N | 아니요 | Array of String | 서브넷 ID 리스트, VPC 시나리오에서 서브넷을 반드시 지정해야 합니다. |
| TerminationPolicies.N | 아니요 | Array of String | 폐기 전략, 현재 길이 상한은 1입니다. 가능한 값은 OLDEST_INSTANCE와 NEWEST_INSTANCE를 포함하고 기본 값은 OLDEST_INSTANCE입니다.<br/><br><li> OLDEST_INSTANCE, 조정 그룹 중 가장 오래된 인스턴스를 우선 폐기합니다.<br/><br><li> NEWEST_INSTANCE, 조정 그룹 중 최신 인스턴스를 우선 폐기합니다. |
| Zones.N | 아니요 | Array of String | 가용 영역 리스트, 기본 네트워크 시나리오에서 가용 영역을 반드시 지정해야 합니다. |
| RetryPolicy | 아니요 | String | 다시 시도 전략, 가능한 값은 IMMEDIATE_RETRY와 INCREMENTAL_INTERVALS를 포함하고 기본값은 IMMEDIATE_RETRY입니다.<br/><br><li> IMMEDIATE_RETRY는 즉시 다시 시도, 비교적 짧은 시간 내 빠르게 다시 시도하고 연속 실패가 일정 횟수(5회)를 초과한 후 다시 시도하지 않습니다.<br/><br><li> INCREMENTAL_INTERVALS는 간격이 증가하면서 다시 시도, 연속 실패 횟수가 증가할수록 다시 시도 간격도 점차 커지고 다시 시도 간격은 초 단위에서 1일까지 다양합니다. |
| ZonesCheckPolicy | 아니요 | String | 가용 영역 검사 전략, 가능한 값은 ALL과 ANY를 포함하고 기본값은 ANY입니다. <br/><br><li> ALL, 모든 가용 영역(Zone) 또는 서브넷(SubnetId)이 사용 가능하면 검사를 통과할 수 있고 그렇지 않은 경우 검사 오류를 보고합니다. <br/><br><li> ANY, 하나의 사용 가능한 가용 영역(Zone) 또는 서브넷(SubnetId)이 존재하면 검사를 통과하고 그렇지 않은 경우 검사 오류를 보고합니다. <br/><br/>가용 영역 또는 서브넷을 사용할 수 없는 일반적인 원인은 해당 가용 영역 CVM 인스턴스 유형 매진, 해당 가용 영역 CBS 클라우드 디스크 매진, 해당 가용 영역 할당량 부족, 해당 서브넷 IP 부족 등을 포함합니다. <br/>Zones/SubnetIds 중 가용 영역 또는 서브넷이 존재하지 않으면 ZonesCheckPolicy는 어떤 값을 취해도 검사 오류를 보고합니다. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| AutoScalingGroupId | String | 조정 그룹 ID |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 조정 그룹 생성

조정 그룹 생성, VPC 네트워크, 7계층 로드밸런서 구성

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=CreateAutoScalingGroup
&AutoScalingGroupName=asg-vpc-7layer-lb
&DefaultCooldown=300
&DesiredCapacity=0
&LaunchConfigurationId=asc-7vucy6ae
&MaxSize=10
&MinSize=0
&ProjectId=0
&VpcId=vpc-hy436tmc
&SubnetIds.0=subnet-3tmerl37
&SubnetIds.1=subnet-b0vxjhot
&TerminationPolicies.0=OLDEST_INSTANCE
&ForwardLoadBalancers.0.LoadBalancerId=lb-23aejgcv
&ForwardLoadBalancers.0.ListenerId=lbl-ncw704sn
&ForwardLoadBalancers.0.LocationId=loc-l3hmaev9
&ForwardLoadBalancers.0.TargetAttributes.0.Port=8080
&ForwardLoadBalancers.0.TargetAttributes.0.Weight=10
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "AutoScalingGroupId": "asg-nkdwoui0",
        "RequestId": "a5d66fed-85b9-4f43-8243-597337ba896e"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateAutoScalingGroup)

### SDK

클라우드 API 3.0은 일체화된 SDK를 제공하고 여러 종류의 프로그래밍 언어를 지원하여 편리하게 API를 호출할 수 있습니다.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. 오류 코드

다음은 API 비즈니스 로직과 관련된 오류 코드만 나열하며 다른 오류 코드는 [공통 오류 코드](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81)를 참조하십시오.

| 오류 코드 | 설명 |
|---------|---------|
| InternalError | 내부 오류 |
| InvalidParameter.InScenario | 특정 시나리오에서의 잘못된 매개변수. |
| InvalidParameterValue.CvmError | CVM 매개변수 검사에 이상이 생겼습니다. |
| InvalidParameterValue.ForwardLb | 하나의 응용형 로드밸런서를 잘못 지정했습니다. |
| InvalidParameterValue.GroupNameDuplicate | 조정 그룹 이름 중복. |
| InvalidParameterValue.LaunchConfigurationNotFound | 지정한 시동 구성을 찾지 못했습니다. |
| InvalidParameterValue.LbProjectInconsistent | 로드밸런서 항목이 일치하지 않습니다. |
| InvalidParameterValue.LbVpcInconsistent | 로드밸런서와 조정 그룹의 VPC가 일치하지 않습니다. |
| InvalidParameterValue.LimitExceeded | 값이 제한을 초과했습니다. |
| InvalidParameterValue.OnlyVpc | 계정은 VPC 네트워크만 지원합니다. |
| InvalidParameterValue.Range | 값이 지정한 범위를 초과했습니다. |
| InvalidParameterValue.Size | 조정 그룹 최대 수량, 최소 수량, 에상 인스턴스 수의 값이 잘못되었습니다. |
| InvalidParameterValue.SubnetIds | 서브넷 정보가 잘못되었습니다. |
| InvalidParameterValue.TooLong | 값이 너무 많습니다. |
| LimitExceeded | 할당량 한도를 초과했습니다. |
| LimitExceeded.AutoScalingGroupLimitExceeded | 조정 그룹 수량이 한도를 초과했습니다. |
| LimitExceeded.MaxSizeLimitExceeded | 최대 인스턴스 수가 한도보다 큽니다. |
| LimitExceeded.MinSizeLimitExceeded | 최소 인스턴스 수가 한도보다 작습니다. |
| MissingParameter.InScenario | 특정 시나리오에서의 매개변수 결함. |
| ResourceNotFound.LoadBalancerNotFound | 지정한 로드밸런서를 찾지 못했습니다. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | 시동 구성 상태 이상. |
| ResourceUnavailable.ProjectInconsistent | 프로젝트가 일치하지 않습니다. |

