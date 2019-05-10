## 제8차 런칭

런칭 시간: 2019-02-14 16:01:19

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

데이터 구조 수정:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* **수정된 멤버:**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## 제7차 런칭

런칭 시간: 2019-01-24 17:23:35

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [ModifyLoadBalancers](/document/api/377/32868)

수정된 API:

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)
	* 새로 추가된 입력 매개변수: UserData

## 제6차 런칭

런칭 시간: 2018-12-27 19:18:13

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

데이터 구조 수정:

* [DataDisk](/document/api/377/20453#DataDisk)
	* 새로 추가된 멤버: SnapshotId

## 제5차 런칭

런칭 시간: 2018-12-19 10:09:33

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [DescribeAutoScalingActivities](/document/api/377/31735)

새로 추가된 데이터 구조:

* [Activity](/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](/document/api/377/20453#ActivtyRelatedInstance)

## 제4차 런칭

런칭 시간: 2018-12-06 18:57:45

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)

수정된 API:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* 새로 추가된 입력 매개변수: ZonesCheckPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* 새로 추가된 입력 매개변수: ZonesCheckPolicy

## 제3차 런칭

런칭 시간: 2018-11-15 15:42:48

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

수정된 API:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* 새로 추가된 입력 매개변수: RetryPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceTypes
	* **수정된 입력 매개변수:** InstanceType
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* 새로 추가된 입력 매개변수: RetryPolicy

데이터 구조 수정:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* 새로 추가된 멤버: RetryPolicy
* [Instance](/document/api/377/20453#Instance)
	* 새로 추가된 멤버: InstanceType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* 새로 추가된 멤버: InstanceTypes

## 제2차 런칭

런칭 시간: 2018-10-19 17:44:13

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

수정된 API:

* [CreateLaunchConfiguration](/document/api/377/20447)
	* 새로 추가된 입력 매개변수: InstanceChargeType, InstanceMarketOptions

새로 추가된 데이터 구조:

* [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](/document/api/377/20453#SpotMarketOptions)

데이터 구조 수정:

* [Instance](/document/api/377/20453#Instance)
	* **수정된 멤버:** CreationType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* 새로 추가된 멤버: InstanceChargeType, InstanceMarketOptions

## 제1차 런칭

런칭 시간: 2018-10-11 15:37:12

이번 런칭은 다음의 내용을 포함합니다.

기존의 문서를 개선했습니다.

새로 추가된 API:

* [AttachInstances](/document/api/377/20441)
* [CreateAutoScalingGroup](/document/api/377/20440)
* [CreateLaunchConfiguration](/document/api/377/20447)
* [CreateScheduledAction](/document/api/377/20452)
* [DeleteAutoScalingGroup](/document/api/377/20439)
* [DeleteLaunchConfiguration](/document/api/377/20446)
* [DeleteScheduledAction](/document/api/377/20451)
* [DescribeAccountLimits](/document/api/377/20443)
* [DescribeAutoScalingGroups](/document/api/377/20438)
* [DescribeAutoScalingInstances](/document/api/377/20437)
* [DescribeLaunchConfigurations](/document/api/377/20445)
* [DescribeScheduledActions](/document/api/377/20450)
* [DetachInstances](/document/api/377/20436)
* [DisableAutoScalingGroup](/document/api/377/20435)
* [EnableAutoScalingGroup](/document/api/377/20434)
* [ModifyAutoScalingGroup](/document/api/377/20433)
* [ModifyDesiredCapacity](/document/api/377/20432)
* [ModifyScheduledAction](/document/api/377/20449)
* [RemoveInstances](/document/api/377/20431)

새로 추가된 데이터 구조:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
* [AutoScalingGroupAbstract](/document/api/377/20453#AutoScalingGroupAbstract)
* [DataDisk](/document/api/377/20453#DataDisk)
* [EnhancedService](/document/api/377/20453#EnhancedService)
* [Filter](/document/api/377/20453#Filter)
* [ForwardLoadBalancer](/document/api/377/20453#ForwardLoadBalancer)
* [Instance](/document/api/377/20453#Instance)
* [InternetAccessible](/document/api/377/20453#InternetAccessible)
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
* [LimitedLoginSettings](/document/api/377/20453#LimitedLoginSettings)
* [LoginSettings](/document/api/377/20453#LoginSettings)
* [RunMonitorServiceEnabled](/document/api/377/20453#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](/document/api/377/20453#RunSecurityServiceEnabled)
* [ScheduledAction](/document/api/377/20453#ScheduledAction)
* [SystemDisk](/document/api/377/20453#SystemDisk)
* [TargetAttribute](/document/api/377/20453#TargetAttribute)


