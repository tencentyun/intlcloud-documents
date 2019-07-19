## Release 8

Release time: February 14, 2019 16:01:19

This release contains:

Improvement on existing documentation.

Modified data structure:

* [AutoScalingGroup](/document/api/377/31018#AutoScalingGroup)
	* **Modified members:**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## Release 7

Release time: January 24, 2019 17:23:35

This release contains:

Improvement on existing documentation.

New APIs:

* [ModifyLoadBalancers](/document/api/377/31006)

Modified APIs:

* [ModifyLaunchConfigurationAttributes](/document/api/377/30998)
	* New input parameters: UserData

## Release 6

Release time: December 27, 2018 19:18:13

This release contains:

Improvement on existing documentation.

Modified data structure:

* [DataDisk](/document/api/377/31018#DataDisk)
	* New members: SnapshotId

## Release 5

Release time: December 19, 2018 10:09:33

This release contains:

Improvement on existing documentation.

New APIs:

* [DescribeAutoScalingActivities](/document/api/377/31014)

New data structures:

* [Activity](/document/api/377/31018#Activity)
* [ActivtyRelatedInstance](/document/api/377/31018#ActivtyRelatedInstance)

## Release 4

Release time: December 6, 2018 18:57:45

This release contains:

Improvement on existing documentation.

New APIs:

* [ModifyLaunchConfigurationAttributes](/document/api/377/30998)

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/31016)
	* New input parameters: ZonesCheckPolicy
* [CreateLaunchConfiguration](/document/api/377/31001)
	* New input parameters: InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](/document/api/377/31008)
	* New input parameters: ZonesCheckPolicy

## Release 3

Release time: November 15, 2018 15:42:48

This release contains:

Improvement on existing documentation.

Modified APIs:

* [CreateAutoScalingGroup](/document/api/377/31016)
	* New input parameters: RetryPolicy
* [CreateLaunchConfiguration](/document/api/377/31001)
	* New input parameters: InstanceTypes
	* **Modified input parameters:** InstanceType
* [ModifyAutoScalingGroup](/document/api/377/31008)
	* New input parameters: RetryPolicy
	
Modified data structure:

* [AutoScalingGroup](/document/api/377/31018#AutoScalingGroup)
	* New members: RetryPolicy
* [Instance](/document/api/377/31018#Instance)
	* New members: InstanceType
* [LaunchConfiguration](/document/api/377/31018#LaunchConfiguration)
	* New members: InstanceTypes

## Release 2

Release time: October 19, 2018 17:44:13

This release contains:

Improvement on existing documentation.

Modified APIs:

* [CreateLaunchConfiguration](/document/api/377/31001)
	* New input parameters: InstanceChargeType, InstanceMarketOptions
	
New data structures:

* [InstanceMarketOptionsRequest](/document/api/377/31018#InstanceMarketOptionsRequest)
* [SpotMarketOptions](/document/api/377/31018#SpotMarketOptions)

Modified data structure:

* [Instance](/document/api/377/31018#Instance)
	* **Modified members:** CreationType
* [LaunchConfiguration](/document/api/377/31018#LaunchConfiguration)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 1

Release time: October 11, 2018 15:37:12

This release contains:

Improvement on existing documentation.

New APIs:

* [AttachInstances](/document/api/377/31017)
* [CreateAutoScalingGroup](/document/api/377/31016)
* [CreateLaunchConfiguration](/document/api/377/31001)
* [CreateScheduledAction](/document/api/377/30996)
* [DeleteAutoScalingGroup](/document/api/377/31015)
* [DeleteLaunchConfiguration](/document/api/377/31000)
* [DeleteScheduledAction](/document/api/377/30995)
* [DescribeAccountLimits](/document/api/377/31003)
* [DescribeAutoScalingGroups](/document/api/377/31013)
* [DescribeAutoScalingInstances](/document/api/377/31012)
* [DescribeLaunchConfigurations](/document/api/377/30999)
* [DescribeScheduledActions](/document/api/377/30994)
* [DetachInstances](/document/api/377/31011)
* [DisableAutoScalingGroup](/document/api/377/31010)
* [EnableAutoScalingGroup](/document/api/377/31009)
* [ModifyAutoScalingGroup](/document/api/377/31008)
* [ModifyDesiredCapacity](/document/api/377/31007)
* [ModifyScheduledAction](/document/api/377/30993)
* [RemoveInstances](/document/api/377/31005)

New data structures:

* [AutoScalingGroup](/document/api/377/31018#AutoScalingGroup)
* [AutoScalingGroupAbstract](/document/api/377/31018#AutoScalingGroupAbstract)
* [DataDisk](/document/api/377/31018#DataDisk)
* [EnhancedService](/document/api/377/31018#EnhancedService)
* [Filter](/document/api/377/31018#Filter)
* [ForwardLoadBalancer](/document/api/377/31018#ForwardLoadBalancer)
* [Instance](/document/api/377/31018#Instance)
* [InternetAccessible](/document/api/377/31018#InternetAccessible)
* [LaunchConfiguration](/document/api/377/31018#LaunchConfiguration)
* [LimitedLoginSettings](/document/api/377/31018#LimitedLoginSettings)
* [LoginSettings](/document/api/377/31018#LoginSettings)
* [RunMonitorServiceEnabled](/document/api/377/31018#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](/document/api/377/31018#RunSecurityServiceEnabled)
* [ScheduledAction](/document/api/377/31018#ScheduledAction)
* [SystemDisk](/document/api/377/31018#SystemDisk)
* [TargetAttribute](/document/api/377/31018#TargetAttribute)
