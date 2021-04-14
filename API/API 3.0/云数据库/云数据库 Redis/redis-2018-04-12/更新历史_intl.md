## Release 5

Release time: April 25, 2019 19:15:25

This release contains:

Improvement to existing documentation.

New APIs:

* [CleanUpInstance](https://cloud.tencent.com/document/api/239/34442)
* [DescribeBackupUrl](https://cloud.tencent.com/document/api/239/34443)
* [DescribeInstanceParamRecords](https://cloud.tencent.com/document/api/239/34449)
* [DescribeInstanceParams](https://cloud.tencent.com/document/api/239/34448)
* [DescribeInstanceSecurityGroup](https://cloud.tencent.com/document/api/239/34447)
* [DescribeInstanceShards](https://cloud.tencent.com/document/api/239/34441)
* [DescribeProjectSecurityGroup](https://cloud.tencent.com/document/api/239/34446)
* [DestroyPostpaidInstance](https://cloud.tencent.com/document/api/239/34440)
* [DestroyPrepaidInstance](https://cloud.tencent.com/document/api/239/34439)
* [DisableReplicaReadonly](https://cloud.tencent.com/document/api/239/34438)
* [EnableReplicaReadonly](https://cloud.tencent.com/document/api/239/34437)
* [ModifyInstanceParams](https://cloud.tencent.com/document/api/239/34445)
* [ModifyNetworkConfig](https://cloud.tencent.com/document/api/239/34436)
* [RestoreInstance](https://cloud.tencent.com/document/api/239/34435)

Modified APIs:

* [CreateInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20026)
	* New input parameters: InstanceName
* [DescribeInstanceBackups](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20011)
	* **Modified input parameters:** Status
* [DescribeInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20018)
	* New input parameters: Status, TypeVersion, EngineName, AutoRenew, BillingMode, Type, SearchKeys
* [ModifyInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/31785)
	* New input parameters: ProjectId, AutoRenew
	
New data structures:

* [InstanceClusterNode](https://cloud.tencent.com/document/api/239/20022#InstanceClusterNode)
* [InstanceClusterShard](https://cloud.tencent.com/document/api/239/20022#InstanceClusterShard)
* [InstanceEnumParam](https://cloud.tencent.com/document/api/239/20022#InstanceEnumParam)
* [InstanceIntegerParam](https://cloud.tencent.com/document/api/239/20022#InstanceIntegerParam)
* [InstanceNode](https://cloud.tencent.com/document/api/239/20022#InstanceNode)
* [InstanceParam](https://cloud.tencent.com/document/api/239/20022#InstanceParam)
* [InstanceParamHistory](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceParamHistory)
* [InstanceSecurityGroupDetail](https://cloud.tencent.com/document/api/239/20022#InstanceSecurityGroupDetail)
* [InstanceTagInfo](https://cloud.tencent.com/document/api/239/20022#InstanceTagInfo)
* [InstanceTextParam](https://cloud.tencent.com/document/api/239/20022#InstanceTextParam)
* [SecurityGroupDetail](https://cloud.tencent.com/document/api/239/20022#SecurityGroupDetail)
* [SecurityGroupsInboundAndOutbound](https://cloud.tencent.com/document/api/239/20022#SecurityGroupsInboundAndOutbound)

Modified data structures:

* [InstanceSet](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceSet)
	* New members: InstanceTitle, OfflineTime, SubStatus, Tags, InstanceNode, RedisShardSize, RedisShardNum, RedisReplicasNum, PriceId, CloseTime, SlaveReadWeight, InstanceTags, ProjectName

## Release 4

Release time: December 20, 2018 19:18:40

This release contains:

Improvement to existing documentation.

New APIs:

* [ModifyInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/31785)

## Release 3

Release time: November 29, 2018 15:50:12

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20026)
	* New input parameters: RedisShardNum, RedisReplicasNum, ReplicasReadonly
* [DescribeInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20018)
	* New input parameters: UniqVpcIds, UniqSubnetIds
* [UpgradeInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20013)
	* New input parameters: RedisShardNum, RedisReplicasNum

## Release 2

Release time: November 22, 2018 19:23:49

This release contains:

Improvement to existing documentation.

New APIs:

* [DescribeInstanceDealDetail](https://cloud.tencent.com/document/api/239/30602)
* [DescribeProductInfo](https://cloud.tencent.com/document/api/239/30600)
* [DescribeTaskInfo](https://cloud.tencent.com/document/api/239/30601)

New data structures:

* [ProductConf](https://cloud.tencent.com/document/api/239/20022#ProductConf)
* [RegionConf](https://cloud.tencent.com/document/api/239/20022#RegionConf)
* [TradeDealDetail](https://cloud.tencent.com/document/api/239/20022#TradeDealDetail)
* [ZoneCapacityConf](https://cloud.tencent.com/document/api/239/20022#ZoneCapacityConf)

Modified data structures:

* [InstanceSet](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceSet)
	* New members: Engine, ProductType, UniqVpcId, UniqSubnetId, BillingMode

## Release 1

Release time: September 21, 2018 11:22:59

This release contains:

Improvement to existing documentation.

New APIs:

* [ClearInstance](https://cloud.tencent.com/document/api/239/20021)
* [CreateInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20026)
* [DescribeAutoBackupConfig](https://cloud.tencent.com/document/api/239/20019)
* [DescribeInstanceBackups](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20011)
* [DescribeInstances](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20018)
* [ManualBackupInstance](https://cloud.tencent.com/document/api/239/20010)
* [ModfiyInstancePassword](https://cloud.tencent.com/document/api/239/20025)
* [ModifyAutoBackupConfig](https://cloud.tencent.com/document/api/239/20016)
* [RenewInstance](https://cloud.tencent.com/document/api/239/20015)
* [ResetPassword](https://cloud.tencent.com/document/api/239/20014)
* [UpgradeInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20013)

New data structures:

* [InstanceSet](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/239/20022#InstanceSet)
* [RedisBackupSet](https://cloud.tencent.com/document/api/239/20022#RedisBackupSet)
