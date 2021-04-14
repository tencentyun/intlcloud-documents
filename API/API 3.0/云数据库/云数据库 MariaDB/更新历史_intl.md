## The Second Release

Release time: 2018-09-27 7:27:29 PM

The following changes are contained in this release:

The existing documents were improved.

APIs added:

* [CloneAccount](https://cloud.tencent.com/document/api/237/20257)
* [DescribeSqlLogs](https://cloud.tencent.com/document/api/237/20256)

API modified:

* [DescribeDBInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16184)
	* New input parameters: IsFilterExcluster and ExclusterType
	* **Modified input parameters:** IsFilterVpc, VpcId, and SubnetId
	* **Modified output parameter:** TotalCount
* [DescribeDBLogFiles](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16162)
	* New output parameters: VpcPrefix and NormalPrefix
	* **Deleted output parameters:** Vpcprefix and Normalprefix
* [DescribeDBSlowLogs](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16159)
	* **Modified output parameters:** LockTimeSum, QueryCount, Total, and QueryTimeSum
* [ModifyDBParameters](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16153)
	* New output parameter: Result
	* **Deleted output parameter:** Config
* [UpgradeDBInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16189)
	* **Modified output parameter:** VoucherIds

Data structures added:

* [SqlLogItem](https://cloud.tencent.com/document/api/237/16191#SqlLogItem)

Data structure modified:

* [DBAccount](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#DBAccount)
	* New member: DelayThresh
* [DBInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#DBInstance)
	* New members: UniqueVpcId, UniqueSubnetId, OriginSerialId, NodeCount, IsTmp, ExclusterId, Id, Qps, Paymode, Locker, and StatusDesc
* [Deal](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#Deal)
	* New members: Count and PayMode
	* **Deleted member:** Quantity
* [LogFileInfo](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#LogFileInfo)
	* **Modified member:** Uri
* [ParamConstraint](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#ParamConstraint)
	* New member: String
* [ParamModifyResult](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#ParamModifyResult)
	* **Modified member:** Code
* [SlowLogData](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#SlowLogData)
	* **Modified members:** LockTimeAvg, LockTimeMax, LockTimeMin, LockTimeSum, QueryCount, QueryTimeAvg, QueryTimeMax, QueryTimeMin, QueryTimeSum, RowsExaminedSum, and RowsSentSum

## The 1st Release

Release time: 2018-04-24

The following changes are contained in this release:

The existing documents were improved.

APIs added:

* [CloseDBExtranetAccess](https://cloud.tencent.com/document/api/237/16179)
* [CopyAccountPrivileges](https://cloud.tencent.com/document/api/237/16169)
* [CreateAccount](https://cloud.tencent.com/document/api/237/16165)
* [CreateDBInstance](https://cloud.tencent.com/document/api/237/16180)
* [DeleteAccount](https://cloud.tencent.com/document/api/237/16171)
* [DescribeAccountPrivileges](https://cloud.tencent.com/document/api/237/16164)
* [DescribeAccounts](https://cloud.tencent.com/document/api/237/16167)
* [DescribeBackupTime](https://cloud.tencent.com/document/api/237/16182)
* [DescribeDBInstanceSpecs](https://cloud.tencent.com/document/api/237/16188)
* [DescribeDBInstances](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16184)
* [DescribeDBLogFiles](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16162)
* [DescribeDBParameters](https://cloud.tencent.com/document/api/237/16154)
* [DescribeDBPerformance](https://cloud.tencent.com/document/api/237/16160)
* [DescribeDBPerformanceDetails](https://cloud.tencent.com/document/api/237/16156)
* [DescribeDBResourceUsage](https://cloud.tencent.com/document/api/237/16158)
* [DescribeDBResourceUsageDetails](https://cloud.tencent.com/document/api/237/16157)
* [DescribeDBSlowLogs](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16159)
* [DescribeFlow](https://cloud.tencent.com/document/api/237/16177)
* [DescribeLogFileRetentionPeriod](https://cloud.tencent.com/document/api/237/16152)
* [DescribeOrders](https://cloud.tencent.com/document/api/237/16186)
* [DescribePrice](https://cloud.tencent.com/document/api/237/16175)
* [DescribeRenewalPrice](https://cloud.tencent.com/document/api/237/16181)
* [DescribeSaleInfo](https://cloud.tencent.com/document/api/237/16178)
* [DescribeUpgradePrice](https://cloud.tencent.com/document/api/237/16183)
* [GrantAccountPrivileges](https://cloud.tencent.com/document/api/237/16166)
* [InitDBInstances](https://cloud.tencent.com/document/api/237/16185)
* [ModifyAccountDescription](https://cloud.tencent.com/document/api/237/16170)
* [ModifyBackupTime](https://cloud.tencent.com/document/api/237/16173)
* [ModifyDBInstanceName](https://cloud.tencent.com/document/api/237/16190)
* [ModifyDBInstancesProject](https://cloud.tencent.com/document/api/237/16176)
* [ModifyDBParameters](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16153)
* [ModifyLogFileRetentionPeriod](https://cloud.tencent.com/document/api/237/16151)
* [OpenDBExtranetAccess](https://cloud.tencent.com/document/api/237/16174)
* [RenewDBInstance](https://cloud.tencent.com/document/api/237/16187)
* [ResetAccountPassword](https://cloud.tencent.com/document/api/237/16168)
* [UpgradeDBInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16189)

Data structures added:

* [ConstraintRange](https://cloud.tencent.com/document/api/237/16191#ConstraintRange)
* [DBAccount](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#DBAccount)
* [DBBackupTimeConfig](https://cloud.tencent.com/document/api/237/16191#DBBackupTimeConfig)
* [DBInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#DBInstance)
* [DBParamValue](https://cloud.tencent.com/document/api/237/16191#DBParamValue)
* [Deal](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#Deal)
* [InstanceSpec](https://cloud.tencent.com/document/api/237/16191#InstanceSpec)
* [LogFileInfo](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#LogFileInfo)
* [MonitorData](https://cloud.tencent.com/document/api/237/16191#MonitorData)
* [MonitorIntData](https://cloud.tencent.com/document/api/237/16191#MonitorIntData)
* [ParamConstraint](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#ParamConstraint)
* [ParamDesc](https://cloud.tencent.com/document/api/237/16191#ParamDesc)
* [ParamModifyResult](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#ParamModifyResult)
* [PerformanceMonitorSet](https://cloud.tencent.com/document/api/237/16191#PerformanceMonitorSet)
* [RegionInfo](https://cloud.tencent.com/document/api/237/16191#RegionInfo)
* [ResourceUsageMonitorSet](https://cloud.tencent.com/document/api/237/16191#ResourceUsageMonitorSet)
* [SlowLogData](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/237/16191#SlowLogData)
* [SpecConfigInfo](https://cloud.tencent.com/document/api/237/16191#SpecConfigInfo)
* [ZoneChooseInfo](https://cloud.tencent.com/document/api/237/16191#ZoneChooseInfo)
* [ZonesInfo](https://cloud.tencent.com/document/api/237/16191#ZonesInfo)


