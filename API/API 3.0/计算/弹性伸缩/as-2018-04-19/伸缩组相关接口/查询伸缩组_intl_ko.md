## 1. API 설명

API 요청 도메인 이름: as.tencentcloudapi.com.

본 API(DescribeAutoScalingGroups)는 조정 그룹 정보 조회에 사용됩니다.

* 조정 그룹 ID, 조정 그룹 이름 또는 시동 구성 ID 등 정보에 따라 조정 그룹의 세부 정보를 조회할 수 있습니다. 필터링 세부 정보는 필터 `Filter`를 참조하십시오.
* 매개변수가 비어있으면 현재 사용자에게 일정 수량(`Limit`가 지정한 수량, 기본값은 20)의 조정 그룹을 반환합니다.

기본 API 요청 빈도 제한: 20회/초.

주의: 본 API는 금융 지역을 지원합니다. 금융 지역과 비금융 지역은 격리되어 서로 연결되지 않기 때문에 공통 매개변수 Region이 금융 지역인 경우(예: ap-shanghai-fsi) 금융 지역을 포함한 지역명을 동시에 지정해야 하며 가장 좋은 것은 Region의 지역과 일치하는 것입니다. 예를 들어, as.ap-shanghai-fsi.tencentcloudapi.com입니다.



## 2. 입력 매개변수

다음 요청 매개변수 리스트에는 API 요청 매개변수와 일부 공통 매개변수만 나열합니다. 완전한 공통 매개변수 리스트는 [공통 매개변수](/document/api/377/20426)를 참조하십시오.

| 매개변수 이름 | 필수 여부 | 유형 | 설명 |
|---------|---------|---------|---------|
| Action | 예| String | 공통 매개변수, 본 API 값: DescribeAutoScalingGroups |
| Version | 예 | String | 공통 매개변수, 본 API 값: 2018-04-19 |
| Region | 예 | String | 공통 매개변수, 세부 정보는 제품이 지원하는 [지역 리스트](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8)를 참조하십시오 |
| AutoScalingGroupIds.N | 아니요 | Array of String | 하나 또는 여러 조정 그룹의 ID에 따라 조회합니다. 조정 그룹 ID 형식은 예를 들어 `asg-nkdwoui0`와 같습니다. 매회 요청의 상한은 100입니다. 매개변수는 `AutoScalingGroups`와 `Filters`의 동시 지정을 지원하지 않습니다. |
| Filters.N | 아니요 | Array of [Filter](/document/api/377/20453#Filter) | 필터링 조건입니다. <br/><li> auto-scaling-group-id - String - 필수 입력 여부: 아니요 - (필터링 조건)조정 그룹 ID에 따라 필터링합니다.</li><li> auto-scaling-group-name - String - 필수 입력 조건: 아니요 - (필터링 조건)조정 그룹 이름에 따라 필터링합니다.</li><li> launch-configuration-id - String - 필수 입력 여부: 아니요 - (필터링 조건)시동 구성 ID에 따라 필터링합니다.</li><br/>매회 요청한 `Filters`의 상한은 10이고 `Filter.Values`의 상한은 5입니다. 매개변수는 `AutoScalingGroupIds`와 `Filters`의 동시 지정을 지원하지 않습니다. |
| Limit | 아니요 | Integer | 반환 수량, 기본값은 20, 최대값은 100입니다. `Limit`에 대한 더 상세한 설명은 API [소개](https://cloud.tencent.com/document/api/213/15688) 중 관련 섹션을 참조하십시오. |
| Offset | 아니요 | Integer | 오프셋, 기본값은 0입니다. `Offset`에 대한 더 상세한 설명은 API [소개](https://cloud.tencent.com/document/api/213/15688) 중 관련 섹션을 참조하십시오. |

## 3. 출력 매개변수

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| AutoScalingGroupSet | Array of [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup) | 조정 그룹 세부 정보 리스트 |
| TotalCount | Integer | 조건에 부합하는 조정 그룹 수. |
| RequestId | String | 유일한 요청 ID, 매회 요청 시마다 반환됩니다. 문제를 찾을 경우 해당 요청의 RequestId를 제공해야 합니다. |

## 4. 예시

### 예제 1 조정 그룹 조회

조정 그룹 ID를 지정하여 조정 그룹 조회 

#### 입력 예시

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingGroups
&AutoScalingGroupIds.0=asg-nkdwoui0
&<공통 요청 매개변수>
```

#### 출력 예시

```
{
    "Response": {
        "AutoScalingGroupSet": [
            {
                "LaunchConfigurationId": "asc-7vucy6ae",
                "ForwardLoadBalancerSet": [
                    {
                        "TargetAttributes": [
                            {
                                "Port": 8080,
                                "Weight": 10
                            }
                        ],
                        "LocationId": "loc-l3hmaev9",
                        "ListenerId": "lbl-ncw704sn",
                        "LoadBalancerId": "lb-23aejgcv"
                    }
                ],
                "LoadBalancerIdSet": [],
                "InstanceCount": 1,
                "DesiredCapacity": 1,
                "AutoScalingGroupStatus": "NORMAL",
                "AutoScalingGroupId": "asg-nkdwoui0",
                "ProjectId": 0,
                "TerminationPolicySet": [
                    "OLDEST_INSTANCE"
                ],
                "AutoScalingGroupName": "vpc-7layer-lb",
                "InServiceInstanceCount": 1,
                "DefaultCooldown": 301,
                "MinSize": 0,
                "MaxSize": 10,
                "VpcId": "vpc-hy436tmc",
                "LaunchConfigurationName": "시동 구성 1",
                "CreatedTime": "2018-09-27T02:01:28Z",
                "SubnetIdSet": [
                    "subnet-3tmerl37",
                    "subnet-b0vxjhot"
                ],
                "EnabledStatus": "ENABLED",
                "ZoneSet": []
            }
        ],
        "TotalCount": 1,
        "RequestId": "b8d3660c-bed1-40ad-9e7d-77390c9610be"
    }
}
```


## 5. 개발자 리소스

### API Explorer

**해당 도구는 온라인 호출, 서명 인증, SDK 코드 생성과 빠른 검색 API 등 기능을 제공하고 클라우드 API 사용 난이도를 대폭 낮춰 사용을 추천합니다.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingGroups)

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
| InvalidFilter | 잘못된 필터. |
| InvalidParameterConflict | 지정한 두 개의 매개변수가 충돌해 동시에 존재할 수 없습니다. |
| InvalidParameterValue.Filter | 잘못된 필터입니다. |
| InvalidPermission | 계정이 해당 작업을 지원하지 않습니다. |

