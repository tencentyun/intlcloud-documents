## The Second Release

Release time: 2018-09-27 7:27:29 PM

The following changes are contained in this release:

The existing documents were improved.

APIs added:

* [CloneAccount](/document/api/237/20257)
* [DescribeSqlLogs](/document/api/237/20256)

API modified:

* [DescribeDBInstances](/document/api/237/16184)
	* New input parameters: IsFilterExcluster and ExclusterType
	* **Modified input parameters:** IsFilterVpc, VpcId, and SubnetId
	* **Modified output parameter:** TotalCount
* [DescribeDBLogFiles](/document/api/237/16162)
	* New output parameters: VpcPrefix and NormalPrefix
	* **Deleted output parameters:** Vpcprefix and Normalprefix
* [DescribeDBSlowLogs](/document/api/237/16159)
	* **Modified output parameters:** LockTimeSum, QueryCount, Total, and QueryTimeSum
* [ModifyDBParameters](/document/api/237/16153)
	* New output parameter: Result
	* **Deleted output parameter:** Config
* [UpgradeDBInstance](/document/api/237/16189)
	* **Modified output parameter:** VoucherIds

Data structures added:

* [SqlLogItem](/document/api/237/16191#SqlLogItem)

Data structure modified:

* [DBAccount](/document/api/237/16191#DBAccount)
	* New member: DelayThresh
* [DBInstance](/document/api/237/16191#DBInstance)
	* New members: UniqueVpcId, UniqueSubnetId, OriginSerialId, NodeCount, IsTmp, ExclusterId, Id, Qps, Paymode, Locker, and StatusDesc
* [Deal](/document/api/237/16191#Deal)
	* New members: Count and PayMode
	* **Deleted member:** Quantity
* [LogFileInfo](/document/api/237/16191#LogFileInfo)
	* **Modified member:** Uri
* [ParamConstraint](/document/api/237/16191#ParamConstraint)
	* New member: String
* [ParamModifyResult](/document/api/237/16191#ParamModifyResult)
	* **Modified member:** Code
* [SlowLogData](/document/api/237/16191#SlowLogData)
	* **Modified members:** LockTimeAvg, LockTimeMax, LockTimeMin, LockTimeSum, QueryCount, QueryTimeAvg, QueryTimeMax, QueryTimeMin, QueryTimeSum, RowsExaminedSum, and RowsSentSum

## The 1st Release

Release time: 2018-04-24

The following changes are contained in this release:

The existing documents were improved.

APIs added:

* [CloseDBExtranetAccess](/document/api/237/16179)
* [CopyAccountPrivileges](/document/api/237/16169)
* [CreateAccount](/document/api/237/16165)
* [CreateDBInstance](/document/api/237/16180)
* [DeleteAccount](/document/api/237/16171)
* [DescribeAccountPrivileges](/document/api/237/16164)
* [DescribeAccounts](/document/api/237/16167)
* [DescribeBackupTime](/document/api/237/16182)
* [DescribeDBInstanceSpecs](/document/api/237/16188)
* [DescribeDBInstances](/document/api/237/16184)
* [DescribeDBLogFiles](/document/api/237/16162)
* [DescribeDBParameters](/document/api/237/16154)
* [DescribeDBPerformance](/document/api/237/16160)
* [DescribeDBPerformanceDetails](/document/api/237/16156)
* [DescribeDBResourceUsage](/document/api/237/16158)
* [DescribeDBResourceUsageDetails](/document/api/237/16157)
* [DescribeDBSlowLogs](/document/api/237/16159)
* [DescribeFlow](/document/api/237/16177)
* [DescribeLogFileRetentionPeriod](/document/api/237/16152)
* [DescribeOrders](/document/api/237/16186)
* [DescribePrice](/document/api/237/16175)
* [DescribeRenewalPrice](/document/api/237/16181)
* [DescribeSaleInfo](/document/api/237/16178)
* [DescribeUpgradePrice](/document/api/237/16183)
* [GrantAccountPrivileges](/document/api/237/16166)
* [InitDBInstances](/document/api/237/16185)
* [ModifyAccountDescription](/document/api/237/16170)
* [ModifyBackupTime](/document/api/237/16173)
* [ModifyDBInstanceName](/document/api/237/16190)
* [ModifyDBInstancesProject](/document/api/237/16176)
* [ModifyDBParameters](/document/api/237/16153)
* [ModifyLogFileRetentionPeriod](/document/api/237/16151)
* [OpenDBExtranetAccess](/document/api/237/16174)
* [RenewDBInstance](/document/api/237/16187)
* [ResetAccountPassword](/document/api/237/16168)
* [UpgradeDBInstance](/document/api/237/16189)

Data structures added:

* [ConstraintRange](/document/api/237/16191#ConstraintRange)
* [DBAccount](/document/api/237/16191#DBAccount)
* [DBBackupTimeConfig](/document/api/237/16191#DBBackupTimeConfig)
* [DBInstance](/document/api/237/16191#DBInstance)
* [DBParamValue](/document/api/237/16191#DBParamValue)
* [Deal](/document/api/237/16191#Deal)
* [InstanceSpec](/document/api/237/16191#InstanceSpec)
* [LogFileInfo](/document/api/237/16191#LogFileInfo)
* [MonitorData](/document/api/237/16191#MonitorData)
* [MonitorIntData](/document/api/237/16191#MonitorIntData)
* [ParamConstraint](/document/api/237/16191#ParamConstraint)
* [ParamDesc](/document/api/237/16191#ParamDesc)
* [ParamModifyResult](/document/api/237/16191#ParamModifyResult)
* [PerformanceMonitorSet](/document/api/237/16191#PerformanceMonitorSet)
* [RegionInfo](/document/api/237/16191#RegionInfo)
* [ResourceUsageMonitorSet](/document/api/237/16191#ResourceUsageMonitorSet)
* [SlowLogData](/document/api/237/16191#SlowLogData)
* [SpecConfigInfo](/document/api/237/16191#SpecConfigInfo)
* [ZoneChooseInfo](/document/api/237/16191#ZoneChooseInfo)
* [ZonesInfo](/document/api/237/16191#ZonesInfo)


