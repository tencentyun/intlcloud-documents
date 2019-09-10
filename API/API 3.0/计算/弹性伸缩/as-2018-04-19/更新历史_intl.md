## Release 16

Release time: July 12, 2019 11:37:21

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* New input parameters: ServiceSettings
* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: CamRoleName
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* New input parameters: ServiceSettings
* [UpgradeLaunchConfiguration](/document/api/377/35199)
	* New input parameters: CamRoleName

New data structures:

* [ServiceSettings](/document/api/377/20453#ServiceSettings)

Modified data structures:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* New members: ServiceSettings
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: CamRoleName

## Release 15

Release time: June 13, 2019 16:13:04

This release contains:

Improvements on existing documentation

New APIs:

* [ExecuteScalingPolicy](/document/api/377/35477)

## Release 14

Release time: June 6, 2019 20:15:07

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* New input parameters: Tags

New data structures:

* [Tag](/document/api/377/20453#Tag)

Modified data structures:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* New member added: Tags

## Release 13

Release time: May 30, 2019 19:51:36

This release contains:

Improvements on existing documentation

New APIs:

* [UpgradeLaunchConfiguration](/document/api/377/35199)

Modified APIs:

* [AttachInstances](/document/api/377/20441)
	* New output parameters: ActivityId
* [DetachInstances](/document/api/377/20436)
	* New output parameters: ActivityId
* [RemoveInstances](/document/api/377/20431)
	* New output parameters: ActivityId

Modified data structures:

* [LifecycleHook](/document/api/377/20453#LifecycleHook)
	* **Modify members:** NotificationTarget
* [ScalingPolicy](/document/api/377/20453#ScalingPolicy)
	* **Modified members:** AdjustmentValue

## Release 12

Release time: May 16, 2019 19:38:05

This release contains:

Improvements on existing documentation

Modified data structures:

* [Instance](/document/api/377/20453#Instance)
	* New members: VersionNumber
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: VersionNumber, UpdatedTime

## Release 11

Release time: April 25, 2019 19:24:45

This release contains:

Improvements on existing documentation

New APIs:

* [CompleteLifecycleAction](/document/api/377/34455)
* [CreateLifecycleHook](/document/api/377/34454)
* [CreatePaiInstance](/document/api/377/34459)
* [DeleteLifecycleHook](/document/api/377/34453)
* [DescribeLifecycleHooks](/document/api/377/34452)
* [DescribePaiInstances](/document/api/377/34458)
* [PreviewPaiDomainName](/document/api/377/34457)
* [UpgradeLifecycleHook](/document/api/377/34451)

Modified APIs:

* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceTags

New data structures:

* [InstanceChargePrepaid](/document/api/377/20453#InstanceChargePrepaid)
* [InstanceTag](/document/api/377/20453#InstanceTag)
* [LifecycleHook](/document/api/377/20453#LifecycleHook)
* [NotificationTarget](/document/api/377/20453#NotificationTarget)
* [PaiInstance](/document/api/377/20453#PaiInstance)

Modified data structures:

* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceTags

## Release 10

Release time: March 8, 2019 17:33:58

This release contains:

Improvements on existing documentation

Modified data structures:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* New members: InActivityStatus

## The 9th Release

Release time: February 22, 2019 14:42:40

This release contains:

Improvements on existing documentation

New APIs:

* [CreateNotificationConfiguration](/document/api/377/33185)
* [CreateScalingPolicy](/document/api/377/33180)
* [DeleteNotificationConfiguration](/document/api/377/33184)
* [DeleteScalingPolicy](/document/api/377/33179)
* [DescribeNotificationConfigurations](/document/api/377/33183)
* [DescribeScalingPolicies](/document/api/377/33178)
* [ModifyNotificationConfiguration](/document/api/377/33182)
* [ModifyScalingPolicy](/document/api/377/33177)
* [SetInstancesProtection](/document/api/377/33175)

Modified APIs:

* [DescribeAutoScalingActivities](/document/api/377/31735)
	* New input parameters: StartTime, EndTime

New data structures:

* [AutoScalingNotification](/document/api/377/20453#AutoScalingNotification)
* [MetricAlarm](/document/api/377/20453#MetricAlarm)
* [ScalingPolicy](/document/api/377/20453#ScalingPolicy)

## Release 8

Release time: February 14, 2019 16:01:19

This release contains:

Improvements on existing documentation

Modified data structures:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* **Modified members:** DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## Release 7

Release time: January 24, 2019 17:23:35

This release contains:

Improvements on existing documentation

New APIs:

* [ModifyLoadBalancers](/document/api/377/32868)

Modified APIs:

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)
	* New input parameters: UserData

## Release 6

Release time: December 27, 2018 19:18:13

This release contains:

Improvements on existing documentation

Modified data structures:

* [DataDisk](/document/api/377/20453#DataDisk)
	* New members: SnapshotId

## Release 5

Release time: December 19, 2018 10:09:33

This release contains:

Improvements on existing documentation

New APIs:

* [DescribeAutoScalingActivities](/document/api/377/31735)

New data structures:

* [Activity](/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](/document/api/377/20453#ActivtyRelatedInstance)

## Release 4

Release time: December 6, 2018 18:57:45

This release contains:

Improvements on existing documentation

New APIs:

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* New input parameters: ZonesCheckPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* New input parameters: ZonesCheckPolicy

## Release 3

Release time: November 15, 2018 15:42:48

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* New input parameters: RetryPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceTypes
	* **Modified input parameters:** InstanceType
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* New input parameters: RetryPolicy

Modified data structures:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* New members: RetryPolicy
* [Instance](/document/api/377/20453#Instance)
	* New members: InstanceType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceTypes

## Release 2

Release time: October 19, 2018 17:44:13

This release contains:

Improvements on existing documentation

Modified APIs:

* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceChargeType, InstanceMarketOptions

New data structures:

* [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](/document/api/377/20453#SpotMarketOptions)

Modified data structures:

* [Instance](/document/api/377/20453#Instance)
	* **Modified members:** CreationType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 1

Release time: October 11, 2018 15:37:12

This release contains:

Improvements on existing documentation

New APIs:

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

New data structures:

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

