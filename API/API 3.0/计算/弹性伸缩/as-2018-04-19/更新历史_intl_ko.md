## 제8차 런칭

런칭 시간: 2019-02-14 16:01:19

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

데이터 구조 수정:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* **수정된 멤버:**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## 제7차 런칭

런칭 시간: 2019-01-24 17:23:35

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [ModifyLoadBalancers](https://cloud.tencent.com/document/api/377/32868)

수정된 API:

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)
	* 새로 추가된 입력 매개변수: UserData

## 제6차 런칭

런칭 시간: 2018-12-27 19:18:13

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

데이터 구조 수정:

* [DataDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#DataDisk)
	* 새로 추가된 멤버: SnapshotId

## 제5차 런칭

런칭 시간: 2018-12-19 10:09:33

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [DescribeAutoScalingActivities](https://cloud.tencent.com/document/api/377/31735)

새로 추가된 데이터 구조:

* [Activity](https://cloud.tencent.com/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](https://cloud.tencent.com/document/api/377/20453#ActivtyRelatedInstance)

## 제4차 런칭

런칭 시간: 2018-12-06 18:57:45

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)

수정된 API:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* 새로 추가된 입력 매개변수: ZonesCheckPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* 새로 추가된 입력 매개변수: ZonesCheckPolicy

## 제3차 런칭

런칭 시간: 2018-11-15 15:42:48

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

수정된 API:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* 새로 추가된 입력 매개변수: RetryPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceTypes
	* **수정된 입력 매개변수:** InstanceType
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* 새로 추가된 입력 매개변수: RetryPolicy

데이터 구조 수정:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* 새로 추가된 멤버: RetryPolicy
* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* 새로 추가된 멤버: InstanceType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* 새로 추가된 멤버: InstanceTypes

## 제2차 런칭

런칭 시간: 2018-10-19 17:44:13

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

수정된 API:

* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceChargeType, InstanceMarketOptions

새로 추가된 데이터 구조:

* [InstanceMarketOptionsRequest](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](https://cloud.tencent.com/document/api/377/20453#SpotMarketOptions)

데이터 구조 수정:

* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* **수정된 멤버:** CreationType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* 새로 추가된 멤버: InstanceChargeType, InstanceMarketOptions

## 제1차 런칭

런칭 시간: 2018-10-11 15:37:12

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [AttachInstances](https://cloud.tencent.com/document/api/377/20441)
* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
* [CreateScheduledAction](https://cloud.tencent.com/document/api/377/20452)
* [DeleteAutoScalingGroup](https://cloud.tencent.com/document/api/377/20439)
* [DeleteLaunchConfiguration](https://cloud.tencent.com/document/api/377/20446)
* [DeleteScheduledAction](https://cloud.tencent.com/document/api/377/20451)
* [DescribeAccountLimits](https://cloud.tencent.com/document/api/377/20443)
* [DescribeAutoScalingGroups](https://cloud.tencent.com/document/api/377/20438)
* [DescribeAutoScalingInstances](https://cloud.tencent.com/document/api/377/20437)
* [DescribeLaunchConfigurations](https://cloud.tencent.com/document/api/377/20445)
* [DescribeScheduledActions](https://cloud.tencent.com/document/api/377/20450)
* [DetachInstances](https://cloud.tencent.com/document/api/377/20436)
* [DisableAutoScalingGroup](https://cloud.tencent.com/document/api/377/20435)
* [EnableAutoScalingGroup](https://cloud.tencent.com/document/api/377/20434)
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
* [ModifyDesiredCapacity](https://cloud.tencent.com/document/api/377/20432)
* [ModifyScheduledAction](https://cloud.tencent.com/document/api/377/20449)
* [RemoveInstances](https://cloud.tencent.com/document/api/377/20431)

새로 추가된 데이터 구조:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
* [AutoScalingGroupAbstract](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroupAbstract)
* [DataDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#DataDisk)
* [EnhancedService](https://cloud.tencent.com/document/api/377/20453#EnhancedService)
* [Filter](https://cloud.tencent.com/document/api/377/20453#Filter)
* [ForwardLoadBalancer](https://cloud.tencent.com/document/api/377/20453#ForwardLoadBalancer)
* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
* [InternetAccessible](https://cloud.tencent.com/document/api/377/20453#InternetAccessible)
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
* [LimitedLoginSettings](https://cloud.tencent.com/document/api/377/20453#LimitedLoginSettings)
* [LoginSettings](https://cloud.tencent.com/document/api/377/20453#LoginSettings)
* [RunMonitorServiceEnabled](https://cloud.tencent.com/document/api/377/20453#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](https://cloud.tencent.com/document/api/377/20453#RunSecurityServiceEnabled)
* [ScheduledAction](https://cloud.tencent.com/document/api/377/20453#ScheduledAction)
* [SystemDisk](https://cloud.tencent.com/document/api/377/20453#SystemDisk)
* [TargetAttribute](https://cloud.tencent.com/document/api/377/20453#TargetAttribute)


