## Release 5

Release time: August 17, 2018 15:26:03

This release contains:

Improvement to existing documentation.

Modified data structure:

* [InstanceTypeConfig](/document/api/599/30482#InstanceTypeConfig)
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

* [DescribeCvmZoneInstanceConfigInfos](/document/api/599/30543)

New data structures:

* [Externals](/document/api/599/30482#Externals)
* [InstanceMarketOptionsRequest](/document/api/599/30482#InstanceMarketOptionsRequest)
* [InstanceTypeQuotaItem](/document/api/599/30482#InstanceTypeQuotaItem)
* [ItemPrice](/document/api/599/30482#ItemPrice)
* [LocalDiskType](/document/api/599/30482#LocalDiskType)
* [SpotMarketOptions](/document/api/599/30482#SpotMarketOptions)
* [StorageBlock](/document/api/599/30482#StorageBlock)

Modified data structure:

* [EnvData](/document/api/599/30482#EnvData)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 2

Release time: May 24, 2018 17:08:50

This release contains:

Improvement to existing documentation.

New APIs:

* [TerminateComputeNodes](/document/api/599/30485)

Modified APIs:

* [DescribeJob](/document/api/599/30561)
	* New output parameters: StateReason

Modified data structure:

* [ComputeNode](/document/api/599/30482#ComputeNode)
	* New members: PrivateIpAddresses, PublicIpAddresses
* [Job](/document/api/599/30482#Job)
	* New members: StateIfCreateCvmFailed
* [NamedComputeEnv](/document/api/599/30482#NamedComputeEnv)
	* New members: ActionIfComputeNodeInactive
* [TaskInstanceView](/document/api/599/30482#TaskInstanceView)
	* New members: StateDetailedReason

## Release 1

Release time: April 24, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateComputeEnv](/document/api/599/30521)
* [CreateTaskTemplate](/document/api/599/30569)
* [DeleteComputeEnv](/document/api/599/30519)
* [DeleteJob](/document/api/599/30563)
* [DeleteTaskTemplates](/document/api/599/30567)
* [DescribeAvailableCvmInstanceTypes](/document/api/599/30545)
* [DescribeComputeEnv](/document/api/599/30517)
* [DescribeComputeEnvActivities](/document/api/599/30515)
* [DescribeComputeEnvCreateInfo](/document/api/599/30513)
* [DescribeComputeEnvCreateInfos](/document/api/599/30511)
* [DescribeComputeEnvs](/document/api/599/30509)
* [DescribeJob](/document/api/599/30561)
* [DescribeJobSubmitInfo](/document/api/599/30559)
* [DescribeJobs](/document/api/599/30557)
* [DescribeTask](/document/api/599/30555)
* [DescribeTaskTemplates](/document/api/599/30565)
* [ModifyComputeEnv](/document/api/599/30507)
* [ModifyTaskTemplate](/document/api/599/30491)
* [SubmitJob](/document/api/599/30549)
* [TerminateComputeNode](/document/api/599/30505)
* [TerminateJob](/document/api/599/15911)
* [TerminateTaskInstance](/document/api/599/30489)

New data structures:

* [Activity](/document/api/599/30482#Activity)
* [AgentRunningMode](/document/api/599/30482#AgentRunningMode)
* [AnonymousComputeEnv](/document/api/599/30482#AnonymousComputeEnv)
* [Application](/document/api/599/30482#Application)
* [Authentication](/document/api/599/30482#Authentication)
* [ComputeEnvCreateInfo](/document/api/599/30482#ComputeEnvCreateInfo)
* [ComputeEnvView](/document/api/599/30482#ComputeEnvView)
* [ComputeNode](/document/api/599/30482#ComputeNode)
* [ComputeNodeMetrics](/document/api/599/30482#ComputeNodeMetrics)
* [DataDisk](/document/api/599/30482#DataDisk)
* [Dependency](/document/api/599/30482#Dependence)
* [Docker](/document/api/599/30482#Docker)
* [EnhancedService](/document/api/599/30482#EnhancedService)
* [EnvData](/document/api/599/30482#EnvData)
* [EnvVar](/document/api/599/30482#EnvVar)
* [EventConfig](/document/api/599/30482#EventConfig)
* [EventVar](/document/api/599/30482#EventVar)
* [Filter](/document/api/599/30482#Filter)
* [InputMapping](/document/api/599/30482#InputMapping)
* [InstanceTypeConfig](/document/api/599/30482#InstanceTypeConfig)
* [InternetAccessible](/document/api/599/30482#InternetAccessible)
* [Job](/document/api/599/30482#Job)
* [JobView](/document/api/599/30482#JobView)
* [LoginSettings](/document/api/599/30482#LoginSettings)
* [MountDataDisk](/document/api/599/30482#MountDataDisk)
* [NamedComputeEnv](/document/api/599/30482#NamedComputeEnv)
* [Notification](/document/api/599/30482#Notification)
* [OutputMapping](/document/api/599/30482#OutputMapping)
* [OutputMappingConfig](/document/api/599/30482#OutputMappingConfig)
* [Placement](/document/api/599/30482#Placement)
* [RedirectInfo](/document/api/599/30482#RedirectInfo)
* [RedirectLocalInfo](/document/api/599/30482#RedirectLocalInfo)
* [RunMonitorServiceEnabled](/document/api/599/30482#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](/document/api/599/30482#RunSecurityServiceEnabled)
* [SystemDisk](/document/api/599/30482#SystemDisk)
* [Task](/document/api/599/30482#Task)
* [TaskInstanceMetrics](/document/api/599/30482#TaskInstanceMetrics)
* [TaskInstanceView](/document/api/599/30482#TaskInstanceView)
* [TaskMetrics](/document/api/599/30482#TaskMetrics)
* [TaskTemplateView](/document/api/599/30482#TaskTemplateView)
* [TaskView](/document/api/599/30482#TaskView)
* [VirtualPrivateCloud](/document/api/599/30482#VirtualPrivateCloud)


