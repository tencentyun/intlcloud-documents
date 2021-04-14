## Release 5

Release time: August 17, 2018 15:26:03

This release contains:

Improvement to existing documentation.

Modified data structure:

* [InstanceTypeConfig](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#InstanceTypeConfig)
	* New members: Mem, Cpu
	* **Deleted members:** GPU, CPU, Memory, CbsSupport, InstanceTypeState
	* **Modified members:** InstanceType, Zone, InstanceFamily

## Release 4

Release time: August 2, 2018 15:48:13

This release contains:

Improvement to existing documentation.

## Release 3

Release time: July 26, 2018 15:15:22

This release contains:

Improvement to existing documentation.

New APIs:

* [DescribeCvmZoneInstanceConfigInfos](https://cloud.tencent.com/document/api/599/30543)

New data structures:

* [Externals](https://cloud.tencent.com/document/api/599/30482#Externals)
* [InstanceMarketOptionsRequest](https://cloud.tencent.com/document/api/599/30482#InstanceMarketOptionsRequest)
* [InstanceTypeQuotaItem](https://cloud.tencent.com/document/api/599/30482#InstanceTypeQuotaItem)
* [ItemPrice](https://cloud.tencent.com/document/api/599/30482#ItemPrice)
* [LocalDiskType](https://cloud.tencent.com/document/api/599/30482#LocalDiskType)
* [SpotMarketOptions](https://cloud.tencent.com/document/api/599/30482#SpotMarketOptions)
* [StorageBlock](https://cloud.tencent.com/document/api/599/30482#StorageBlock)

Modified data structure:

* [EnvData](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#EnvData)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 2

Release time: May 24, 2018 17:08:50

This release contains:

Improvement to existing documentation.

New APIs:

* [TerminateComputeNodes](https://cloud.tencent.com/document/api/599/30485)

Modified APIs:

* [DescribeJob](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30561)
	* New output parameters: StateReason

Modified data structure:

* [ComputeNode](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#ComputeNode)
	* New members: PrivateIpAddresses, PublicIpAddresses
* [Job](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#Job)
	* New members: StateIfCreateCvmFailed
* [NamedComputeEnv](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#NamedComputeEnv)
	* New members: ActionIfComputeNodeInactive
* [TaskInstanceView](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskInstanceView)
	* New members: StateDetailedReason

## Release 1

Release time: April 24, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateComputeEnv](https://cloud.tencent.com/document/api/599/30521)
* [CreateTaskTemplate](https://cloud.tencent.com/document/api/599/30569)
* [DeleteComputeEnv](https://cloud.tencent.com/document/api/599/30519)
* [DeleteJob](https://cloud.tencent.com/document/api/599/30563)
* [DeleteTaskTemplates](https://cloud.tencent.com/document/api/599/30567)
* [DescribeAvailableCvmInstanceTypes](https://cloud.tencent.com/document/api/599/30545)
* [DescribeComputeEnv](https://cloud.tencent.com/document/api/599/30517)
* [DescribeComputeEnvActivities](https://cloud.tencent.com/document/api/599/30515)
* [DescribeComputeEnvCreateInfo](https://cloud.tencent.com/document/api/599/30513)
* [DescribeComputeEnvCreateInfos](https://cloud.tencent.com/document/api/599/30511)
* [DescribeComputeEnvs](https://cloud.tencent.com/document/api/599/30509)
* [DescribeJob](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30561)
* [DescribeJobSubmitInfo](https://cloud.tencent.com/document/api/599/30559)
* [DescribeJobs](https://cloud.tencent.com/document/api/599/30557)
* [DescribeTask](https://cloud.tencent.com/document/api/599/30555)
* [DescribeTaskTemplates](https://cloud.tencent.com/document/api/599/30565)
* [ModifyComputeEnv](https://cloud.tencent.com/document/api/599/30507)
* [ModifyTaskTemplate](https://cloud.tencent.com/document/api/599/30491)
* [SubmitJob](https://cloud.tencent.com/document/api/599/30549)
* [TerminateComputeNode](https://cloud.tencent.com/document/api/599/30505)
* [TerminateJob](https://cloud.tencent.com/document/api/599/15911)
* [TerminateTaskInstance](https://cloud.tencent.com/document/api/599/30489)

New data structures:

* [Activity](https://cloud.tencent.com/document/api/599/30482#Activity)
* [AgentRunningMode](https://cloud.tencent.com/document/api/599/30482#AgentRunningMode)
* [AnonymousComputeEnv](https://cloud.tencent.com/document/api/599/30482#AnonymousComputeEnv)
* [Application](https://cloud.tencent.com/document/api/599/30482#Application)
* [Authentication](https://cloud.tencent.com/document/api/599/30482#Authentication)
* [ComputeEnvCreateInfo](https://cloud.tencent.com/document/api/599/30482#ComputeEnvCreateInfo)
* [ComputeEnvView](https://cloud.tencent.com/document/api/599/30482#ComputeEnvView)
* [ComputeNode](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#ComputeNode)
* [ComputeNodeMetrics](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#ComputeNodeMetrics)
* [DataDisk](https://cloud.tencent.com/document/api/599/30482#DataDisk)
* [Dependency](https://cloud.tencent.com/document/api/599/30482#Dependence)
* [Docker](https://cloud.tencent.com/document/api/599/30482#Docker)
* [EnhancedService](https://cloud.tencent.com/document/api/599/30482#EnhancedService)
* [EnvData](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#EnvData)
* [EnvVar](https://cloud.tencent.com/document/api/599/30482#EnvVar)
* [EventConfig](https://cloud.tencent.com/document/api/599/30482#EventConfig)
* [EventVar](https://cloud.tencent.com/document/api/599/30482#EventVar)
* [Filter](https://cloud.tencent.com/document/api/599/30482#Filter)
* [InputMapping](https://cloud.tencent.com/document/api/599/30482#InputMapping)
* [InstanceTypeConfig](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#InstanceTypeConfig)
* [InternetAccessible](https://cloud.tencent.com/document/api/599/30482#InternetAccessible)
* [Job](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#Job)
* [JobView](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#JobView)
* [LoginSettings](https://cloud.tencent.com/document/api/599/30482#LoginSettings)
* [MountDataDisk](https://cloud.tencent.com/document/api/599/30482#MountDataDisk)
* [NamedComputeEnv](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#NamedComputeEnv)
* [Notification](https://cloud.tencent.com/document/api/599/30482#Notification)
* [OutputMapping](https://cloud.tencent.com/document/api/599/30482#OutputMapping)
* [OutputMappingConfig](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#OutputMappingConfig)
* [Placement](https://cloud.tencent.com/document/api/599/30482#Placement)
* [RedirectInfo](https://cloud.tencent.com/document/api/599/30482#RedirectInfo)
* [RedirectLocalInfo](https://cloud.tencent.com/document/api/599/30482#RedirectLocalInfo)
* [RunMonitorServiceEnabled](https://cloud.tencent.com/document/api/599/30482#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](https://cloud.tencent.com/document/api/599/30482#RunSecurityServiceEnabled)
* [SystemDisk](https://cloud.tencent.com/document/api/599/30482#SystemDisk)
* [Task](https://cloud.tencent.com/document/api/599/30482#Task)
* [TaskInstanceMetrics](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskInstanceMetrics)
* [TaskInstanceView](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskInstanceView)
* [TaskMetrics](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskMetrics)
* [TaskTemplateView](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskTemplateView)
* [TaskView](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/599/30482#TaskView)
* [VirtualPrivateCloud](https://cloud.tencent.com/document/api/599/30482#VirtualPrivateCloud)


