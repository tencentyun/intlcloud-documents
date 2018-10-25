## Release 5
Release time: August 17, 2018 15:26:03

This release contains:

Improvement to existing documentation.

Modified data structure:

* [InstanceTypeConfig](/document/api/599/15912#InstanceTypeConfig)
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

* [DescribeCvmZoneInstanceConfigInfos](/document/api/599/18565)

New data structures:

* [Externals](/document/api/599/15912#Externals)
* [InstanceMarketOptionsRequest](/document/api/599/15912#InstanceMarketOptionsRequest)
* [InstanceTypeQuotaItem](/document/api/599/15912#InstanceTypeQuotaItem)
* [ItemPrice](/document/api/599/15912#ItemPrice)
* [LocalDiskType](/document/api/599/15912#LocalDiskType)
* [SpotMarketOptions](/document/api/599/15912#SpotMarketOptions)
* [StorageBlock](/document/api/599/15912#StorageBlock)

Modified data structure:

* [EnvData](/document/api/599/15912#EnvData)
	* New members: InstanceChargeType, InstanceMarketOptions

## Release 2

Release time: May 24, 2018 17:08:50

This release contains:

Improvement to existing documentation.

New APIs:

* [TerminateComputeNodes](/document/api/599/17372)

Modified APIs:

* [DescribeJob](/document/api/599/15904)
	* New output parameters: StateReason

Modified data structure:

* [ComputeNode](/document/api/599/15912#ComputeNode)
	* New members: PrivateIpAddresses, PublicIpAddresses
* [Job](/document/api/599/15912#Job)
	* New members: StateIfCreateCvmFailed
* [NamedComputeEnv](/document/api/599/15912#NamedComputeEnv)
	* New members: ActionIfComputeNodeInactive
* [TaskInstanceView](/document/api/599/15912#TaskInstanceView)
	* New members: StateDetailedReason

## Release 1

Release time: April 24, 2018

This release contains:

Improvement to existing documentation.

New APIs:

* [CreateComputeEnv](/document/api/599/15891)
* [CreateTaskTemplate](/document/api/599/15899)
* [DeleteComputeEnv](/document/api/599/15889)
* [DeleteJob](/document/api/599/15906)
* [DeleteTaskTemplates](/document/api/599/15900)
* [DescribeAvailableCvmInstanceTypes](/document/api/599/15887)
* [DescribeComputeEnv](/document/api/599/15892)
* [DescribeComputeEnvActivities](/document/api/599/15896)
* [DescribeComputeEnvCreateInfo](/document/api/599/15897)
* [DescribeComputeEnvCreateInfos](/document/api/599/15894)
* [DescribeComputeEnvs](/document/api/599/15893)
* [DescribeJob](/document/api/599/15904)
* [DescribeJobSubmitInfo](/document/api/599/15910)
* [DescribeJobs](/document/api/599/15909)
* [DescribeTask](/document/api/599/15905)
* [DescribeTaskTemplates](/document/api/599/15902)
* [ModifyComputeEnv](/document/api/599/15890)
* [ModifyTaskTemplate](/document/api/599/15901)
* [SubmitJob](/document/api/599/15907)
* [TerminateComputeNode](/document/api/599/15895)
* [TerminateJob](/document/api/599/15911)
* [TerminateTaskInstance](/document/api/599/15908)

New data structures:

* [Activity](/document/api/599/15912#Activity)
* [AgentRunningMode](/document/api/599/15912#AgentRunningMode)
* [AnonymousComputeEnv](/document/api/599/15912#AnonymousComputeEnv)
* [Application](/document/api/599/15912#Application)
* [Authentication](/document/api/599/15912#Authentication)
* [ComputeEnvCreateInfo](/document/api/599/15912#ComputeEnvCreateInfo)
* [ComputeEnvView](/document/api/599/15912#ComputeEnvView)
* [ComputeNode](/document/api/599/15912#ComputeNode)
* [ComputeNodeMetrics](/document/api/599/15912#ComputeNodeMetrics)
* [DataDisk](/document/api/599/15912#DataDisk)
* [Dependency](/document/api/599/15912#Dependence)
* [Docker](/document/api/599/15912#Docker)
* [EnhancedService](/document/api/599/15912#EnhancedService)
* [EnvData](/document/api/599/15912#EnvData)
* [EnvVar](/document/api/599/15912#EnvVar)
* [EventConfig](/document/api/599/15912#EventConfig)
* [EventVar](/document/api/599/15912#EventVar)
* [Filter](/document/api/599/15912#Filter)
* [InputMapping](/document/api/599/15912#InputMapping)
* [InstanceTypeConfig](/document/api/599/15912#InstanceTypeConfig)
* [InternetAccessible](/document/api/599/15912#InternetAccessible)
* [Job](/document/api/599/15912#Job)
* [JobView](/document/api/599/15912#JobView)
* [LoginSettings](/document/api/599/15912#LoginSettings)
* [MountDataDisk](/document/api/599/15912#MountDataDisk)
* [NamedComputeEnv](/document/api/599/15912#NamedComputeEnv)
* [Notification](/document/api/599/15912#Notification)
* [OutputMapping](/document/api/599/15912#OutputMapping)
* [OutputMappingConfig](/document/api/599/15912#OutputMappingConfig)
* [Placement](/document/api/599/15912#Placement)
* [RedirectInfo](/document/api/599/15912#RedirectInfo)
* [RedirectLocalInfo](/document/api/599/15912#RedirectLocalInfo)
* [RunMonitorServiceEnabled](/document/api/599/15912#RunMonitorServiceEnabled)
* [RunSecurityServiceEnabled](/document/api/599/15912#RunSecurityServiceEnabled)
* [SystemDisk](/document/api/599/15912#SystemDisk)
* [Task](/document/api/599/15912#Task)
* [TaskInstanceMetrics](/document/api/599/15912#TaskInstanceMetrics)
* [TaskInstanceView](/document/api/599/15912#TaskInstanceView)
* [TaskMetrics](/document/api/599/15912#TaskMetrics)
* [TaskTemplateView](/document/api/599/15912#TaskTemplateView)
* [TaskView](/document/api/599/15912#TaskView)
* [VirtualPrivateCloud](/document/api/599/15912#VirtualPrivateCloud)


