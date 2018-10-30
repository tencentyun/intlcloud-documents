## ConstraintRange

Range of constraint type values

It is referenced by the API DescribeDBParameters.

| Name | Type | Description |
|------|------|-------|
| Min | String | The minimum value when constraint type is "section" |
| Max | String | The maximum value when constraint type is "section" |

## DBAccount

Information of the database account

It is referenced by the API DescribeAccounts.

| Name | Type | Description |
|------|------|-------|
| UserName | String | User name |
| Host | String | Server used for login which is corresponding to the "host" field of a MySQL user (UserName + Host is a unique identifier to a user). The server is in the form of an IP ending with %. Null means %. |
| Description | String | User notes |
| CreateTime | Timestamp | Creation time |
| UpdateTime | Timestamp | Last update time |
| ReadOnly | Integer | Read-only tag. 0: No; 1: Slave is preferred for the SQL request of the account. The master is used when the slave is not available; 2: The slave is preferred. The operation fails if the slave is not available. |
| DelayThresh | Integer | Used only for read-only accounts. Select the slave whose master/slave delay is less than this value. |

## DBBackupTimeConfig

Backup time configurations of a database instance

It is referenced by the API DescribeBackupTime.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| StartBackupTime | String | Start time of daily backup time span. Format: mm:ss, such as 22:00. |
| EndBackupTime | String | End time of daily backup time span. Format: mm:ss, such as 23:00. |

## DBInstance

Database instance details

It is referenced by DescribeDBInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID, which is used to uniquely identify a TDSQL instance. |
| InstanceName | String | Instance name, which can be customized. |
| AppId | Integer | Instance App ID |
| ProjectId | Integer | Project ID to which an instance belongs |
| Region | String | Name of the region in which the instance resides, such as ap-shanghai |
| Zone | String | Name of the availability zone in which the instance resides, such as ap-shanghai-1. |
| VpcId | Integer | VPC ID. 0 is for basic network. |
| SubnetId | Integer | Subnet ID. 0 indicates basic network. |
| Status | Integer | Instance status: 0 Creating; 1 In process; 2 Running; 3 Uninitialized; -1 Isolated; -2 Deleted. |
| Vip | String | Private IP address |
| Vport | Integer | Private network port |
| WanDomain | String | Domain name of public network, which can be parsed by public network. |
| WanVip | String | Public IP address, which can be accessed via public network. |
| WanPort | Integer | Public network port |
| CreateTime | Timestamp | Instance creation time, such as 2006-01-02 15:04:05. |
| UpdateTime | Timestamp | Last update time of the instance, such as 2006-01-02 15:04:05. |
| AutoRenewFlag | Integer | Auto renewal flag. 0: No; 1: Yes. |
| PeriodEndTime | Timestamp | Expiration time of an instance, such as 2006-01-02 15:04:05. |
| Uin | String | ID of the account to which the instance belongs |
| TdsqlVersion | String | TDSQL version details |
| Memory | Integer | Memory capacity of the instance (in GB) |
| Storage | Integer | Instance storage space (in GB) |
| UniqueVpcId | String | VPC ID (string) |
| UniqueSubnetId | String | VPC subnet ID (string) |
| OriginSerialId | String | Original instance ID, which is obsolete. Please don't refer to this value. |
| NodeCount | Integer | Number of nodes. 2: one master node with one slave node; 3: one master node with two slave nodes. |
| IsTmp | Integer | Whether it is a temporary instance. 0: No; other values: Yes. |
| ExclusterId | String | Exclusive cluster ID. Null: regular instance. |
| Id | Integer | Digital instance ID, which is obsolete. Please don't refer to this value. |
| Pid | Integer | Product type ID |
| Qps | Integer | Maximum QPS |
| Paymode | String | Billing method |
| Locker | Integer | Asynchronous task process ID when the instance is processing asynchronous tasks |
| StatusDesc | String | Description of instance execution status |

## DBParamValue

Database parameters.

It is referenced by InitDBInstances and ModifyDBParameters.

| Name | Type | Required | Description |
|------|------|----------|------|
| Param | String | Yes | Parameter name |
| Value | String | Yes | Parameter value |

## Deal

Order information

It is referenced by DescribeOrders.

| Name | Type | Description |
|------|------|-------|
| DealName | String | Order number |
| OwnerUin | String | Account |
| Count | Integer | Quantity of goods |
| FlowId | Integer | Associated process ID, which can be used to query the process execution status. |
| InstanceIds | Array of String | This filed is required only for the order for which an instance is created, and indicates the ID of the created instance. |
| PayMode | Integer | Billing method. 0: postpaid; 1: prepaid. |

## InstanceSpec

Available instance specification by models

It is referenced by the API DescribeDBInstanceSpecs.

| Name | Type | Required | Description |
|------|------|----------|------|
| Machine | String | Yes | Device model |
| SpecInfos | Array of [SpecConfigInfo](#SpecConfigInfo) | Yes | List of available specifications of the model |

## LogFileInfo

Pulled log information

It is referenced by the API DescribeDBLogFiles.

| Name | Type | Description |
|------|------|-------|
| Mtime | Integer | Last modification time of the log |
| Length | Integer | File length |
| Uri | String | Uniform resource identifier used to download logs |

## MonitorData

Monitoring data

It is referenced by DescribeDBPerformance, DescribeDBPerformanceDetails, DescribeDBResourceUsage and DescribeDBResourceUsageDetails.

| Name | Type | Description |
|------|------|-------|
| StartTime | Timestamp | Start time, such as 2018-03-24 23:59:59. |
| EndTime | Timestamp | End time, such as 2018-03-24 23:59:59. |
| Data | Array of Float | Monitoring data |

## MonitorIntData

Integer monitoring data

It is referenced by the API DescribeDBResourceUsageDetails.

| Name | Type | Description |
|------|------|-------|
| StartTime | Timestamp | Start time |
| EndTime | Timestamp | End time |
| Data | Integer | Monitoring data |

## ParamConstraint

Parameter constraints

It is referenced by the API DescribeDBParameters.

| Name | Type | Description |
|------|------|-------|
| Type | String | Constraint type, such as enum and section. |
| Enum | String | List of available values when constraint type is "enum" |
| Range | [ConstraintRange](#ConstraintRange) | Range when constraint type is "section" |
| String | String | List of available values when constraint type is "string" |

## ParamDesc

Database parameter description

It is referenced by the API DescribeDBParameters.

| Name | Type | Description |
|------|------|-------|
| Param | String | Parameter name |
| Value | String | Current parameter value |
| SetValue | String | The set value, which is the same as "value". This field is not returned if not set. |
| Default | String | Default value |
| Constraint | [ParamConstraint](#ParamConstraint) | Parameter constraints |

## ParamModifyResult

Result of parameter modification

It is referenced by the API ModifyDBParameters.

| Name | Type | Description |
|------|------|-------|
| Param | String | Parameter name to be modified |
| Code | Integer | Parameter modification result. 0: Successful; -1: Failed; -2: The parameter value is invalid. |

## PerformanceMonitorSet

A set of database performance monitoring metrics

It is referenced by the API DescribeDBPerformanceDetails.

| Name | Type | Description |
|------|------|-------|
| UpdateTotal | [MonitorData](#MonitorData) | Number of UPDATE actions |
| DiskIops | [MonitorData](#MonitorData) | IOs per second of the disk |
| ConnActive | [MonitorData](#MonitorData) | Active connections |
| MemHitRate | [MonitorData](#MonitorData) | Cache hit rate |
| SlaveDelay | [MonitorData](#MonitorData) | Master/slave delay |
| SelectTotal | [MonitorData](#MonitorData) | Number of SELECT actions |
| LongQuery | [MonitorData](#MonitorData) | Number of slow logs |
| DeleteTotal | [MonitorData](#MonitorData) | Number of DELETE actions |
| InsertTotal | [MonitorData](#MonitorData) | Number of INSERT actions |
| IsMasterSwitched | [MonitorData](#MonitorData) | Whether a switching between the master and slave occurs. 1: Yes; 0: No. |

## RegionInfo

Information of supported availability zone

It is referenced by the API DescribeSaleInfo.

| Name | Type | Description |
|------|------|-------|
| Region | String | Region ID |
| RegionId | Integer | Region number |
| RegionName | String | Region name |
| ZoneList | Array of [ZonesInfo](#ZonesInfo) | List of availability zones |
| AvailableChoice | Array of [ZoneChooseInfo](#ZoneChooseInfo) | Supported master/slave availability zone |

## ResourceUsageMonitorSet

A set of monitoring metrics of database resource usage

It is referenced by the API DescribeDBResourceUsageDetails.

| Name | Type | Description |
|------|------|-------|
| BinlogDiskAvailable | [MonitorData](#MonitorData) | Available space of a binlog disk (in GB) |
| CpuUsageRate | [MonitorData](#MonitorData) | CPU utilization |
| MemAvailable | [MonitorData](#MonitorData) | Available space of memory (in GB) |
| DataDiskAvailable | [MonitorIntData](#MonitorIntData) | Available space of a disk (in GB) |

## SlowLogData

Slow log information

It is referenced by the API DescribeDBSlowLogs.

| Name | Type | Description |
|------|------|-------|
| CheckSum | String | Statement checksum used for querying details |
| Db | String | Database name |
| FingerPrint | String | Abstract SQL statement |
| LockTimeAvg | Float | Average lock time |
| LockTimeMax | Float | Maximum lock time |
| LockTimeMin | Float | Minimum lock time |
| LockTimeSum | Float | Total lock time |
| QueryCount | Integer | Count of queries |
| QueryTimeAvg | Float | Average query time |
| QueryTimeMax | Float | Maximum query time |
| QueryTimeMin | Float | Minimum query time |
| QueryTimeSum | Float | Total query time |
| RowsExaminedSum | Integer | Number of rows examined |
| RowsSentSum | Integer | Number of rows sent |
| TsMax | Timestamp | First execution time |
| TsMin | Timestamp | Last execution time |
| User | String | Account |

## SpecConfigInfo

Available specifications of an instance. Pid+MemSize is unique to a specification and available disk capacity range is [MinDataDisk,MaxDataDisk] during instance creation and capacity expansion.

It is referenced by the API DescribeDBInstanceSpecs.

| Name | Type | Description |
|------|------|-------|
| Machine | String | Device model |
| Memory | Integer | Memory capacity (in GB) |
| MinStorage | Integer | Minimum disk space (in GB) |
| MaxStorage | Integer | Maximum disk space (in GB) |
| SuitInfo | String | Recommended scenarios |
| Qps | Integer | Maximum QPS |
| Pid | Integer | Product type ID |
| NodeCount | Integer | Number of nodes. 2: one master node with one slave node; 3: one master node with two slave nodes. |

## SqlLogItem

SQL log details

It is referenced by the API DescribeSqlLogs.

| Name | Type | Description |
|------|------|-------|
| Offset | Integer | Offset of the log in the message queue |
| User | String | User executing this SQL |
| Client | String | Client IP and port executing this SQL |
| DbName | String | Database name |
| Sql | String | SQL statement executed |
| SelectRowNum | Integer | Number of rows returned |
| AffectRowNum | Integer | Number of rows affected |
| Timestamp | Integer | Timestamp when the SQL is executed |
| TimeCostMs | Integer | Time consumed by SQL (in ms) |
| ResultCode | Integer | SQL error code. 0: Successful. |

## ZoneChooseInfo

Selection of availability zones of shard nodes

It is referenced by the API DescribeSaleInfo.

| Name | Type | Description |
|------|------|-------|
| MasterZone | [ZonesInfo](#ZonesInfo) | Master availability zone |
| SlaveZones | Array of [ZonesInfo](#ZonesInfo) | Supported slave availability zone |

## ZonesInfo

Information of availability zone

It is referenced by the API DescribeSaleInfo.

| Name | Type | Description |
|------|------|-------|
| Zone | String | Availability zone ID |
| ZoneId | Integer | Availability zone number |
| ZoneName | String | Availability zone name |


