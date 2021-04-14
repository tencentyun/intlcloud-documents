## Release 4

Release time: May 30, 2019 20:41:02

This release contains:

Improvements on existing documentation.

Modified APIs:

* [CreateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30633)
	* New input parameters: DeployMode, MultiZoneInfo, LicenseType

New data structures:

* [MultiZoneInfo](https://cloud.tencent.com/document/api/845/30634#MultiZoneInfo)
* [TagInfo](https://cloud.tencent.com/document/api/845/30634#TagInfo)

Modified data structures:

* [InstanceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#InstanceInfo)
	* New members: TagList, LicenseType

## Release 3

Release time: March 14, 2019 16:33:24

This release contains:

Improvements on existing documentation.

New APIs:

* [DescribeInstanceLogs](https://cloud.tencent.com/document/api/845/33760)
* [DescribeInstanceOperations](https://cloud.tencent.com/document/api/845/33759)

Modified APIs:

* [CreateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30633)
	* New input parameters: ClusterNameInConf
* [UpdateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30629)
	* New input parameters: CosBackup

New data structures:

* [InstanceLog](https://cloud.tencent.com/document/api/845/30634#InstanceLog)
* [KeyValue](https://cloud.tencent.com/document/api/845/30634#KeyValue)
* [Operation](https://cloud.tencent.com/document/api/845/30634#Operation)
* [OperationDetail](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#OperationDetail)
* [SubTaskDetail](https://cloud.tencent.com/document/api/845/30634#SubTaskDetail)
* [TaskDetail](https://cloud.tencent.com/document/api/845/30634#TaskDetail)

## Release 2

Release time: March 7, 2019 21:24:06

This release contains:

Improvements on existing documentation.

Modified APIs:

* [CreateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30633)
	* New input parameters: EnableDedicatedMaster, MasterNodeNum, MasterNodeType, MasterNodeDiskSize
* [RestartInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30630)
	* New input parameters: ForceRestart
* [UpdateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30629)
	* New input parameters: MasterNodeNum, MasterNodeType, MasterNodeDiskSize, ForceRestart

New data structures:

* [CosBackup](https://cloud.tencent.com/document/api/845/30634#CosBackup)

Modified data structures:

* [InstanceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#InstanceInfo)
	* New members: CosBackup, AllowCosBackup
* [MasterNodeInfo](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#MasterNodeInfo)
	* New members: MasterNodeDiskType

## Release 1

Release time: November 22, 2018 20:16:54

This release contains:

Improvements on existing documentation.

New APIs:

* [CreateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30633)
* [DeleteInstance](https://cloud.tencent.com/document/api/845/30632)
* [DescribeInstances](https://cloud.tencent.com/document/api/845/30631)
* [RestartInstance](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30630)
* [UpdateInstance](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30629)

New data structures:

* [DictInfo](https://cloud.tencent.com/document/api/845/30634#DictInfo)
* [EsAcl](https://cloud.tencent.com/document/api/845/30634#EsAcl)
* [EsDictionaryInfo](https://cloud.tencent.com/document/api/845/30634#EsDictionaryInfo)
* [InstanceInfo](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#InstanceInfo)
* [MasterNodeInfo](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/845/30634#MasterNodeInfo)

