## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(ModifyLoadBalancers)는 조정 그룹 로드밸런서 수정에 사용됩니다.

* 본 API는 조정 그룹에 새로운 로드밸런서 구성을 지정하는 데 사용됩니다. 이전의 구성에 관계없이 API 매개변수에 따라 새로운 로드밸런서로 구성하는 방식을 취합니다 
* 조정 그룹의 로드밸런서를 모두 지우려면 본 API를 호출 시 조정 그룹 ID만 지정하고 구체적인 로드밸런서는 지정하지 않습니다.
* 본 API는 조정 그룹의 로드밸런서를 즉시 수정하고 하나의 조정 활동을 생성하며 기존 인스턴스의 로드밸런서를 비동기식으로 수정합니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예 | String | 공통 매개변수, 본 API 값: ModifyLoadBalancers |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| AutoScalingGroupId | 예 | String | 조정 그룹 ID |
| LoadBalancerIds.N | 아니요 | Array of String | 기존 로드밸런서 ID 리스트, 현재 길이 상한은 1, LoadBalancerIds와 ForwardLoadBalancers 2가지는 한 번에 1개만 지정 가능 |
| ForwardLoadBalancers.N | 아니요 | Array of [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer) | 응용형 로드밸런서 리스트, 현재 길이 상한은 1, LoadBalancerIds와 ForwardLoadBalancers 2가지는 한 번에 1개만 지정 가능 |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| ActivityId | String | 조정 활동 ID|
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 조정 그룹의 로드밸런서를 기존의 로드밸런서 lb-crhgatrf로 수정

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&LoadBalancerIds.0=lb-crhgatrf
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ActivityId": "asa-67izy66g",
        "RequestId": "bd3c91e8-3051-4c02-ac58-54d47b9c9d63"
    }
}
```

### 예제 2 조정 그룹의 로드밸런서를 응용형 로드밸런서 lb-23aejgcv로 수정하고 수신기는 lbl-ncw704sn입니다.

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
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
        "ActivityId": "asa-9asddelc",
        "RequestId": "8d78668d-61eb-456d-855b-f34f91371089"
    }
}
```

### 예제 3 조정 그룹의 로드밸런서 지우기

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=ModifyLoadBalancers
&AutoScalingGroupId=asg-12wjuh0s
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "ActivityId": "asa-rp63a5q8",
        "RequestId": "7de5a82f-b781-4302-b723-e7a879c20767"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyLoadBalancers)

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
| InvalidParameterValue.ForwardLb | 하나의 응용형 로드밸런서를 잘못 지정했습니다. |
| InvalidParameterValue.LbProjectInconsistent | 로드밸런서 항목이 일치하지 않습니다. |
| InvalidParameterValue.LbVpcInconsistent | 로드밸런서와 조정 그룹의 VPC가 일치하지 않습니다. |
| ResourceNotFound.AutoScalingGroupIdNotFound | 조정 그룹이 존재하지 않습니다. |
| ResourceNotFound.LoadBalancerNotFound | 지정한 로드밸런서를 찾지 못했습니다. |
| ResourceUnavailable.AutoScalingGroupInActivity | 조정 그룹이 활동 중입니다. |

