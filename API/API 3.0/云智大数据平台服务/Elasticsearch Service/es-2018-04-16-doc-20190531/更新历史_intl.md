## Release 4

Release time: May 30, 2019 20:41:02

This release contains:

Improvements on existing documentation.

Modified APIs:

* [CreateInstance](/document/api/845/30633)
	* New input parameters: DeployMode, MultiZoneInfo, LicenseType

New data structures:

* [MultiZoneInfo](/document/api/845/30634#MultiZoneInfo)
* [TagInfo](/document/api/845/30634#TagInfo)

Modified data structures:

* [InstanceInfo](/document/api/845/30634#InstanceInfo)
	* New members: TagList, LicenseType

## Release 3

Release time: March 14, 2019 16:33:24

This release contains:

Improvements on existing documentation.

New APIs:

* [DescribeInstanceLogs](/document/api/845/33760)
* [DescribeInstanceOperations](/document/api/845/33759)

Modified APIs:

* [CreateInstance](/document/api/845/30633)
	* New input parameters: ClusterNameInConf
* [UpdateInstance](/document/api/845/30629)
	* New input parameters: CosBackup

New data structures:

* [InstanceLog](/document/api/845/30634#InstanceLog)
* [KeyValue](/document/api/845/30634#KeyValue)
* [Operation](/document/api/845/30634#Operation)
* [OperationDetail](/document/api/845/30634#OperationDetail)
* [SubTaskDetail](/document/api/845/30634#SubTaskDetail)
* [TaskDetail](/document/api/845/30634#TaskDetail)

## Release 2

Release time: March 7, 2019 21:24:06

This release contains:

Improvements on existing documentation.

Modified APIs:

* [CreateInstance](/document/api/845/30633)
	* New input parameters: EnableDedicatedMaster, MasterNodeNum, MasterNodeType, MasterNodeDiskSize
* [RestartInstance](/document/api/845/30630)
	* New input parameters: ForceRestart
* [UpdateInstance](/document/api/845/30629)
	* New input parameters: MasterNodeNum, MasterNodeType, MasterNodeDiskSize, ForceRestart

New data structures:

* [CosBackup](/document/api/845/30634#CosBackup)

Modified data structures:

* [InstanceInfo](/document/api/845/30634#InstanceInfo)
	* New members: CosBackup, AllowCosBackup
* [MasterNodeInfo](/document/api/845/30634#MasterNodeInfo)
	* New members: MasterNodeDiskType

## Release 1

Release time: November 22, 2018 20:16:54

This release contains:

Improvements on existing documentation.

New APIs:

* [CreateInstance](/document/api/845/30633)
* [DeleteInstance](/document/api/845/30632)
* [DescribeInstances](/document/api/845/30631)
* [RestartInstance](/document/api/845/30630)
* [UpdateInstance](/document/api/845/30629)

New data structures:

* [DictInfo](/document/api/845/30634#DictInfo)
* [EsAcl](/document/api/845/30634#EsAcl)
* [EsDictionaryInfo](/document/api/845/30634#EsDictionaryInfo)
* [InstanceInfo](/document/api/845/30634#InstanceInfo)
* [MasterNodeInfo](/document/api/845/30634#MasterNodeInfo)

