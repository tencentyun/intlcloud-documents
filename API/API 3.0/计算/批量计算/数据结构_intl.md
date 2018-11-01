## Activity
Compute environment creation or termination activities

Referenced by: DescribeComputeEnvActivities.

| Name | Type | Description |
|------|------|-------|
| ActivityId | String | Activity ID |
| ComputeNodeId | String | Compute node ID |
| ComputeNodeActivityType | String | Compute node activity type: creation or termination |
| EnvId | String | Compute environment ID |
| Cause | String | Cause |
| ActivityState | String | Activity state |
| StateReason | String | State reason |
| StartTime | String | Activity start time |
| EndTime | String | Activity end time |

## AgentRunningMode

Agent running mode

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Scene | String | Yes | Scenario type; Windows is supported |
| User | String | Yes | The user that runs Agent |
| Session | String | Yes | The session that runs Agent |

## AnonymousComputeEnv

Compute environment

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| EnvType | String | Yes | Compute environment management type |
| EnvData | [EnvData](#EnvData) | Yes | Compute environment's specific parameters |
| MountDataDisks | Array of [MountDataDisk](#MountDataDisk) | No | Data disk mounting option |
| AgentRunningMode | [AgentRunningMode](#AgentRunningMode) | No | Agent running mode; applicable for Windows OS |

## Application

Application information

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Command | String | Yes | Task execution command |
| DeliveryForm | String | Yes | The delivery method of the application, including two values: PACKAGE and LOCAL, which refer to the remotely stored software package and the local compute environment respectively. |
| PackagePath | String | No | Remote storage path of the application package |
| Docker | [Docker](#Docker) | No | The related configuration of the Docker used by the application. In case the Docker configuration is used, DeliveryForm of LOCAL means that the application software inside the Docker image is used directly and run in Docker mode; DeliveryForm of PACKAGE means that the remote application package is run in Docker mode after being injected into the Docker image. To avoid compatibility issues with different versions of Docker, the Docker installation package and related dependencies are taken care of by Batch. For custom images that have Docker installed, please uninstall it first and then use the Docker feature. |

## Authentication

Authentication information

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Scene | String | Yes | Authentication scenario such as COS |
| SecretId | String | Yes | SecretId |
| SecretKey | String | Yes | SecretKey |

## ComputeEnvCreateInfo

Compute environment creation information

Referenced by: DescribeComputeEnvCreateInfos.

| Name | Type | Description |
|------|------|-------|
| EnvId | String | Compute environment ID |
| EnvName | String | Compute environment name |
| EnvDescription | String | Compute environment description |
| EnvType | String | Compute environment type; only "MANAGED" type is supported |
| EnvData | [EnvData](#EnvData) | Compute environment parameters |
| MountDataDisks | Array of [MountDataDisk](#MountDataDisk) | Data disk mounting option |
| InputMappings | Array of [InputMapping](#InputMapping) | Input mapping |
| Authentications | Array of [Authentication](#Authentication) | Authentication information |
| Notifications | Array of [Notification](#Notification) | Notification information |
| DesiredComputeNodeCount | Integer | Number of desired compute nodes |

## ComputeEnvView

Compute environment information

Referenced by: DescribeComputeEnvs.

| Name | Type | Description |
|------|------|-------|
| EnvId | String | Compute environment ID |
| EnvName | String | Compute environment name |
| Placement | [Placement](#Placement) | Location information|
| CreateTime | String | Created time |
| ComputeNodeMetrics | [ComputeNodeMetrics](#ComputeNodeMetrics) | Compute node statistical metrics |
| EnvType | String | Compute environment type |
| DesiredComputeNodeCount | Integer | Number of desired compute nodes |

## ComputeNode

Compute node

Referenced by: DescribeComputeEnv.

| Name | Type | Description |
|------|------|-------|
| ComputeNodeId | String | Compute node ID |
| ComputeNodeInstanceId | String | Compute node instance ID; for CVM scenario, CVM InstanceId |
| ComputeNodeState | String | Compute node state |
| Cpu | Integer | Number of CPU cores |
| Mem | Integer | Memory capacity in GB |
| ResourceCreatedTime | String | Resource created time |
| TaskInstanceNumAvailable | Integer | Available capacity of the compute node when running TaskInstance. If 0, the compute node is busy. |
| AgentVersion | String | Batch Agent version |
| PrivateIpAddresses | Array of String | Private IP of the instance |
| PublicIpAddresses | Array of String | Public IP of the instance |

## ComputeNodeMetrics

Compute node statistical metrics

Referenced by: DescribeComputeEnv, DescribeComputeEnvs.

| Name | Type | Description |
|------|------|-------|
| SubmittedCount | String | Number of compute nodes that have been submitted |
| CreatingCount | String | Number of compute nodes that are being created |
| CreationFailedCount | String | Number of compute nodes that failed to be created |
| CreatedCount | String | Number of compute nodes that have been created |
| RunningCount | String | Number of compute nodes that are running |
| DeletingCount | String | Number of compute nodes that are being terminated |
| AbnormalCount | String | Number of abnormal compute nodes |

## DataDisk

This describes data disk information

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskSize | Integer | Yes | Data disk size in GB. The minimum adjustment step width is 10 GB, and the value range varies for different data disk types. For details, see [CVM Instance Configuration](/document/product/213/2177). The default value is 0, which means that data disk is not purchased. For more information about restrictions, see the product documentation. |
| DiskType | String | No | Data disk type. For more information about restrictions on data disk types, see [CVM Instance Configuration](/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: local disk <br><li>LOCAL_SSD: Local SSD <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><br>Default value: LOCAL_BASIC. <br><br>This parameter is not valid for the `ResizeInstanceDisk` API. |
| DiskId | String | No | Data disk ID. The LOCAL_BASIC and LOCAL_SSD types do not have an ID. They don't support this parameter temporarily. |

## Dependency

Dependency

Referenced by: DescribeJob, DescribeJobSubmitInfo, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| StartTask | String | Yes | Dependency start task name |
| EndTask | String | Yes | Dependency end task name |

## Docker

Docker container information

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| User | String | Yes | Docker Hub username or Tencent Registry username |
| Password | String | Yes | Docker Hub password or Tencent Registry password |
| Image | String | Yes | For Docker Hub, enter "[user/repo]:[tag]"; for Tencent Registry, enter "ccr.ccs.tencentyun.com/[namespace/repo]:[tag]" |
| Server | String | No | For Docker Hub, this can be left blank, but please ensure public network access is present. For Tencent Registry, the server address is "ccr.ccs.tencentyun.com" |

## EnhancedService

This describes the conditions of enhancement services for the instance and their settings, such as the Agent of Cloud Security or Cloud Monitor

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | No | This is to enable the Cloud Security service. If this parameter is not specified, the Cloud Security service is enabled by default. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | No | This is to enable the Cloud Monitor service. If this parameter is not specified, the Cloud Monitor service is enabled by default. |

## EnvData

Compute environmental information

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceType | String | Yes | CVM instance type |
| ImageId | String | Yes | CVM image ID |
| SystemDisk | [SystemDisk](#SystemDisk) | No | Information of the instance's system disk configuration |
| DataDisks | Array of [DataDisk](#DataDisk) | No | Information of the instance's data disk configuration |
| VirtualPrivateCloud | [VirtualPrivateCloud](#VirtualPrivateCloud) | No | Information of the VPC configuration |
| InternetAccessible | [InternetAccessible](#InternetAccessible) | No | Information of the Internet bandwidth configuration |
| InstanceName | String | No | CVM instance display name |
| LoginSettings | [LoginSettings](#LoginSettings) | No | Instance login settings |
| SecurityGroupIds | Array of String | No | Security group of the instance |
| EnhancedService | [EnhancedService](#EnhancedService) | No | Enhancement services. This parameter allows you to specify whether to enable services such as Cloud Security and Cloud Monitor. If this parameter is not specified, Cloud Monitor and Cloud Security are enabled by default. |
| InstanceChargeType | String | No | CVM instance billing method <br><li>POSTPAID_BY_HOUR: Postpaid on a per hour basis <br><li>SPOTPAID: Billed on a bidding basis <br>Default value: POSTPAID_BY_HOUR. |
| InstanceMarketOptions | [InstanceMarketOptionsRequest](#InstanceMarketOptionsRequest) | No | Market-related options of the instance, such as the parameters related to the bidding instance |

## EnvVar

Environmental variable

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Environment variable name |
| Value | String | Yes | Environment variable value |

## EventConfig

Event configuration

Referenced by: CreateComputeEnv, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| EventName | String | Yes | Event type |
| EventVars | Array of [EventVar](#EventVar) | Yes | Custom key-value pair |

## EventVar

Custom key-value pair

Referenced by: CreateComputeEnv, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Custom key |
| Value | String | Yes | Custom value |

## Externals

Extended data

Referenced by: DescribeCvmZoneInstanceConfigInfos.

| Name | Type | Required | Description |
|------|------|----------|------|
| ReleaseAddress | Boolean | No | Release address |
| UnsupportNetworks | Array of String | No | Unsupported network type |
| StorageBlockAttr | [StorageBlock](#StorageBlock) | No | HDD local storage properties |

## Filter

> Used to describe key-value pair filters for conditional filtering queries, such as filtering ID, name and state.
> * If there are multiple `Filter`, the relationship among them is logical `AND`.
> * If there are multiple `Values` in the same `Filter`, the relationship among the `Values` in the same `Filter` is logical `OR`.
>
> Take the `Filter` of the [DescribeInstances](https://cloud.tencent.com/document/api/213/15728) API as an example. If you want to query the instances in availability zone (`zone`) "Guangzhou Zone 1" ***and*** with billing method (`instance-charge-type`) "prepaid" **or** "postpaid", the query can be implemented as follows:
```
Filters.0.Name=zone
&Filters.0.Values.0=ap-guangzhou-1
&Filters.1.Name=instance-charge-type
&Filters.1.Values.0=PREPAID
&Filters.1.Values.1=POSTPAID_BY_HOUR
```

Referenced by: DescribeAvailableCvmInstanceTypes, DescribeComputeEnvActivities, DescribeComputeEnvCreateInfos, DescribeComputeEnvs, DescribeCvmZoneInstanceConfigInfos, DescribeJobs, DescribeTaskTemplates.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Field to be filtered. |
| Values | Array of String | Yes | Filter value of the field. |

## InputMapping

Input mapping

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| SourcePath | String | Yes | Source path |
| DestinationPath | String | Yes | Destination path |
| MountOptionParameter | String | No | Mounting configuration item parameter |

## InstanceMarketOptionsRequest

Bidding request-related options

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| MarketType | String | No | Market option type; currently, this only supports the value "spot" |
| SpotOptions | [SpotMarketOptions](#SpotMarketOptions) | No | Bidding-related option |

## InstanceTypeConfig

Information of InstanceTypeConfig available to Batch

Referenced by: DescribeAvailableCvmInstanceTypes.

| Name | Type | Description |
|------|------|-------|
| Mem | Integer | Memory capacity in `GB`. |
| Cpu | Integer | Number of CPU cores. |
| InstanceType | String | Instance model. |
| Zone | String | Availability zone. |
| InstanceFamily | String | Instance model series. |

## InstanceTypeQuotaItem

This describes the instance model quota information

Referenced by: DescribeCvmZoneInstanceConfigInfos.

| Name | Type | Description |
|------|------|-------|
| Zone | String | Availability zone. |
| InstanceType | String | Instance model. |
| InstanceChargeType | String | Instance billing method. Value range: <br><li>PREPAID: Prepaid <br><li>POSTPAID_BY_HOUR: Postpaid <br><li>CDHPAID: Billed based on [CDH](https://cloud.tencent.com/document/product/416), i.e. only CDH is charged but not the instances on CDH. |
| NetworkCard | Integer | Network interface type, for example: 25 for 25 Gbps |
| Externals | [Externals](#Externals) | Extended properties. |
| Cpu | Integer | Number of instance CPU cores. |
| Memory | Integer | Instance memory capacity in `GB`. |
| InstanceFamily | String | Instance model series. |
| TypeName | String | Model name. |
| LocalDiskTypeList | Array of [LocalDiskType](#LocalDiskType) | List of local disk specifications. |
| Status | String | Whether the instance is for sale. |
| Price | [ItemPrice](#ItemPrice) | Selling price of the instance. |

## InternetAccessible

This describes the Internet accessibility of the instance and declare the Internet usage billing method of the instance and the maximum bandwidth

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| InternetChargeType | String | No | Internet billing method. Value range: <br><li>BANDWIDTH_PREPAID: Prepaid by bandwidth <br><li>TRAFFIC_POSTPAID_BY_HOUR: Postpaid by traffic on a per hour basis <br><li>BANDWIDTH_POSTPAID_BY_HOUR: Postpaid by bandwidth on a per hour basis <br><li>BANDWIDTH_PACKAGE: BWP user <br>Default value: TRAFFIC_POSTPAID_BY_HOUR. |
| InternetMaxBandwidthOut | Integer | No | The upper limit of outbound Internet bandwidth in Mbps. Default value: 0 Mbps. The upper limit of bandwidth varies for different models. For details, see [Buying Network Bandwidth](/document/product/213/509). |
| PublicIpAssigned | Boolean | No | Whether to assign a public IP. Value range: <br><li>TRUE: A public IP is assigned <br><li>FALSE: No public IP is assigned <br><br>If the Internet bandwidth is greater than 0 Mbps, either value can be used. The default value is TRUE. If the Internet bandwidth is 0, it is not allowed to assign a public IP. |

## ItemPrice

This describes the price information of a single item

Referenced by: DescribeCvmZoneInstanceConfigInfos.

| Name | Type | Description |
|------|------|-------|
| UnitPrice | Float | Subsequent unit price in CNY. |
| ChargeUnit | String | Subsequent pricing unit; value range: <br><li>HOUR: The pricing unit is on a per hour basis. Currently, scenarios involving this pricing unit include: instance postpaid by hour (POSTPAID_BY_HOUR), bandwidth postpaid by hour (BANDWIDTH_POSTPAID_BY_HOUR); <br><li>GB: The pricing unit is on a per GB basis. Currently, scenarios involving this pricing unit include: traffic postpaid by hour (TRAFFIC_POSTPAID_BY_HOUR). |
| OriginalPrice | Float | Original price of the prepayment in CNY. |
| DiscountPrice | Float | Discounted price of the prepayment in CNY. |

## Job

Job

Referenced by: SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| JobName | String | Yes | Job name |
| Priority | Integer | Yes | Job priority; task (Task) and task instance (TaskInstance) inherit priority of the job |
| Tasks | Array of [Task](#Task) | Yes | Task information |
| JobDescription | String | No | Job description |
| Dependences | Array of [Dependence](#Dependence) | No | Dependency information |
| Notifications | Array of [Notification](#Notification) | No | Notification information |
| TaskExecutionDependOn | String | No | This is the dependency of the subsequent task on the previous task if there is a dependent relationship between them. Value range: PRE_TASK_SUCCEED, PRE_TASK_AT_LEAST_PARTLY_SUCCEED, PRE_TASK_FINISHED. Default value: PRE_TASK_SUCCEED. |
| StateIfCreateCvmFailed | String | No| This indicates which policy will be used in case of CVM creation fails. Value range: FAILED, RUNNABLE. FAILED indicates that the CVM creation failure is processed as an execution failure, while RUNNABLE indicates that the CVM creation failure is processed as "keep waiting". Default value: FAILED. StateIfCreateCvmFailed is not valid for jobs submitted for a specified compute environment. |

## JobView

Job information

Referenced by: DescribeJobs.

| Name | Type | Description |
|------|------|-------|
| JobId | String | Job ID |
| JobName | String | Job name |
| JobState | String | Job state |
| Priority | Integer | Job priority |
| Placement | [Placement](#Placement) | Location information|
| CreateTime | String | Created time |
| EndTime | String | End time |
| TaskMetrics | [TaskMetrics](#TaskMetrics) | Task statistical metrics |

## LocalDiskType

Local disk specifications

Referenced by: DescribeCvmZoneInstanceConfigInfos.

| Name | Type | Description |
|------|------|-------|
| Type | String | Local disk type. |
| PartitionType | String | Local disk properties. |
| MinSize | Integer | Local disk minimum size. |
| MaxSize | Integer | Local disk maximum size. |

## LoginSettings

This describes the configuration and information related to instance login

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Password | String | No | Instance login password. Different operating systems have different password complexity restrictions as follows: <br><li>For Linux instances, the password must be 8 to 16 characters long, including at least two of the following three types of characters: [a-z，A-Z]、[0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]. <br><li>For Windows instances, the passwords must be 12 to 16 characters long, including at least three of the following four types of characters: [a-z], [A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]. <br><br>If this parameter is not specified, the system will generate a random password and notify the user of it through internal messages. |
| KeyIds | Array of String | No | List of key IDs. After the key is associated, the instance can be accessed through the corresponding private key. KeyId can be obtained through the DescribeKeyPairs API. Key and password cannot be specified simultaneously. For Windows, it is not supported to specify the key. Currently, it is only supported to specify a key at the time of purchase. |
| KeepImageLogin | String | No | This is to keep the original settings of the image. This parameter cannot be specified together with Password or KeyIds.N. This parameter can be specified as TRUE only if the instance is created using a custom, shared or imported image. Value range: <br><li>TRUE: This indicates the login settings for the image are kept <br><li>FALSE: This indicates the login settings if the image are not kept <br><br>Default value: FALSE. |

## MountDataDisk

Data disk mounting option

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| LocalPath | String | Yes | Mounting point; for Linux, a valid path; for Windows, the system disk letter such as "H:\\" |
| FileSystemType | String | No | File system type; for Linux, "EXT3" and "EXT4" are supported and the default value is "EXT3"; for Windows, only "NTFS" is supported |

## NamedComputeEnv

Compute environment

Referenced by: CreateComputeEnv.

| Name | Type | Required | Description |
|------|------|----------|------|
| EnvName | String | Yes | Compute environment name |
| EnvType | String | Yes | Compute environment management type |
| EnvData | [EnvData](#EnvData) | Yes | Compute environment's specific parameters |
| DesiredComputeNodeCount | Integer | Yes | Number of desired compute nodes |
| EnvDescription | String | No | Compute environment description |
| MountDataDisks | Array of [MountDataDisk](#MountDataDisk) | No | Data disk mounting option |
| Authentications | Array of [Authentication](#Authentication) | No | Authentication information |
| InputMappings | Array of [InputMapping](#InputMapping) | No | Input mapping information |
| AgentRunningMode | [AgentRunningMode](#AgentRunningMode) | No | Agent running mode; applicable for Windows OS |
| Notifications | [Notification](#Notification) | No | Notification information |
| ActionIfComputeNodeInactive | String | No | Inactive node processing policy; default value: RECREATE, which means that instance resources are re-created periodically for the compute node where instance creation fails or is abnormally returned. |

## Notification

Notification information

Referenced by: CreateComputeEnv, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| TopicName | String | Yes | CMQ topic name which has to be valid and associated with a subscription |
| EventConfigs | Array of [EventConfig](#EventConfig) | Yes | Event configuration |

## OutputMapping

Output mapping

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| SourcePath | String | Yes | Source path |
| DestinationPath | String | Yes | Destination path |

## OutputMappingConfig

Output mapping configuration

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Scene | String | Yes | Storage type; only COS is supported |
| WorkerNum | Integer | Yes | Number of concurrent workers |
| WorkerPartSize | Integer | Yes | Worker block size |

## Placement

This describes the abstract location of the instance, including the availability zone in which it resides, the project it belongs to and the host (only available for CDH)

Referenced by: CreateComputeEnv, DescribeComputeEnv, DescribeComputeEnvs, DescribeJobs, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Zone | String | Yes | ID of the [availability zone](/document/product/213/9452#zone) to which the instance belongs. This parameter can also be obtained by calling the Zone field in the return value of [DescribeZones](/document/api/213/9455). |
| ProjectId | Integer | No | ID of the project to which the instance belongs. This parameter can also be obtained by calling the projectId field in the return value of [DescribeProject](/document/api/378/4400). If left blank, the default project. |
| HostIds | Array of String | No | ID List of the CDH to which the instance belongs. If you have purchased dedicated hosts and specified this parameter, the instances you purchase will be randomly deployed on these hosts. |

## RedirectInfo

Redirection information


Referenced by: CreateTaskTemplate, DescribeJob, DescribeJobSubmitInfo, DescribeTask, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| StdoutRedirectPath | String | No | Standard output redirection path |
| StderrRedirectPath | String | No | Standard error redirection path |
| StdoutRedirectFileName | String | No | Standard output redirection file name, which supports three placeholders: ${BATCH_JOB_ID}, ${BATCH_TASK_NAME}, ${BATCH_TASK_INSTANCE_INDEX} |
| StderrRedirectFileName | String | No | Standard error redirection file name, which supports three placeholders: ${BATCH_JOB_ID}, ${BATCH_TASK_NAME}, ${BATCH_TASK_INSTANCE_INDEX} |

## RedirectLocalInfo

Local redirection information

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| StdoutLocalPath | String | No | Standard output redirection local path |
| StderrLocalPath | String | No | Standard error redirection local path |
| StdoutLocalFileName | String | No | Standard output redirection local file name, which supports three placeholders: ${BATCH_JOB_ID}, ${BATCH_TASK_NAME}, ${BATCH_TASK_INSTANCE_INDEX} |
| StderrLocalFileName | String | No | Standard error redirection local file name, which supports three placeholders: ${BATCH_JOB_ID}, ${BATCH_TASK_NAME}, ${BATCH_TASK_INSTANCE_INDEX} |

## RunMonitorServiceEnabled

This describes the information related to the Cloud Monitor service

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable the [Cloud Monitor](/document/product/248) service. Value range: <br><li>TRUE: Cloud Monitor is enabled <br><li>FALSE: Cloud Monitor is disabled <br><br>Default value: TRUE. |

## RunSecurityServiceEnabled

This describes the information about the Cloud Security service

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable the [Cloud Security](/document/product/296) service. Value range: <br><li>TRUE: Cloud Security is enabled <br><li>FALSE: Cloud Security is disabled <br><br>Default value: TRUE. |

## SpotMarketOptions

Bidding-related options

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| MaxPrice | String | Yes | Bidding price |
| SpotInstanceType | String | No | Spot request type; currently, only "one-time" type is supported |

## StorageBlock

HDD local storage information

Referenced by: DescribeCvmZoneInstanceConfigInfos.

| Name | Type | Description |
|------|------|-------|
| Type | String | HDD local storage type, value: LOCAL_PRO. |
| MinSize | Integer | Minimum capacity of HDD local storage |
| MaxSize | Integer | Maximum capacity of HDD local storage |

## SystemDisk

This describes the information about the block device (i.e. system disk) where the operating system resides

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | No | System disk type. For more information about restrictions on system disk types, see [CVM Instance Configuration](/document/product/213/2177). Value range: <br><li>LOCAL_BASIC: Local disk <br><li>LOCAL_SSD: Local SSD <br><li>CLOUD_BASIC: HDD cloud disk <br><li>CLOUD_SSD: SSD cloud disk <br><li>CLOUD_PREMIUM: Premium cloud disk <br><br>Default value: CLOUD_BASIC. |
| DiskId | String | No | System disk ID. The LOCAL_BASIC and LOCAL_SSD types do not have an ID. They don't support this parameter temporarily. |
| DiskSize | Integer | No | System disk size in GB. Default value: 50 |

## Task

Task

Referenced by: CreateTaskTemplate, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| TaskName | String | Yes | Task name; unique within a job |
| TaskInstanceNum | Integer | Yes | Number of running task instances |
| Application | [Application](#Application) | Yes | Application information |
| RedirectInfo | [RedirectInfo](#RedirectInfo) | Yes | Redirection information |
| MaxRetryCount | Integer | Yes | Maximum number of retries after a task fails; default value: 0 |
| Timeout | Integer | Yes | Timeout after the task starts in seconds; defaults value: 3600 |
| ComputeEnv | [AnonymousComputeEnv](#AnonymousComputeEnv) | No | Compute environment information; one (and only one) parameter must be specified for ComputeEnv and EnvId. |
| EnvId | String | No | Compute environment ID; one (and only one) parameter must be specified for ComputeEnv and EnvId. |
| RedirectLocalInfo | [RedirectLocalInfo](#RedirectLocalInfo) | No | Redirection local information |
| InputMappings | Array of [InputMapping](#InputMapping) | No | Input mapping |
| OutputMappings | Array of [OutputMapping](#OutputMapping) | No | Output mapping |
| OutputMappingConfigs | Array of [OutputMappingConfig](#OutputMappingConfig) | No | Output mapping configuration |
| EnvVars | Array of [Authentication](#Authentication) | No | Custom environment variable |
| Authentications | Array of [EnvVar](#EnvVar) | No | Authentication information |
| FailedAction | String | No | The processing method after TaskInstance fails; values range: TERMINATE (default), INTERRUPT, FAST_INTERRUPT. |

## TaskInstanceMetrics

Task instance statistical metrics

Referenced by: DescribeTask.

| Name | Type | Description |
|------|------|-------|
| SubmittedCount | Integer | Number of submitted instances |
| PendingCount | Integer | Number of pending instances |
| RunnableCount | Integer | Number of runnable instances |
| StartingCount | Integer | Number of starting instances |
| RunningCount | Integer | Number of running instances |
| SucceedCount | Integer | Number of succeeding instances |
| FailedInterruptedCount | Integer | Number of FailedInterrupted instances |
| FailedCount | Integer | Number of failing instances |

## TaskInstanceView

Task instance view information

Referenced by: DescribeJob, DescribeTask.

| Name | Type | Description |
|------|------|-------|
| TaskInstanceIndex | Integer | Task instance index |
| TaskInstanceState | String | Task instance state |
| ExitCode | Integer | Exit code after application execution is completed |
| StateReason | String | Task instance state reason; if the task instance fails, the reason for the failure will be logged |
| ComputeNodeInstanceId | String | The InstanceId of the compute node (e.g. CVM) at which the task instance is running. This field is empty if the task instance is not running or has already been completed. This field will change when the task instance is retried |
| CreateTime | String | Created time |
| LaunchTime | String | Launch time |
| RunningTime | String | Running start time |
| EndTime | String | End time |
| RedirectInfo | [RedirectInfo](#RedirectInfo) | Redirection information|
| StateDetailedReason | String | Task instance state reason details; if the task instance fails, the reason for the failure will be logged |

## TaskMetrics

Task statistical metrics

Referenced by: DescribeJob, DescribeJobs.

| Name | Type | Description |
|------|------|-------|
| SubmittedCount | Integer | Number of submitted instances |
| PendingCount | Integer | Number of pending instances |
| RunnableCount | Integer | Number of runnable instances |
| StartingCount | Integer | Number of starting instances |
| RunningCount | Integer | Number of running instances |
| SucceedCount | Integer | Number of succeeding instances |
| FailedInterruptedCount | Integer | Number of FailedInterrupted instances |
| FailedCount | Integer | Number of failing instances |

## TaskTemplateView

Task template information

Referenced by: DescribeTaskTemplates.

| Name | Type | Description |
|------|------|-------|
| TaskTemplateId | String | Task template ID |
| TaskTemplateName | String | Task template name |
| TaskTemplateDescription | String | Task template description |
| TaskTemplateInfo | [Task](#Task) | Task template information |
| CreateTime | String | Created time |

## TaskView

Task view information

Referenced by: DescribeJob.

| Name | Type | Description |
|------|------|-------|
| TaskName | String | Task name |
| TaskState | String | Task state |
| CreateTime | String | Start time |
| EndTime | String | End time |

## VirtualPrivateCloud

This describes the information related to VPC, including subnet and IP

Referenced by: CreateComputeEnv, CreateTaskTemplate, DescribeComputeEnvCreateInfo, DescribeComputeEnvCreateInfos, DescribeJobSubmitInfo, DescribeTaskTemplates, ModifyTaskTemplate, SubmitJob.

| Name | Type | Required | Description |
|------|------|----------|------|
| VpcId | String | Yes | VPC ID in the format of `vpc-xxx`. A valid VpcId can be queried by logging in to the [console](https://console.cloud.tencent.com/vpc/vpc?rid=1) or obtained from the `unVpcId` field returned after calling the [DescribeVpcEx](/document/api/215/1372) API. |
| SubnetId | String | Yes | VPC subnet ID in the format of `subnet-xxx`. A valid SubnetId can be queried by logging in to the [console](https://console.cloud.tencent.com/vpc/subnet?rid=1) or obtained from the `unSubnetId` field returned after calling the [DescribeSubnets](/document/api/215/15784) API. |
| AsVpcGateway | Boolean | No | Whether to use as a public gateway. Public gateway can be used normally only if the instance has a public IP and is in a VPC. Value range: <br><li>TRUE: Used as a public gateway <br><li>FALSE: Not used as a public gateway <br><br>Default value: FALSE. |
| PrivateIpAddresses | Array of String | No | VPC subnet IP array, which can be used when creating an instance or modifying the instance's VPC properties. Currently, multiple IPs from the same subnet can be passed in only when batch creating multiple instances. |
