## Release 5

Release time: April 25, 2019 19:15:25

This release contains:

Improvement to existing documentation.

New APIs:

* [CleanUpInstance](/document/api/239/34442)
* [DescribeBackupUrl](/document/api/239/34443)
* [DescribeInstanceParamRecords](/document/api/239/34449)
* [DescribeInstanceParams](/document/api/239/34448)
* [DescribeInstanceSecurityGroup](/document/api/239/34447)
* [DescribeInstanceShards](/document/api/239/34441)
* [DescribeProjectSecurityGroup](/document/api/239/34446)
* [DestroyPostpaidInstance](/document/api/239/34440)
* [DestroyPrepaidInstance](/document/api/239/34439)
* [DisableReplicaReadonly](/document/api/239/34438)
* [EnableReplicaReadonly](/document/api/239/34437)
* [ModifyInstanceParams](/document/api/239/34445)
* [ModifyNetworkConfig](/document/api/239/34436)
* [RestoreInstance](/document/api/239/34435)

Modified APIs:

* [CreateInstances](/document/api/239/20026)
	* New input parameters: InstanceName
* [DescribeInstanceBackups](/document/api/239/20011)
	* **Modified input parameters:** Status
* [DescribeInstances](/document/api/239/20018)
	* New input parameters: Status, TypeVersion, EngineName, AutoRenew, BillingMode, Type, SearchKeys
* [ModifyInstance](/document/api/239/31785)
	* New input parameters: ProjectId, AutoRenew
	
New data structures:

* [InstanceClusterNode](/document/api/239/20022#InstanceClusterNode)
* [InstanceClusterShard](/document/api/239/20022#InstanceClusterShard)
* [InstanceEnumParam](/document/api/239/20022#InstanceEnumParam)
* [InstanceIntegerParam](/document/api/239/20022#InstanceIntegerParam)
* [InstanceNode](/document/api/239/20022#InstanceNode)
* [InstanceParam](/document/api/239/20022#InstanceParam)
* [InstanceParamHistory](/document/api/239/20022#InstanceParamHistory)
* [InstanceSecurityGroupDetail](/document/api/239/20022#InstanceSecurityGroupDetail)
* [InstanceTagInfo](/document/api/239/20022#InstanceTagInfo)
* [InstanceTextParam](/document/api/239/20022#InstanceTextParam)
* [SecurityGroupDetail](/document/api/239/20022#SecurityGroupDetail)
* [SecurityGroupsInboundAndOutbound](/document/api/239/20022#SecurityGroupsInboundAndOutbound)

Modified data structures:

* [InstanceSet](/document/api/239/20022#InstanceSet)
	* New members: InstanceTitle, OfflineTime, SubStatus, Tags, InstanceNode, RedisShardSize, RedisShardNum, RedisReplicasNum, PriceId, CloseTime, SlaveReadWeight, InstanceTags, ProjectName

## Release 4

Release time: December 20, 2018 19:18:40

This release contains:

Improvement to existing documentation.

New APIs:

* [ModifyInstance](/document/api/239/31785)

## Release 3

Release time: November 29, 2018 15:50:12

This release contains:

Improvement to existing documentation.

Modified APIs:

* [CreateInstances](/document/api/239/20026)
	* New input parameters: RedisShardNum, RedisReplicasNum, ReplicasReadonly
* [DescribeInstances](/document/api/239/20018)
	* New input parameters: UniqVpcIds, UniqSubnetIds
* [UpgradeInstance](/document/api/239/20013)
	* New input parameters: RedisShardNum, RedisReplicasNum

## Release 2

Release time: November 22, 2018 19:23:49

This release contains:

Improvement to existing documentation.

New APIs:

* [DescribeInstanceDealDetail](/document/api/239/30602)
* [DescribeProductInfo](/document/api/239/30600)
* [DescribeTaskInfo](/document/api/239/30601)

New data structures:

* [ProductConf](/document/api/239/20022#ProductConf)
* [RegionConf](/document/api/239/20022#RegionConf)
* [TradeDealDetail](/document/api/239/20022#TradeDealDetail)
* [ZoneCapacityConf](/document/api/239/20022#ZoneCapacityConf)

Modified data structures:

* [InstanceSet](/document/api/239/20022#InstanceSet)
	* New members: Engine, ProductType, UniqVpcId, UniqSubnetId, BillingMode

## Release 1

Release time: September 21, 2018 11:22:59

This release contains:

Improvement to existing documentation.

New APIs:

* [ClearInstance](/document/api/239/20021)
* [CreateInstances](/document/api/239/20026)
* [DescribeAutoBackupConfig](/document/api/239/20019)
* [DescribeInstanceBackups](/document/api/239/20011)
* [DescribeInstances](/document/api/239/20018)
* [ManualBackupInstance](/document/api/239/20010)
* [ModfiyInstancePassword](/document/api/239/20025)
* [ModifyAutoBackupConfig](/document/api/239/20016)
* [RenewInstance](/document/api/239/20015)
* [ResetPassword](/document/api/239/20014)
* [UpgradeInstance](/document/api/239/20013)

New data structures:

* [InstanceSet](/document/api/239/20022#InstanceSet)
* [RedisBackupSet](/document/api/239/20022#RedisBackupSet)
