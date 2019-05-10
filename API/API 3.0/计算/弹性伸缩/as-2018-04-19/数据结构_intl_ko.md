## Activity

조건에 부합하는 조정 활동 관련 정보입니다.

API: DescribeAutoScalingActivities에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| AutoScalingGroupId | String | 조정 그룹 ID. |
| ActivityId | String | 조정 활동 ID. |
| ActivityType | String | 조정 활동 유형입니다. 값은 다음과 같습니다. <br><br/><li>SCALE_OUT: 확장 활동<li>SCALE_IN: 축소 활동<li>ATTACH_INSTANCES: 인스턴스 추가 <li>REMOVE_INSTANCES: 인스턴스 폐기 <li>DETACH_INSTANCES: 인스턴스 제거 <li>TERMINATE_INSTANCES_UNEXPECTEDLY: 인스턴스가 CVM 콘솔에서 폐기됨<li>REPLACE_UNHEALTHY_INSTANCE: 비정상 인스턴스 교체 |
| StatusCode | String | 조정 활동 상태입니다. 값은 다음과 같습니다. <br><br/><li>INIT: 초기화 중<br/><li>RUNNING: 실행 중<br/><li>SUCCESSFUL: 활동 성공<br/><li>PARTIALLY_SUCCESSFUL: 활동 일부 성공<br/><li>FAILED: 활동 실패<br/><li>CANCELLED: 활동 취소 |
| StatusMessage | String | 조정 활동 상태 설명. |
| Cause | String | 조정 활동 원인. |
| Description | String | 조정 활동 설명. |
| StartTime | Timestamp | 조정 활동 시작 시간. |
| EndTime | Timestamp | 조정 활동 종료 시간. |
| CreatedTime | Timestamp | 조정 활동 생성 시간. |
| ActivityRelatedInstanceSet | Array of [ActivtyRelatedInstance](#ActivtyRelatedInstance) | 조정 활동 관련 인스턴스 정보 집합. |
| StatusMessageSimplified | String | 조정 활동 상태 개요. |

## ActivtyRelatedInstance

이번 조정 활동과 관련된 인스턴스 정보입니다.

API: DescribeAutoScalingActivities에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 인스턴스 ID |
| InstanceStatus | String | 조정 활동 중 인스턴스 상태. 값은 다음과 같습니다. <br/><li>SUCCESSFUL: 활동 성공<br/><li>FAILED: 활동 실패 |

## AutoScalingGroup

조정 그룹

API: DescribeAutoScalingGroups에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| AutoScalingGroupId | String | 조정 그룹 ID |
| AutoScalingGroupName | String | 조정 그룹 이름 |
| AutoScalingGroupStatus | String | 조정 그룹 상태 |
| CreatedTime | Timestamp | 생성 시간, UTC 기준 |
| DefaultCooldown | Integer | 기본 쿨 타임, 단위는 초 |
| DesiredCapacity | Integer | 에상 인스턴스 수 |
| EnabledStatus | String | 활성화 상태, 값은 `ENABLED`와 `DISABLED` 포함 |
| ForwardLoadBalancerSet | Array of [ForwardLoadBalancer](#ForwardLoadBalancer) | 응용형 로드밸런서 리스트 |
| InstanceCount | Integer | 인스턴스 수량 |
| InServiceInstanceCount | Integer | `IN_SERVICE` 상태인 인스턴스 수량 |
| LaunchConfigurationId | String | 시동 구성 ID |
| LaunchConfigurationName | String | 시동 구성 이름 |
| LoadBalancerIdSet | Array of String | 기존형 로드밸런서 ID 리스트 |
| MaxSize | Integer | 최대 인스턴스 수 |
| MinSize | Integer | 최소 인스턴스 수 |
| ProjectId | Integer | 프로젝트 ID |
| SubnetIdSet | Array of String | 서브넷 ID 리스트 |
| TerminationPolicySet | Array of String | 폐기 전략 |
| VpcId | String | VPC 표시 |
| ZoneSet | Array of String | 가용 영역 리스트 |
| RetryPolicy | String | 다시 시도 전략 |

## AutoScalingGroupAbstract

조정 그룹 개요입니다.

API: DescribeLaunchConfigurations에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| AutoScalingGroupId | String | 조정 그룹 ID. |
| AutoScalingGroupName | String | 조정 그룹 이름. |

## DataDisk

시동 구성의 데이터 디스크 구성 정보입니다. 해당 매개변수를 지정하지 않으면 기본적으로 데이터 디스크를 구매하지 않습니다. 현재는 구매 시 하나의 데이터 디스크만 지정할 수 있습니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| DiskType | String | 아니요 | 데이터 디스크 유형입니다. 데이터 디스크 유형 제한은 [CVM 인스턴스 구성](https://cloud.tencent.com/document/product/213/2177)을 참조하십시오. 값 범위: <br><li>LOCAL_BASIC: 로컬 디스크<br><li>LOCAL_SSD: 로컬 SSD 디스크<br><li>CLOUD_BASIC: HDD 클라우드 디스크<br><li>CLOUD_PREMIUM: 프리미엄 클라우드 디스크<br><li>CLOUD_SSD: SSD 클라우드 디스크<br><br> 기본 값: LOCAL_BASIC입니다. |
| DiskSize | Integer | 아니요 | 데이터 디스크 크기, 단위: GB. 최소 조정 단위는 10G, 서로 다른 유형의 데이터 디스크는 값이 다릅니다. 구체적인 제한은 [CVM 인스턴스 구성](https://cloud.tencent.com/document/product/213/2177)을 참조하십시오. 기본값은 0으로 데이터 디스크 구매하지 않음을 표시합니다. 더 많은 제한은 제품 문서를 참조하십시오. |
| SnapshotId | String | 아니요 | 데이터 디스크 스냅샷 ID, 형식은 `snap-l8psqwnt`와 유사합니다. |

## EnhancedService

인스턴스의 강화형 서비스 활성화 상황과 해당 설정을 설명합니다. 예를 들어 보안, CM 등 인스턴스 Agent입니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | 아니요 | 클라우드 보안 서비스를 활성화합니다. 해당 매개변수를 지정하지 않으면 클라우드 보안 서비스를 기본으로 활성화합니다. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | 아니요 | CM 서비스를 활성화합니다. 해당 매개변수를 지정하지 않으면 CM 서비스를 기본으로 활성화합니다. |

## Filter

> 키-값 쌍 필터, 조건 필터링 조회에 사용합니다. 예를 들어 필터링 ID, 이름, 상태 등입니다.
> * 여러 개의 `Filter`가 존재하는 경우, `Filter` 간 관계는 논리곱(`AND`)입니다.
> * 동일한 `Filter`에 여러 개의 `Values`가 존재하면 동일한 `Filter`하의 `Values` 간의 관계는 논리합(`OR`)입니다.
>
> [DescribeInstances](https://cloud.tencent.com/document/api/213/9388) API의 `Filter`를 예로 들자면 가용 영역(`zone`)이 광저우 1지역 ***그리고*** 요금제(`instance-charge-type`)가 연/월정액 ***또는*** 사용량 기반 요금제인 인스턴스를 조회해야 하는 경우 다음과 같이 구현할 수 있습니다.
```
Filters.1.Name=zone
&Filters.1.Values.1=ap-guangzhou-1
&Filters.2.Name=instance-charge-type
&Filters.2.Values.1=PREPAID
&Filters.3.Values.2=POSTPAID_BY_HOUR
```

API: DescribeAutoScalingActivities, DescribeAutoScalingGroups, DescribeAutoScalingInstances, DescribeLaunchConfigurations, DescribeScheduledActions에 참조됩니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| Name | String | 예 | 필터링할 필드. |
| Values | Array of String | 예 | 필드의 필터링. |

## ForwardLoadBalancer

응용형 로드밸런서

API: CreateAutoScalingGroup, DescribeAutoScalingGroups odifyLoadBalancers에 참조됩니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| LoadBalancerId | String | 에 | 로드밸런서 ID |
| ListenerId | String | 예 | 응용형 로드밸런싱 수신기 ID |
| TargetAttributes | Array of [TargetAttribute](#TargetAttribute) | 예 | 목표 규칙 속성 리스트 |
| LocationId | String | 아니요 | 포워딩 규칙 ID |

## Instance

인스턴스 정보

API: DescribeAutoScalingInstances에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| InstanceId | String | 인스턴스 ID |
| AutoScalingGroupId | String | 조정 그룹 ID |
| LaunchConfigurationId | String | 시동 구성 ID |
| LaunchConfigurationName | String | 시동 구성 이름 |
| LifeCycleState | String | 생명 주기 상태, 가능한 값은 IN_SERVICE, CREATING, TERMINATING, ATTACHING, DETACHING, ATTACHING_LB, DETACHING_LB 등이 있습니다. |
| HealthStatus | String | 정상 상태, 가능한 값은 HEALTHY와 UNHEALTHY입니다 |
| ProtectedFromScaleIn | Boolean | 축소 보호 여부 |
| Zone | String | 가용 영역 |
| CreationType | String | 생성 유형, 가능한 값은 AUTO_CREATION, MANUAL_ATTACHING입니다. |
| AddTime | Timestamp | 인스턴스 추가 시간 |
| InstanceType | String | 인스턴스 유형 |

## InstanceMarketOptionsRequest

CVM 비딩 요청 관련 선택 사항

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| SpotOptions | [SpotMarketOptions](#SpotMarketOptions) | 예 | 비딩 관련 옵션 |
| MarketType | String | 아니요 | 마켓 옵션 유형, 현재 가능한 값은 Spot만입니다. |

## InternetAccessible

시동 구성으로 생성한 인스턴스의 공중망 접근 가능성, 인스턴스의 공중망 접근 요금제, 최대 대역폭 등을 설명합니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| InternetChargeType | String | 아니요 | 네트워크 요금제. 가능한 값: <br><li>BANDWIDTH_PREPAID: 대역폭에 따른 선불제 <br><li>TRAFFIC_POSTPAID_BY_HOUR: 트래픽 시간별 후불제<br><li>BANDWIDTH_POSTPAID_BY_HOUR: 대역폭 시간별 후불제 <br><li>BANDWIDTH_PACKAGE: 대역폭 패키지 <br> 기본 값은 TRAFFIC_POSTPAID_BY_HOUR입니다. |
| InternetMaxBandwidthOut | Integer | 아니요 | 공중망 아웃바운드 대역폭 상한, 단위는 Mbps, 기본 값은 0Mbps입니다. 모델에 따라 대역폭 상한이 달라집니다. 구체적인 제한은 [구매한 네트워크 대역폭](https://cloud.tencent.com/document/product/213/509)을 참조하십시오. |
| PublicIpAssigned | Boolean | 아니요 | 공인 IP 할당 여부입니다. 가능한 값: <br><li>TRUE: 공인 IP 할당<br><li>FALSE: 공인 IP 할당하지 않음<br><br>공중망 대역폭이 0Mbps보다 클 경우 자유롭게 개통 여부를 선택할 수 있고 기본적으로 공인 IP를 활성화합니다. 공중망 대역폭이 0인 경우, 공인 IP의 할당을 허용하지 않습니다. |

## LaunchConfiguration

조건에 부합하는 시동 구성 정보의 집합입니다.

API: DescribeLaunchConfigurations에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ProjectId | Integer | 인스턴스 소속 프로젝트 ID. |
| LaunchConfigurationId | String | 시동 구성 ID. |
| LaunchConfigurationName | String | 시동 구성 이름. |
| InstanceType | String | 인스턴스 모델. |
| SystemDisk | [SystemDisk](#SystemDisk) | 인스턴스 시스템 디스크 정보. |
| DataDisks | Array of [DataDisk](#DataDisk) | 인스턴스 데이터 디스크 구성 정보. |
| LoginSettings | [LimitedLoginSettings](#LimitedLoginSettings) | 인스턴스 로그인 설정. |
| InternetAccessible | [InternetAccessible](#InternetAccessible) | 공중망 대역폭 관련 정보 설정. |
| SecurityGroupIds | Array of String | 인스턴스 소속 보안 그룹. |
| AutoScalingGroupAbstractSet | Array of [AutoScalingGroupAbstract](#AutoScalingGroupAbstract) | 시동 구성 관련 조정 그룹. |
| UserData | String | 사용자 지정 데이터. |
| CreatedTime | Timestamp | 시동 구성 생성 시간. |
| EnhancedService | [EnhancedService](#EnhancedService) | 인스턴스의 강화형 서비스 활성화 상태 및 관련 설정. |
| ImageId | String | 이미지 ID. |
| LaunchConfigurationStatus | String | 시동 구성 현재 상태입니다. 가능한 값: <br><li>NORMAL: 정상<br><li>IMAGE_ABNORMAL: 시동 구성 이미지 이상<br><li>CBS_SNAP_ABNORMAL: 시동 구성 데이터 디스크 스냅샷 이상<br><li>SECURITY_GROUP_ABNORMAL: 시동 구성 보안 그룹 이상<br> |
| InstanceChargeType | String | 인스턴스 요금제, CVM 기본값은 POSTPAID_BY_HOUR입니다.<br/><br><li>POSTPAID_BY_HOUR: 시간별 후불제<br/><br><li>SPOTPAID: 비딩 지불 |
| InstanceMarketOptions | [InstanceMarketOptionsRequest](#InstanceMarketOptionsRequest) | 인스턴스의 마켓 관련 옵션, 예를 들어 스팟 인스턴스 관련 매개변수입니다. 지정한 인스턴스의 요금제가 비딩 지불이면 해당 매개변수는 반드시 전달합니다. |
| InstanceTypes | Array of String | 인스턴스 모델 리스트. |

## LimitedLoginSettings

인스턴스 로그인 관련 구성과 정보를 설명합니다. 보안성을 고려하여 민감한 정보는 설명하지 않습니다. 

API: DescribeLaunchConfigurations에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| KeyIds | Array of String | 키 ID 리스트. |

## LoginSettings

인스턴스 로그인 관련 구성과 정보를 설명합니다.

API: CreateLaunchConfiguration에 참조됩니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| Password | String | 아니요 | 인스턴스 로그인 비밀번호입니다. 운영 체제에 따라 비밀번호 복잡도 제한은 달라집니다. 다음과 같습니다. <br><li>Linux 인스턴스 비밀번호는 반드시 8 ~ 16자리이고 [a-z, A-Z], [0-9] 및 [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]의 특수 문자 중 적어도 두 가지를 포함해야 합니다.<br><li>Windows 인스턴스 비밀번호는 반드시 12 ~ 16자리이고 [a-z], [A-Z], [0-9] 및 [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]의 특수 문자 중 적어도 세 가지를 포함해야 합니다.<br><br>해당 매개변수를 지정하지 않으면 시스템에서 랜덤으로 비밀번호를 생성하고 내부 메시지를 통해 사용자에게 발송합니다. |
| KeyIds | Array of String | 아니요 | 키 ID 리스트. 키 연결 후 대응하는 개인 키를 통해 인스턴스에 액세스할 수 있습니다. KeyId 는 DescribeKeyPairs API를 통해 획득할 수 있고 키와 비밀번호는 동시에 지정할 수 없으며, Windows 운영 체제는 키 지정을 지원하지 않습니다. 현재는 구매 시 하나의 키 지정만 지원합니다. |
| KeepImageLogin | Boolean | 아니요 | 이미지의 원본 설정을 유지합니다. 해당 매개변수와 Password 또는 KeyIds.N은 동시에 지정할 수 없습니다. 사용자 지정 이미지, 공유 이미지 또는 외부에서 가져온 이미지를 사용하여 인스턴스를 지정할 때만 해당 매개변수를 TRUE로 지정할 수 있습니다. 가능한 값:<br><li>TRUE: 이미지의 로그인 설정 유지<br><li>FALSE: 이미지의 로그인 설정 유지하지 않음<br><br>기본 값은 FALSE입니다. |

## RunMonitorServiceEnabled

"CM" 서비스 관련 정보를 설명합니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| Enabled | Boolean | 아니요 | [CM](https://cloud.tencent.com/document/product/248) 서비스 활성화 여부입니다. 가능한 값 범위:<br><li>TRUE: Cloud Monitoring 서비스 활성화 <br><li>FALSE: Cloud Monitoring 서비스 활성화하지 않음<br><br> 기본 값은 TRUE입니다. |

## RunSecurityServiceEnabled

"클라우드 보안" 서비스 관련 정보를 설명합니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| Enabled | Boolean | 아니요 | [클라우드 보안](https://cloud.tencent.com/document/product/296) 서비스 활성화 여부입니다. 가능한 값 범위: <br><li>TRUE: 클라우드 보안 서비스 활성화<br><li>FALSE: 클라우드 보안 서비스를 활성화하지 않음<br><br>기본 값은 TRUE입니다. |

## ScheduledAction

시간 제한 태스크 정보 설명

API: DescribeScheduledActions에 참조됩니다.

| 이름 | 유형 | 설명 |
|------|------|-------|
| ScheduledActionId | String | 시간 제한 태스크 ID. |
| ScheduledActionName | String | 시간 제한 태스크 이름. |
| AutoScalingGroupId | String | 시간 제한 태스크 속한 조정 그룹 ID. |
| StartTime | Timestamp | 시간 제한 태스크의 시작 시간입니다. 값은 `베이징 시간`(UTC+8)으로 `ISO8601` 표준에 따르며 형식은 `YYYY-MM-DDThh:mm:ss+08:00`입니다. |
| Recurrence | String | 시간 제한 태스크 중복 방식. |
| EndTime | Timestamp | 시간 제한 태스크의 종료 시간입니다. 값은 `베이징 시간`(UTC+8)으로 `ISO8601` 표준에 따르며 형식은 `YYYY-MM-DDThh:mm:ss+08:00`입니다. |
| MaxSize | Integer | 시간 제한 태스크에 설정한 최대 인스턴스 수. |
| DesiredCapacity | Integer | 시간 제한 태스크에 설정한 에상 인스턴스 수. |
| MinSize | Integer | 시간 제한 태스크에 설정한 최소 인스턴스 수. |
| CreatedTime | Timestamp | 시간 제한 태스크의 생성 시간입니다. 값은 `UTC` 시간으로 `ISO8601` 표준에 따르며 형식은 `YYYY-MM-DDThh:mm:ssZ`입니다. |

## SpotMarketOptions

비딩 관련 옵션

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| MaxPrice | String | 예 | 비딩 가격, 예: 1.05 |
| SpotInstanceType | String | 아니요 | 비딩 요청 유형, 현재는 one-time 유형만 지원하며, 기본 값은 one-time입니다. |

## SystemDisk

시동 구성의 시스템 디스크 구성 정보입니다. 해당 매개변수를 지정하지 않으면 시스템 기본값에 따라 할당합니다.

API: CreateLaunchConfiguration, DescribeLaunchConfigurations에 참조욉니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| DiskType | String | 아니요 | 시스템 디스크 유형입니다. 시스템 디스크 유형 제한의 상세한 내용은 [CVM 인스턴스 구성](https://cloud.tencent.com/document/product/213/2177)을 참조하십시오. 가능한 값 범위: <br><li>LOCAL_BASIC: 로컬 디스크<br><li>LOCAL_SSD: 로컬 SSD 디스크<br><li>CLOUD_BASIC: HDD 클라우드 디스크<br><li>CLOUD_PREMIUM: 프리미엄 클라우드 디스크<br><li>CLOUD_SSD: SSD 클라우드 디스크<br><br>기본 값은 LOCAL_BASIC입니다. |
| DiskSize | Integer | 아니요 | 시스템 디크스 크기, 단위는 GB입니다. 기본값은 50입니다. |

## TargetAttribute

로드밸런서 목표 속성

API: CreateAutoScalingGroup, DescribeAutoScalingGroups odifyLoadBalancers에 참조됩니다.

| 이름 | 유형 | 필수 선택 항목 | 설명 |
|------|------|----------|------|
| Port | Integer | 예 | 포트 |
| Weight | Integer | 예 | 가중치 |


