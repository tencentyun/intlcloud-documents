## AccountCreateInfo

Account creation information

Referenced by: CreateAccount.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | Instance username |
| Password | String | Yes | Instance password |
| DBPrivileges | Array of [DBPrivilege](#DBPrivilege) | No | Database permission list |
| Remark | String | No | Account remarks |

## AccountDetail

Account details

Referenced by: DescribeAccounts.

| Name | Type | Description |
|------|------|-------|
| Name | String | Account name |
| Remark | String | Account remarks |
| CreateTime | Timestamp | Account creation time |
| Status | Integer | Account status; 1: creating, 2: normal, 3: modifying, 4: resetting password, -1: deleting |
| UpdateTime | Timestamp | Account update time |
| PassTime | Timestamp | Password update time |
| InternalStatus | String | Internal account status; normal status: "enable" |
| Dbs | Array of [DBPrivilege](#DBPrivilege) | Information about account’s database read and write permissions |

## AccountPassword

Instance account password information

Referenced by: ResetAccountPassword.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | Username |
| Password | String | Yes | Password |

## AccountPrivilege

Database account permission information, which is set when the database is created

Referenced by: CreateDB, DescribeDBs.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | Database username |
| Privilege | String | Yes | Database permissions. ReadWrite: read and write, ReadOnly: read-only |

## AccountPrivilegeModifyInfo

Database account permission change information

Referenced by: ModifyAccountPrivilege.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | Database username |
| DBPrivileges | Array of [DBPrivilegeModifyInfo](#DBPrivilegeModifyInfo) | Yes | Account permission change information |

## AccountRemark

Account remarks

Referenced by: ModifyAccountRemark.

| Name | Type | Description |
|------|------|-------|
| UserName | String | Account name |
| Remark | String | New remarks of the account |

## Backup

Backup file details

Referenced by: DescribeBackups.

| Name | Type | Description |
|------|------|-------|
| FileName | String | Filename |
| Size | Integer | File size in KB |
| StartTime | Timestamp | Backup start time |
| EndTime | Timestamp | Backup end time |
| InternalAddr | String | Download address on the private network |
| ExternalAddr | String | Download address on the public network |
| Id | Integer | Unique ID of the backup file, which will be used by the RestoreInstance API |
| Status | Integer | Backup file status (0: creating, 1: succeeded, 2: failed) |
| DBs | Array of String | List of databases for multi-database backup |
| Strategy | Integer | Backup policy (0: instance backup, 1: multi-database backup) |
| BackupWay | Integer | Backup mode. 0: scheduled, 1: manual |

## DBCreateInfo

Database creation information

Referenced by: CreateDB.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Charset | String | Yes | Character set. Valid values: Chinese_PRC_CI_AS, Chinese_PRC_CS_AS, Chinese_PRC_BIN, Chinese_Taiwan_Stroke_CI_AS, SQL_Latin1_General_CP1_CI_AS, and SQL_Latin1_General_CP1_CS_AS. If this field is left empty, default is Chinese_PRC_CI_AS
| Accounts | Array of [AccountPrivilege](#AccountPrivilege) | Yes | Database account permission information |
| Remark | String | Yes | Remarks |

## DBDetail

Database information

Referenced by: DescribeDBs.

| Name | Type | Description |
|------|------|-------|
| Name | String | Instance ID |
| Charset | String | Character set |
| Remark | String | Remarks |
| CreateTime | Timestamp | Database creation time |
| Status | Integer | Database status. 1: creating, 2: running, 3: modifying, -1: deleting |
| Accounts | Array of [AccountPrivilege](#AccountPrivilege) | Database account permission information |
| InternalStatus | String | Internal status. ONLINE: running |

## DBInstance

Instance details

Referenced by: DescribeDBInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| Name | String | Instance name |
| ProjectId | Integer | ID of the project to which the instance belongs |
| RegionId | Integer | Instance region ID |
| ZoneId | Integer | Instance AZ ID |
| VpcId | Integer | Instance VPC ID, which is 0 if a basic network is used |
| SubnetId | Integer | Instance VPC subnet ID, which is 0 if a basic network is used |
| Status | Integer | Instance status. Value range: <li>1: applying </li> <li>2: running </li> <li>3: restrictedly running (master/slave switching) </li> <li>4: isolated </li> <li>5: repossessing </li> <li>6: repossessed </li> <li>7: task running (e.g., backing up or rolling back the instance) </li> <li>8: decommissioned </li> <li>9: scaling </li> <li>10: migrating </li> <li>11: read-only </li> <li>12: restarting </li> |
| Vip | String | Instance access IP |
| Vport | Integer | Instance access port |
| CreateTime | Timestamp | Instance creation time |
| UpdateTime | Timestamp | Instance update time |
| StartTime | Timestamp | Instance billing start time |
| EndTime | Timestamp | Instance billing end time |
| IsolateTime | Timestamp | Instance isolation time |
| Memory | Integer | Instance memory size in GB |
| UsedStorage | Integer | Used storage capacity of the instance in GB |
| Storage | Integer | Instance storage capacity in GB |
| VersionName | String | Instance version |
Model | Integer | Instance high availability (HA). 1: dual-server HA, 2: single-server |
| Region | String | Instance region name such as ap-guangzhou |
| Zone | String | Instance Availability Zone name such as ap-guangzhou-1 |
| BackupTime | String | Backup time |

## DBPrivilege

Database permission information of the account

Referenced by: CreateAccount, DescribeAccounts.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Privilege | String | Yes | Database permissions. ReadWrite: read and write, ReadOnly: read-only |

## DBPrivilegeModifyInfo

Database permission change information

Referenced by: ModifyAccountPrivilege.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Privilege | String | Yes | Permission change information. ReadWrite: read and write, ReadOnly: read-only, Delete: the account has the permission to delete this database |

## DBRemark

Database remarks

Referenced by: ModifyDBRemark.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Database name |
| Remark | String | Yes | Remarks |

## DbRollbackTimeInfo

Information of the time range available for database rollback

Referenced by: DescribeRollbackTime.

| Name | Type | Description |
|------|------|-------|
| DBName | String | Database name |
| StartTime | Timestamp | Start time available for rollback |
| EndTime | Timestamp | End time available for rollback |

## DealInfo

Order information

Referenced by: DescribeOrders.

| Name | Type | Description |
|------|------|-------|
| DealName | String | Order name |
| Count | Integer | Item quantity |
| FlowId | Integer | ID of the associated flow, which can be used to query the flow execution status |
| InstanceIdSet | Array of String |  ID of the instance created for the specified order. This field is required only for the order for which an instance has been created. |
| OwnerUin | String | Account |

## InstanceDBDetail

Instance database information

Referenced by: DescribeDBs.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| DBDetails | Array of [DBDetail](#DBDetail) | Database information list |

## MigrateDB

List of databases to be migrated

Referenced by: CreateMigration, DescribeMigrationDetail, ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | No | Name of the database to be migrated |

## MigrateDetail

Migration progress details

Referenced by: DescribeMigrations.

| Name | Type | Description |
|------|------|-------|
| StepName | String | Name of the current step |
| Progress | Integer | Progress of the current step (in %) |

## MigrateSource

Source type of the migration task

Referenced by: CreateMigration, DescribeMigrationDetail, ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceId | String | No | ID of the source instance in the format of mssql-si2823jyl, which is used when MigrateType is 1 (TencentDB for SQL Server) |
| CvmId | String | No | ID of the source CVM database, which is used when MigrateType is 2 (where CVM creates an SQL Server database) |
| VpcId | String | No | VPC ID of the source CVM database in the format of vpc-6ys9ont9, which is used when MigrateType is 2 (where CVM creates an SQL Server database) |
| SubnetId | String | No | VPC subnet ID of the source CVM database in the format of subnet-h9extioi, which is used when MigrateType is 2 (where CVM creates an SQL Server database) |
| UserName | String | No | Username, which is used when MigrateType is 1 or 2 |
| Password | String | No | Password, which is used when MigrateType is 1 or 2 |
| Ip | String | No | Private IP of the source CVM database, which is used when MigrateType is 2 (where CVM creates an SQL Server database) |
| Port | Integer | No | Port number of the source CVM database, which is used when MigrateType is 2 (where CVM creates an SQL Server database) |
| Url | Array of String | No | Source backup address for offline migration, which is used when MigrateType is 4 or 5 |
| UrlPassword | String | No | Source backup password for offline migration, which is used when MigrateType is 4 or 5 |

## MigrateTarget

Target type of the migration task

Referenced by: CreateMigration, DescribeMigrationDetail, ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceId | String | No | ID of the target instance in the format of mssql-si2823jyl |
| UserName | String | No | Username of the target instance |
| Password | String | No | Password of the target instance |

## MigrateTask

Migration task type

Referenced by: DescribeMigrations.

| Name | Type | Description |
|------|------|-------|
| MigrateId | Integer | Migration task ID |
| MigrateName | String | Migration task name |
| AppId | Integer | ID of the user to which the migration task belongs |
| Region | String | Region of the migration task |
| SourceType | Integer | Type of migration source. 1: TencentDB for SQL Server, 2: SQL Server database created by CVM, 4: SQL Server backup restoration, 5: SQL Server backup restoration (in COS mode) |
| CreateTime | Timestamp | Migration task creation time |
| StartTime | Timestamp | Migration task start time |
| EndTime | Timestamp | Migration task end time |
| Status | Integer | Migration task status (1: initializing, 4: migrating, 5: migration failed, 6: migration succeeded) |
| Message | String | Message |
| CheckFlag | Integer | Whether the migration task has been checked (0: not checked, 1: check succeeded, 2: check failed, 3: checking) |
| Progress | Integer | Migration task progress in % |
| MigrateDetail | [MigrateDetail](#MigrateDetail) | Migration task progress details |

## RegionInfo

Region information

Referenced by: DescribeRegions.

| Name | Type | Description |
|------|------|-------|
| Region | String | Region ID, e.g., ap-guangzhou |
| RegionName | String | Region name |
| RegionId | Integer | Region ID in digits |
| RegionState | String | Purchasability of the current region. UNAVAILABLE: not purchasable, AVAILABLE: purchasable |

## SlowlogInfo

Slow query log 

Referenced by: DescribeSlowlogs.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID of the slow query log |
| StartTime | Timestamp | File generation start time |
| EndTime | Timestamp | File generation end time |
| Size | Integer | File size in KB |
| Count | Integer | Number of logs in the file |
| InternalAddr | String | Download address on the private network |
| ExternalAddr | String | Download address on the public network |

## SpecInfo

Information of purchasable specification for an instance

Referenced by: DescribeProductConfig.

| Name | Type | Description |
|------|------|-------|
| SpecId | Integer | Instance specification ID. You may find the information about   what specifications can be purchased in a specified Availability Zone by referring to SpecId and API DescribeProductConfig  |
| MachineType | String | Model ID |
| MachineTypeName | String | Model name |
| Version | String | Database version information. Valid values: 2008R2 (SQL Server 2008 R2), 2012SP3 (SQL Server 2012), and 2016SP1 (SQL Server 2016 SP1) |
| VersionName | String | Version name corresponding to the "Version" field |
| Memory | Integer | Memory size in GB |
| CPU | Integer | Number of CPU cores |
| MinStorage | Integer | Minimum disk size under this specification in GB |
| MaxStorage | Integer | Maximum disk size under this specification in GB |
| QPS | Integer | QPS of this specification |
| SuitInfo | String | Description of this specification |
| Pid | Integer | Pid of this specification |

## ZoneInfo

AZ information

Referenced by: DescribeZones.

| Name | Type | Description |
|------|------|-------|
| Zone | String | AZ ID in the format of ap-guangzhou-1 (i.e., Guangzhou Zone 1) |
| ZoneName | String | AZ name |
| ZoneId | Integer | AZ ID |
| SpecId | Integer |Instance specification ID. You may find the information about   what specifications can be purchased in a specified Availability Zone by referring to SpecId and API DescribeProductConfig |
| Version | String | Purchasable version for the database under the current AZ and specification in the format of 2008R2 (SQL Server 2008 R2). Value range: 2008R2 (SQL Server 2008 R2), 2012SP3 (SQL Server 2012), and 2016SP1 (SQL Server 2016 SP1) |

