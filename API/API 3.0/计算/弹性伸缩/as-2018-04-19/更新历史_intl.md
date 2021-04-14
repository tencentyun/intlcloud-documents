## Release 16

Release time: July 12, 2019 11:37:21

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* New input parameters: ServiceSettings
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* New input parameters: CamRoleName
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* New input parameters: ServiceSettings
* [UpgradeLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/35199)
	* New input parameters: CamRoleName

New data structures:

* [ServiceSettings](https://cloud.tencent.com/document/api/377/20453#ServiceSettings)

Modified data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* New members: ServiceSettings
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* New members: CamRoleName

## Release 15

Release time: June 13, 2019 16:13:04

This release contains:

Improvements on existing documentation

New APIs:

* [ExecuteScalingPolicy](https://cloud.tencent.com/document/api/377/35477)

## Release 14

Release time: June 6, 2019 20:15:07

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* New input parameters: Tags

New data structures:

* [Tag](https://cloud.tencent.com/document/api/377/20453#Tag)

Modified data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* New member added: Tags

## Release 13

Release time: May 30, 2019 19:51:36

This release contains:

Improvements on existing documentation

New APIs:

* [UpgradeLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/35199)

Modified APIs:

* [AttachInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20441)
	* New output parameters: ActivityId
* [DetachInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20436)
	* New output parameters: ActivityId
* [RemoveInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20431)
	* New output parameters: ActivityId

Modified data structures:

* [LifecycleHook](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LifecycleHook)
	* **Modify members:** NotificationTarget
* [ScalingPolicy](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#ScalingPolicy)
	* **Modified members:** AdjustmentValue

## Release 12

Release time: May 16, 2019 19:38:05

This release contains:

Improvements on existing documentation

Modified data structures:

* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* New members: VersionNumber
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* New members: VersionNumber, UpdatedTime

## Release 11

Release time: April 25, 2019 19:24:45

This release contains:

Improvements on existing documentation

New APIs:

* [CompleteLifecycleAction](https://cloud.tencent.com/document/api/377/34455)
* [CreateLifecycleHook](https://cloud.tencent.com/document/api/377/34454)
* [CreatePaiInstance](https://cloud.tencent.com/document/api/377/34459)
* [DeleteLifecycleHook](https://cloud.tencent.com/document/api/377/34453)
* [DescribeLifecycleHooks](https://cloud.tencent.com/document/api/377/34452)
* [DescribePaiInstances](https://cloud.tencent.com/document/api/377/34458)
* [PreviewPaiDomainName](https://cloud.tencent.com/document/api/377/34457)
* [UpgradeLifecycleHook](https://cloud.tencent.com/document/api/377/34451)

Modified APIs:

* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* New input parameters: InstanceTags

New data structures:

* [InstanceChargePrepaid](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#InstanceChargePrepaid)
* [InstanceTag](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#InstanceTag)
* [LifecycleHook](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LifecycleHook)
* [NotificationTarget](https://cloud.tencent.com/document/api/377/20453#NotificationTarget)
* [PaiInstance](https://cloud.tencent.com/document/api/377/20453#PaiInstance)

Modified data structures:

* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceTags

## Release 10

Release time: March 8, 2019 17:33:58

This release contains:

Improvements on existing documentation

Modified data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* New members: InActivityStatus

## The 9th Release

Release time: February 22, 2019 14:42:40

This release contains:

Improvements on existing documentation

New APIs:

* [CreateNotificationConfiguration](https://cloud.tencent.com/document/api/377/33185)
* [CreateScalingPolicy](https://cloud.tencent.com/document/api/377/33180)
* [DeleteNotificationConfiguration](https://cloud.tencent.com/document/api/377/33184)
* [DeleteScalingPolicy](https://cloud.tencent.com/document/api/377/33179)
* [DescribeNotificationConfigurations](https://cloud.tencent.com/document/api/377/33183)
* [DescribeScalingPolicies](https://cloud.tencent.com/document/api/377/33178)
* [ModifyNotificationConfiguration](https://cloud.tencent.com/document/api/377/33182)
* [ModifyScalingPolicy](https://cloud.tencent.com/document/api/377/33177)
* [SetInstancesProtection](https://cloud.tencent.com/document/api/377/33175)

Modified APIs:

* [DescribeAutoScalingActivities](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31735)
	* New input parameters: StartTime, EndTime

New data structures:

* [AutoScalingNotification](https://cloud.tencent.com/document/api/377/20453#AutoScalingNotification)
* [MetricAlarm](https://cloud.tencent.com/document/api/377/20453#MetricAlarm)
* [ScalingPolicy](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#ScalingPolicy)

## Release 8

Release time: February 14, 2019 16:01:19

This release contains:

Improvements on existing documentation

Modified data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* **Modified members:** DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## Release 7

Release time: January 24, 2019 17:23:35

This release contains:

Improvements on existing documentation

New APIs:

* [ModifyLoadBalancers](https://cloud.tencent.com/document/api/377/32868)

Modified APIs:

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)
	* New input parameters: UserData

## Release 6

Release time: December 27, 2018 19:18:13

This release contains:

Improvements on existing documentation

Modified data structures:

* [DataDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#DataDisk)
	* New members: SnapshotId

## Release 5

Release time: December 19, 2018 10:09:33

This release contains:

Improvements on existing documentation

New APIs:

* [DescribeAutoScalingActivities](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31735)

New data structures:

* [Activity](https://cloud.tencent.com/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](https://cloud.tencent.com/document/api/377/20453#ActivtyRelatedInstance)

## Release 4

Release time: December 6, 2018 18:57:45

This release contains:

Improvements on existing documentation

New APIs:

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)

Modified APIs:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* New input parameters: ZonesCheckPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* New input parameters: InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* New input parameters: ZonesCheckPolicy

## Release 3

Release time: November 15, 2018 15:42:48

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* New input parameters: RetryPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* New input parameters: InstanceTypes
	* **Modified input parameters:** InstanceType
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* New input parameters: RetryPolicy

Modified data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* New members: RetryPolicy
* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* New members: InstanceType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceTypes

## Release 2

Release time: October 19, 2018 17:44:13

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* New input parameters: InstanceChargeType, InstanceMarketOptions

New data structures:

* [InstanceMarketOptionsRequest](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](https://cloud.tencent.com/document/api/377/20453#SpotMarketOptions)

Modified data structures:

* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* **Modified members:** CreationType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 1

Release time: October 11, 2018 15:37:12

This release contains:

Improvements on existing documentation

New APIs:

* [AttachInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20441)
* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
* [CreateScheduledAction](https://cloud.tencent.com/document/api/377/20452)
* [DeleteAutoScalingGroup](https://cloud.tencent.com/document/api/377/20439)
* [DeleteLaunchConfiguration](https://cloud.tencent.com/document/api/377/20446)
* [DeleteScheduledAction](https://cloud.tencent.com/document/api/377/20451)
* [DescribeAccountLimits](https://cloud.tencent.com/document/api/377/20443)
* [DescribeAutoScalingGroups](https://cloud.tencent.com/document/api/377/20438)
* [DescribeAutoScalingInstances](https://cloud.tencent.com/document/api/377/20437)
* [DescribeLaunchConfigurations](https://cloud.tencent.com/document/api/377/20445)
* [DescribeScheduledActions](https://cloud.tencent.com/document/api/377/20450)
* [DetachInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20436)
* [DisableAutoScalingGroup](https://cloud.tencent.com/document/api/377/20435)
* [EnableAutoScalingGroup](https://cloud.tencent.com/document/api/377/20434)
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
* [ModifyDesiredCapacity](https://cloud.tencent.com/document/api/377/20432)
* [ModifyScheduledAction](https://cloud.tencent.com/document/api/377/20449)
* [RemoveInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20431)

New data structures:

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
* [AutoScalingGroupAbstract](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroupAbstract)
* [DataDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#DataDisk)
* [EnhancedService](https://cloud.tencent.com/document/api/377/20453#EnhancedService)
* [Filter](https://cloud.tencent.com/document/api/377/20453#Filter)
* [ForwardLoadBalancer](https://cloud.tencent.com/document/api/377/20453#ForwardLoadBalancer)
* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
* [InternetAccessible](https://cloud.tencent.com/document/api/377/20453#InternetAccessible)
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
* [LimitedLoginSettings](https://cloud.tencent.com/document/api/377/20453#LimitedLoginSettings)
* [LoginSettings](https://cloud.tencent.com/document/api/377/20453#LoginSettings)
* [RunMonitorServiceEnabled](https://cloud.tencent.com/document/api/377/20453#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](https://cloud.tencent.com/document/api/377/20453#RunSecurityServiceEnabled)
* [ScheduledAction](https://cloud.tencent.com/document/api/377/20453#ScheduledAction)
* [SystemDisk](https://cloud.tencent.com/document/api/377/20453#SystemDisk)
* [TargetAttribute](https://cloud.tencent.com/document/api/377/20453#TargetAttribute)

