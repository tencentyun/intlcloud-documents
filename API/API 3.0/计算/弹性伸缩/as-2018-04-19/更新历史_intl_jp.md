## 第8回目のリリース

リリース時間：2019-02-14 16:01:19

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

データ構造の変更：

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* **メンバーの変更：**DefaultCooldown, DesiredCapacity, InstanceCount, InServiceInstanceCount, MaxSize, MinSize, ProjectId

## 第7回目のリリース

リリース時間：2019/01/24 17:23:35

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [ModifyLoadBalancers](https://cloud.tencent.com/document/api/377/32868)

APIの変更：

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)
	* パラメータの追加：UserData

## 第6回目のリリース

リリース時間：2018/12/27 19:18:13

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

データ構造の変更：

* [DataDisk](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#DataDisk)
	* メンバーの追加：SnapshotId

## 第5回目のリリース

リリース時間：2018/12/19 10:09:33

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [DescribeAutoScalingActivities](https://cloud.tencent.com/document/api/377/31735)

データ構造の追加：

* [Activity](https://cloud.tencent.com/document/api/377/20453#Activity)
* [ActivtyRelatedInstance](https://cloud.tencent.com/document/api/377/20453#ActivtyRelatedInstance)

## 第4回目のリリース

リリース時間：2018/12/06 18:57:45

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

* [ModifyLaunchConfigurationAttributes](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/31298)

APIの変更：

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* パラメータの追加：ZonesCheckPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* パラメータの追加：InstanceTypesCheckPolicy
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* パラメータの追加：ZonesCheckPolicy

## 第3回目のリリース

リリース時間：2018/11/15 15:42:48

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの変更：

* [CreateAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20440)
	* パラメータの追加：RetryPolicy
* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* パラメータの追加：InstanceTypes
	* **パラメータの変更：**InstanceType
* [ModifyAutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20433)
	* パラメータの追加：RetryPolicy

データ構造の変更：

* [AutoScalingGroup](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#AutoScalingGroup)
	* メンバーの追加：RetryPolicy
* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* メンバーの追加：InstanceType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* メンバーの追加：InstanceTypes

## 第2回目のリリース

リリース時間：2018/10/19 17:44:13

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの変更：

* [CreateLaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20447)
	* パラメータの追加：InstanceChargeType、InstanceMarketOptions

データ構造の追加：

* [InstanceMarketOptionsRequest](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#InstanceMarketOptionsRequest)
* [SpotMarketOptions](https://cloud.tencent.com/document/api/377/20453#SpotMarketOptions)

データ構造の変更：

* [Instance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#Instance)
	* **メンバーの変更：**CreationType
* [LaunchConfiguration](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20453#LaunchConfiguration)
	* メンバーの追加：InstanceChargeType、InstanceMarketOptions

## 第1回目のリリース

リリース時間：2018/10/11 15:37:12

今回のリリースは以下の内容を含みます：

既存のドキュメントの改善。

APIの追加：

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

データ構造の追加：

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


