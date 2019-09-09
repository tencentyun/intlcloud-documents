## CosBackup

Configuration of auto-backup to COS

Referenced by: DescribeInstances, UpdateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| IsAutoBackup | Boolean | Yes | Whether to enable auto-backup to COS |
| BackupTime | String | Yes | Auto-backup time (accurate down to the hour), such as "22:00" |

## DictInfo

Information of the IK plugin dictionary

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| Key | String | Dictionary key value |
| Name | String | Dictionary name |
| Size | Integer | Dictionary size in B |

## EsAcl

ES cluster configuration item

Referenced by: DescribeInstances, UpdateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| BlackIpList | Array of String | No | Kibana access blacklist |
| WhiteIpList | Array of String | No | Kibana access whitelist |

## EsDictionaryInfo

ES IK dictionary information

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| MainDict | Array of [DictInfo](#DictInfo) | Non-stop word dictionary list |
| Stopwords | Array of [DictInfo](#DictInfo) | Stop word dictionary list |

## InstanceInfo

Instance details

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| InstanceName | String | Instance name |
| Region | String | Region |
| Zone | String | AZ |
| AppId | Integer | User ID |
| Uin | String | User UIN |
| VpcUid | String | UID of the VPC where the instance resides |
| SubnetUid | String | UID of the subnet where the instance resides |
| Status | Integer | Instance status. 0: processing; 1: normal; -1: stopped; -2: terminating; -3: terminated |
| ChargeType | String | Instance billing method. Value range: PREPAID: Monthly subscription; POSTPAID_BY_HOUR: Pay-as-you-go on an hourly basis; CDHPAID: Billed based on CDH, i.e., only CDH is billed but not the instances on CDH. |
| ChargePeriod | Integer | Purchased duration for monthly subscription in month |
| RenewFlag | String | Auto-renewal flag. Value range: NOTIFY_AND_AUTO_RENEW: Notify of expiry and auto-renew; NOTIFY_AND_MANUAL_RENEW: Notify of expiry but do not auto-renew; DISABLE_NOTIFY_AND_MANUAL_RENEW: Do not notify of expiry or auto-renew. NOTIFY_AND_AUTO_RENEW by default. If this parameter is specified as NOTIFY_AND_AUTO_RENEW, the instance will be auto-renewed on a monthly basis upon expiry. |
| NodeType | String | Node specification <li>ES.S1.SMALL2: 1-core 2 GB </li><li>ES.S1.MEDIUM4: 2-core 4 GB </li><li>ES.S1.MEDIUM8: 2-core 8 GB </li><li>ES.S1.LARGE16: 4-core 16 GB </li><li>ES.S1.2XLARGE32: 8-core 32 GB </li><li>ES.S1.4XLARGE32: 16-core 32 GB </li><li>ES.S1.4XLARGE64: 16-core 64 GB </li> |
| NodeNum | Integer | Number of nodes |
| CpuNum | Integer | Number of CPU cores of the node |
| MemSize | Integer | Node memory size in GB |
| DiskType | String | Node disk type |
| DiskSize | Integer | Node disk size in GB |
| EsDomain | String | ES domain name |
| EsVip | String | ES VIP |
| EsPort | Integer | ES port |
| KibanaUrl | String | Kibana access URL |
| EsVersion | String | ES version number |
| EsConfig | String | ES configuration item |
| EsAcl | [EsAcl](#EsAcl) | ES access control configuration |
| CreateTime | String | Creation time of the instance |
| UpdateTime | String | Last modified time of the instance |
| Deadline | String | Instance expiry time |
| InstanceType | Integer | Instance type (instance type identifier, which can be only 1 or 2 currently) |
| IkConfig | [EsDictionaryInfo](#EsDictionaryInfo) | IK analyzer configuration |
| MasterNodeInfo | [MasterNodeInfo](#MasterNodeInfo) | Dedicated master node configuration |
| CosBackup | [CosBackup](#CosBackup) | Configuration of auto-backup to COS |
| AllowCosBackup | Boolean | Whether to allow auto-backup to COS |
| TagList | Array of [TagInfo](#TagInfo) | List of tags owned by the instance |
| LicenseType | String | License type <li>oss: Open Source Edition </li><li>basic: Basic Edition </li><li>platinum: Platinum Edition </li>platinum by default |

## InstanceLog

Details of an ES cluster log

Referenced by: DescribeInstanceLogs.

| Name | Type | Description |
|------|------|-------|
| Time | String | Log time |
| Level | String | Log level |
| Ip | String | Cluster node IP |
| Message | String | Log content |

## KeyValue

OperationDetail uses an array of this structure to describe the old and new configuration information

Referenced by: DescribeInstanceOperations.

| Name | Type | Description |
|------|------|-------|
| Key | String | Key |
| Value | String | Value |

## MasterNodeInfo

Information of the dedicated master node in an instance

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| EnableDedicatedMaster | Boolean | Whether to enable the dedicated master node |
| MasterNodeType | String | Dedicated master node specification <li>ES.S1.SMALL2: 1-core 2 GB</li><li>ES.S1.MEDIUM4: 2-core 4 GB</li><li>ES.S1.MEDIUM8: 2-core 8 GB</li><li>ES.S1.LARGE16: 4-core 16 GB</li><li>ES.S1.2XLARGE32: 8-core 32 GB</li><li>ES.S1.4XLARGE32: 16-core 32 GB</li><li>ES.S1.4XLARGE64: 16-core 64 GB</li> |
| MasterNodeNum | Integer | Number of dedicated master nodes |
| MasterNodeCpuNum | Integer | Number of CPU cores of the dedicated master node |
| MasterNodeMemSize | Integer | Memory size of the dedicated master node in GB |
| MasterNodeDiskSize | Integer | Disk size of the dedicated master node in GB |
| MasterNodeDiskType | String | Disk type of the dedicated master node |

## MultiZoneInfo

Details of AZs in multi-AZ deployment mode

Referenced by: CreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| Zone | String | Yes | AZ |
| SubnetId | String | Yes | Subnet ID |

## Operation

Details of an ES cluster activity

Referenced by: DescribeInstanceOperations.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID of an activity |
| StartTime | String | Activity start time |
| Type | String | Activity type |
| Detail | [OperationDetail](#OperationDetail) | Activity details |
| Result | String | Activity result |
| Tasks | Array of [TaskDetail](#TaskDetail) | Flow task information |
| Progress | Float | Activity progress |

## OperationDetail

Activity details

Referenced by: DescribeInstanceOperations.

| Name | Type | Description |
|------|------|-------|
| OldInfo | Array of [KeyValue](#KeyValue) | Original configuration information of the instance |
| NewInfo | Array of [KeyValue](#KeyValue) | Updated configuration information of the instance |

## SubTaskDetail

Information of a sub-task in a flow task in the instance activity record (such as each check item in a check for update task)

Referenced by: DescribeInstanceOperations.

| Name | Type | Description |
|------|------|-------|
| Name | String | Sub-task name |
| Result | Boolean | Sub-task result |
| ErrMsg | String | Sub-task error message |

## TagInfo

Instance tag information

Referenced by: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| TagKey | String | Tag key |
| TagValue | String | Tag key |

## TaskDetail

Information of a flow task in the instance activity record

Referenced by: DescribeInstanceOperations.

| Name | Type | Description |
|------|------|-------|
| Name | String | Task name |
| Progress | Float | Task progress |
| FinishTime | String | Task completion time |
| SubTasks | Array of [SubTaskDetail](#SubTaskDetail) | Sub-task |

