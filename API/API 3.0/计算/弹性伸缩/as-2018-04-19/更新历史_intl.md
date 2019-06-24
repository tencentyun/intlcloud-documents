## Release 8

Release time: February 14, 2019 16:01:19

This release contains:

Improvement to existing documentation.

Modified data structure:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* **Modified members:**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## Release 7

Release time: January 24, 2019 17:23:35

This release contains:

Improvement to existing documentation.

New APIs:

* [ModifyLoadBalancers](/document/api/377/32868)

Modified APIs:

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)
	* New input parameters: UserData

## Release 6

Release time: December 27, 2018 19:18:13

This release contains:

Improvement to existing documentation.

Modified data structure:

* [DataDisk](/document/api/377/20453#DataDisk)
	* New members: SnapshotId

## Release 5

Release time: December 19, 2018 10:09:33

This release contains:

Improvement to existing documentation.

New APIs:

* [DescribeAutoScalingActivities](/document/api/377/31735)

New data structures:

* [Activity](/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](/document/api/377/20453#ActivtyRelatedInstance)

## Release 4

Release time: December 6, 2018 18:57:45

This release contains:

Improvement to existing documentation.

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

Improvement to existing documentation.

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/20440)
	* New input parameters: RetryPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceTypes
	* **Modified input parameters:** InstanceType
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* New input parameters: RetryPolicy
	
Modified data structure:

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* New members: RetryPolicy
* [Instance](/document/api/377/20453#Instance)
	* New members: InstanceType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceTypes

## Release 2

Release time: October 19, 2018 17:44:13

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateLaunchConfiguration](/document/api/377/20447)
	* New input parameters: InstanceChargeType, InstanceMarketOptions
	
New data structures:

* [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](/document/api/377/20453#SpotMarketOptions)

Modified data structure:

* [Instance](/document/api/377/20453#Instance)
	* **Modified members:** CreationType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 1

Release time: October 11, 2018 15:37:12

This release contains:

Improvement to existing documentation.

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
