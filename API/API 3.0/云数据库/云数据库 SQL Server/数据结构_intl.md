## AccountCreateInfo

Information of account creation

It is referenced by the API CreateAccount.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | User name of instance |
| Password | String | Yes | Password of instance |
| DBPrivileges | Array of [DBPrivilege](#DBPrivilege) | No | List of database permissions |
| Remark | String | No | Remarks of account |

## AccountDetail

Account details

It is referenced by the API DescribeAccounts.

| Name | Type | Description |
|------|------|-------|
| Name | String | Account name |
| Remark | String | Remarks of account |
| CreateTime | Timestamp | Creation time of account |
| Status | Integer | Account status. 1: Creating; 2: Normal; 3: Modifying; 4: Resetting password; -1: Deleting |
| UpdateTime | Timestamp | The time when the account was updated |
| PassTime | Timestamp | The time when the password was updated |
| InternalStatus | String | Internal status of account. It defaults to "enable". |
| Dbs | Array of [DBPrivilege](#DBPrivilege) | Read and write permissions of the account for the database |

## AccountPassword

Account password of instance

It is referenced by the API ResetAccountPassword.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | User name |
| Password | String | Yes | Password |

## AccountPrivilege

Account permissions for the database (set this when creating the database).

It is referenced by the APIs CreateDB and DescribeDBs.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | User name of database |
| Privilege | String | Yes | Permissions for the database. ReadWrite indicates both read and write operations are allowed, and ReadOnly indicates only read operation is allowed. |

## AccountPrivilegeModifyInfo

Information of modification of database account permissions

It is referenced by the API ModifyAccountPrivilege.

| Name | Type | Required | Description |
|------|------|----------|------|
| UserName | String | Yes | User name of database |
| DBPrivileges | Array of [DBPrivilegeModifyInfo](#DBPrivilegeModifyInfo) | Yes | Information of modification of account permissions |

## AccountRemark

Remarks of account

It is referenced by the API ModifyAccountRemark.

| Name | Type | Description |
|------|------|-------|
| UserName | String | Account name |
| Remark | String | New remarks of account |

## Backup

Details of backup file

It is referenced by the API DescribeBackups.

| Name | Type | Description |
|------|------|-------|
| FileName | String | File name |
| Size | Integer | File size (in KB) |
| StartTime | Timestamp | Start time of backup |
| EndTime | Timestamp | End time of backup |
| InternalAddr | String | Download address in private network |
| ExternalAddr | String | Download address in public network |
| Id | Integer | Unique ID of backup file. This field is used by the API RestoreInstance. |
| Status | Integer | Backup file status (0: Creating; 1: Successful; 2: Failed. |
| DBs | Array of String | List of databases in case of multi-database backup |
| Strategy | Integer | Backup policy (0: Instance backup; 1: Multi-database backup |
| BackupWay | Integer | Backup method. 0: Scheduled backup; 1: Manual temporary backup |

## DBCreateInfo

Information of database creation

It is referenced by the API CreateDB.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Charset | String | Yes | Character set. Supported values include: Chinese_PRC_CI_AS, Chinese_PRC_CS_AS, Chinese_PRC_BIN, Chinese_Taiwan_Stroke_CI_AS, SQL_Latin1_General_CP1_CI_AS, and SQL_Latin1_General_CP1_CS_AS. It defaults to Chinese_PRC_CI_AS if left empty. |
| Accounts | Array of [AccountPrivilege](#AccountPrivilege) | Yes | Account permissions for the database |
| Remark | String | Yes | Remarks |

## DBDetail

Database information

It is referenced by the API DescribeDBs.

| Name | Type | Description |
|------|------|-------|
| Name | String | Instance ID |
| Charset | String | Character set |
| Remark | String | Remarks |
| CreateTime | Timestamp | Creation time of database |
| Status | Integer | Database status. 1: Creating; 2: Running; 3: Modifying; -1: Deleting. |
| Accounts | Array of [AccountPrivilege](#AccountPrivilege) | Account permissions for the database |
| InternalStatus | String | Internal status. ONLINE indicates "running". |

## DBInstance

Instance details

It is referenced by the API DescribeDBInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| Name | String | Instance name |
| ProjectId | Integer | ID of project to which the instance belongs |
| RegionId | Integer | ID of the region to which the instance belongs |
| ZoneId | Integer | ID of the availability zone to which the instance belongs |
| VpcId | Integer | ID of the VPC to which the instance belongs. It is 0 in case of basic network. |
| SubnetId | Integer | ID of the VPC subnet to which the instance belongs. It is 0 in case of basic network. |
| Status | Integer | Instance status. Supported values: <li>1: In application;</li> <li>2: In operation;</li> <li>3: In restricted operation (switching between master and salve);</li> <li>4: Isolated; </li><li>5: Reclaiming;</li> <li>6: Reclaimed; </li><li>7: Task is running (backing up, rolling back, etc.) </li> <li>8: Deactivated;</li> <li>9: Expanding capacity;</li> <li>10: Migrating; </li><li>11: Read only; </li><li>12: Restarting</li> |
| Vip | String | Instance's access IP |
| Vport | Integer | Instance's access port |
| CreateTime | Timestamp | Creation time of instance |
| UpdateTime | Timestamp | The last update time of instance |
| StartTime | Timestamp | Start time of billing period for the instance |
| EndTime | Timestamp | End time of billing period for the instance |
| IsolateTime | Timestamp | The time when the instance was isolated |
| Memory | Integer | Memory capacity of the instance (in GB) |
| UsedStorage | Integer | Storage used by the instance (in GB) |
| Storage | Integer | Storage of the instance (in GB) |
| VersionName | String | Instance version |
| RenewFlag | Integer | Instance renewal flag. 0: Normal renewal; 1: Auto renewal; 2: No renewal upon expiration. |
| Model | Integer | High availability mode. 1: Dual. 2: Standalone |
| Region | String | Region name, e.g. ap-guangzhou |
| Zone | String | Name of the availability zone to which the instance belongs, e.g. ap-guangzhou-1 |
| BackupTime | String | Backup time |

## DBPrivilege

The account permissions for the database

It is referenced by the APIs CreateAccount and DescribeAccounts.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Privilege | String | Yes | Permissions for the database. ReadWrite indicates both read and write operations are allowed, and ReadOnly indicates only read operation is allowed. |

## DBPrivilegeModifyInfo

Information of modification of database permissions

It is referenced by the API ModifyAccountPrivilege.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | Yes | Database name |
| Privilege | String | Yes | Information of modification of permissions. ReadWrite indicates both read and write operations are allowed, and ReadOnly indicates only read operation is allowed, and Delete indicates the deletion of the account permissions for the database. |

## DBRemark

Remarks of the database.

It is referenced by the API ModifyDBRemark.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Database name |
| Remark | String | Yes | Remarks |

## DbRollbackTimeInfo

Rollback time range available for the database

It is referenced by the API DescribeRollbackTime.

| Name | Type | Description |
|------|------|-------|
| DBName | String | Database name |
| StartTime | Timestamp | Start time of available rollback time range |
| EndTime | Timestamp | End time of available rollback time range |

## DealInfo

Order information

It is referenced by the API DescribeOrders.

| Name | Type | Description |
|------|------|-------|
| DealName | String | Order name |
| Count | Integer | Quantity of goods |
| FlowId | Integer | Associated process ID, which can be used to query the process execution status |
| InstanceIdSet | Array of String | This filed is required only for the order for which an instance is created, and indicates the ID of the created instance. |
| OwnerUin | String | Account |

## InstanceDBDetail

Database information of instance

It is referenced by the API DescribeDBs.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | Instance ID |
| DBDetails | Array of [DBDetail](#DBDetail) | List of database information |

## InstanceRenewInfo

Information of instance renewal status

It is referenced by the API ModifyDBInstanceRenewFlag.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceId | String | Yes | Instance ID, such as mssql-j8kv137v |
| RenewFlag | Integer | Yes | Instance renewal flag. 0: Normal renewal; 1: Auto renewal; 2: No renewal upon expiration. |

## MigrateDB

List of the databases to be migrated

It is referenced by the APIs CreateMigration, DescribeMigrationDetail and ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| DBName | String | No | Name of the database to be migrated |

## MigrateDetail

Details of the migration progress

It is referenced by the API DescribeMigrations.

| Name | Type | Description |
|------|------|-------|
| StepName | String | Name of the current step |
| Progress | Integer | Progress of current step (%) |

## MigrateSource

Source type of migration task

It is referenced by the APIs CreateMigration, DescribeMigrationDetail and ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceId | String | No | ID of the source instance in the migration, such as mssql-si2823jyl. It is used when MigrateType=1 (CDB for SQLServers). |
| CvmId | String | No | ID of the source CVM in the migration. It is used when MigrateType=2 (Self-built SQLServer database on CVM). |
| VpcId | String | No | ID of the VPC to which the source CVM in the migration belongs, such as vpc-6ys9ont9. It is used when MigrateType=2 (Self-built SQLServer database on CVM). |
| SubnetId | String | No | Subnet ID under the VPC of the source CVM in the migration, such as subnet-h9extioi. It is used when MigrateType=2 (Self-built SQLServer database on CVM). |
| UserName | String | No | User name. It is used when MigrateType=1 or MigrateType=2. |
| Password | String | No | Password. It is used when MigrateType=1 or MigrateType=2. |
| Ip | String | No | Private IP of the self-built database on the source CVM in the migration. It is used when MigrateType=2 (Self-built SQLServer database on CVM). |
| Port | Integer | No | Port number of the self-built database on the source CVM in the migration. It is used when MigrateType=2 (Self-built SQLServer database on CVM). |
| Url | Array of String | No | Source backup address for offline migration. It is used when MigrateType=4 or MigrateType=5. |
| UrlPassword | String | No | Source backup password for offline migration. It is used when MigrateType=4 or MigrateType=5. |

## MigrateTarget

Destination type of the migration task

It is referenced by the APIs CreateMigration, DescribeMigrationDetail and ModifyMigration.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceId | String | No | ID of the destination instance in the migration, such as mssql-si2823jyl. |
| UserName | String | No | User name of the destination instance in the migration |
| Password | String | No | Password of the destination instance in the migration |

## MigrateTask

Query the migration task list (Type)

It is referenced by the API DescribeMigrations.

| Name | Type | Description |
|------|------|-------|
| MigrateId | Integer | Migration task ID |
| MigrateName | String | Migration task name |
| AppId | Integer | User ID of the migration task |
| Region | String | Region of the migration task |
| SourceType | Integer | Type of the migration source. 1: CDB for SQLServer; 2: Self-built SQLServer database on CVM; 4: SQLServer backup and restoration; 5: SQLServer backup and restoration (via COS). |
| CreateTime | Timestamp | Creation time of the migration task |
| StartTime | Timestamp | Start time of the migration task |
| EndTime | Timestamp | End time of the migration task |
| Status | Integer | Status of migration task. 1: Initializing; 4: Migrating; 5: Failed; 6: Successful. |
| Message | String | Message |
| CheckFlag | Integer | Indicates whether the migration task has been checked. 0: Not checked; 1: Checked successfully; 2: Check failed; 3: Checking |
| Progress | Integer | Progress of migration task (%) |
| MigrateDetail | [MigrateDetail](#MigrateDetail) | Details of migration task progress |

## RegionInfo

Region information

It is referenced by the API DescribeRegions.

| Name | Type | Description |
|------|------|-------|
| Region | String | Region ID, such as ap-guanghou |
| RegionName | String | Region name |
| RegionId | Integer | Region number |
| RegionState | String | Indicates whether the instance is available in the region. Supported values include UNAVAILABLE and AVAILABLE. |

## SlowlogInfo

Information of slow log file

It is referenced by the API DescribeSlowlogs.

| Name | Type | Description |
|------|------|-------|
| Id | Integer | Unique ID of slow log file |
| StartTime | Timestamp | Start time of file generation |
| EndTime | Timestamp | End time of file generation |
| Size | Integer | File size (in KB) |
| Count | Integer | Number of log entries in the log file |
| InternalAddr | String | Download address in private network |
| ExternalAddr | String | Download address in public network |

## SpecInfo

Available specifications of the instance

It is referenced by the API DescribeProductConfig.

| Name | Type | Description |
|------|------|-------|
| SpecId | Integer | Instance specification ID. You can use the SpecId returned by DescribeZones with the information of available specifications returned by DescribeProductConfig to learn which instance specifications are available in an availability zone. |
| MachineType | String | Model ID |
| MachineTypeName | String | Model name |
| Version | String | Database version. Supported values include 2008R2 (SQL Server 2008 R2), 2012SP3 (SQL Server 2012) and 2016SP1 (SQL Server 2016 SP1). |
| VersionName | String | Version name corresponding to the Version field. |
| Memory | Integer | Memory capacity (in GB) |
| CPU | Integer | Number of CPU cores |
| MinStorage | Integer | The minimum disk capacity under this specification (in GB) |
| MaxStorage | Integer | The maximum disk capacity under this specification (in GB) |
| QPS | Integer | QPS corresponding to this specification |
| SuitInfo | String | Description of this specification |
| Pid | Integer | Pid of this specification |

## ZoneInfo

Information of availability zone

It is referenced by the API DescribeZones.

| Name | Type | Description |
|------|------|-------|
| Zone | String | Availability zone ID, such as ap-guangzhou-1 (Guangzhou Zone 1) |
| ZoneName | String | Availability zone name |
| ZoneId | Integer | Availability zone number |
| SpecId | Integer | ID of the specification available in this availability zone. You can use the SpecId with the data returned by the API DescribeProductConfig to learn the information of the specification available in this availability zone. |
| Version | String | Database version available under the current specification in this availability zone. Supported values include 2008R2 (SQL Server 2008 R2), 2012SP3 (SQL Server 2012) and 2016SP1 (SQL Server 2016 SP1). |


