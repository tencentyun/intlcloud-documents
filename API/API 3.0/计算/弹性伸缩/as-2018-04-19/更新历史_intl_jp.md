## 第8回目のリリース

リリース時間：2019-02-14 16:01:19

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

データ構造の変更：

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* **メンバーの変更：**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## 第7回目のリリース

リリース時間：2019/01/24 17:23:35

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [ModifyLoadBalancers](/document/api/377/32868)

APIの変更：

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)
	* パラメータの追加：UserData

## 第6回目のリリース

リリース時間：2018/12/27 19:18:13

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

データ構造の変更：

* [DataDisk](/document/api/377/20453#DataDisk)
	* メンバーの追加：SnapshotId

## 第5回目のリリース

リリース時間：2018/12/19 10:09:33

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [DescribeAutoScalingActivities](/document/api/377/31735)

データ構造の追加：

* [Activity](/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](/document/api/377/20453#ActivtyRelatedInstance)

## 第4回目のリリース

リリース時間：2018/12/06 18:57:45

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [ModifyLaunchConfigurationAttributes](/document/api/377/31298)

APIの変更：

* [CreateAutoScalingGroup](/document/api/377/20440)
	* パラメータの追加：ZonesCheckPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* パラメータの追加：InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* パラメータの追加：ZonesCheckPolicy

## 第3回目のリリース

リリース時間：2018/11/15 15:42:48

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの変更：

* [CreateAutoScalingGroup](/document/api/377/20440)
	* パラメータの追加：RetryPolicy
* [CreateLaunchConfiguration](/document/api/377/20447)
	* パラメータの追加：InstanceTypes
	* **パラメータの変更：**InstanceType
* [ModifyAutoScalingGroup](/document/api/377/20433)
	* パラメータの追加：RetryPolicy

データ構造の変更：

* [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup)
	* メンバーの追加：RetryPolicy
* [Instance](/document/api/377/20453#Instance)
	* メンバーの追加：InstanceType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* メンバーの追加：InstanceTypes

## 第2回目のリリース

リリース時間：2018/10/19 17:44:13

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの変更：

* [CreateLaunchConfiguration](/document/api/377/20447)
	* パラメータの追加：InstanceChargeType、InstanceMarketOptions

データ構造の追加：

* [InstanceMarketOptionsRequest](/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](/document/api/377/20453#SpotMarketOptions)

データ構造の変更：

* [Instance](/document/api/377/20453#Instance)
	* **メンバーの変更：**CreationType
* [LaunchConfiguration](/document/api/377/20453#LaunchConfiguration)
	* メンバーの追加：InstanceChargeType、InstanceMarketOptions

## 第1回目のリリース

リリース時間：2018/10/11 15:37:12

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

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

データ構造の追加：

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


