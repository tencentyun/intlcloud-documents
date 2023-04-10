
Resource-level permission can be used to specify which resources a user can manipulate. TencentDB supports certain resource-level permissions. This means that for TencentDB operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- |:-------------- |
| TencentDB instance-related |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`

The table below lists the TencentDB API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. You can use the `*` wildcard in a resource path when defining it.

## List of APIs supporting resource-level authorization
| API | Resource Path |
|:---------|:-------------|
| AddTimeWindow| `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| AssociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CloseWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| CreateDBImportJob|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteBackup|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DeleteTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeAccounts|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupDownloadDbTableCode|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBackupTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeBinlogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabases|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBImportRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceCharset|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBInstanceRebootTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSwitchRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDBSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParamRecords|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeInstanceParams|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRoGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeRollbackRangeTime|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSlowLogs|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeSupportedPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeDatabasesForInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeMonitorData |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DescribeTableColumns |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DropDatabaseTables|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| InitDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| IsolateDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountDescription|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPassword|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAccountPrivileges|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyAutoRenewFlag|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupConfig|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyBackupInfo|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceName|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceProject|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceVipVport|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyInstanceParam|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyDBInstanceModes|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyTimeWindow|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ModifyProtectMode |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OfflineDBInstances |  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenDBInstanceGTID|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| OpenWanService|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| ReleaseIsolatedDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| RestartDBInstances|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| StartBatchRollback|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SubmitBatchOperation|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchDrInstanceToMaster|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| SwitchForUpgrade|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| DisassociateSecurityGroups|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstance|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 
| UpgradeDBInstanceEngineVersion|  `qcs::cdb:$region:$account:instanceId/*`<br>`qcs::cdb:$region:$account:instanceId/$instanceId`| 

## List of APIs not supporting resource-level authorization
For TencentDB API operations that don't support resource-level authorization, you can still authorize a user to perform them, but you must specify `*` as the resource element in the policy statement.

| API | Description |
| ----------------------------- | ---------------------------- |
| CreateDBInstance              | Creates a monthly subscribed TencentDB instance |
| CreateDBInstanceHour          | Creates a pay-as-you-go TencentDB instance |
| CreateParamTemplate           | Creates a parameter template               |
| DeleteParamTemplate           | Deletes a monitoring template item           |
| DescribeProjectSecurityGroups | Queries the security group information of a project            |
| DescribeDefaultParams         | Queries the list of default configurable parameters     |
| DescribeParamTemplateInfo     | Queries the details of a parameter template            |
| DescribeParamTemplates        | Queries the list of parameter templates             |
| DescribeAsyncRequestInfo      | Queries the execution result of an async task       |
| DescribeTasks                 | Queries the list of tasks for a TencentDB instance     |
| DescribeUploadedFiles         | Queries the list of imported SQL files          |
| ModifyParamTemplate           | Modifies a parameter template                 |
| RenewDBInstance               | Renews a TencentDB instance             |
| StopDBImportJob               | Stops a data import task             |
| DescribleRoMinScale           | Queries the minimum specification supported by a read-only instance          |
| DescribeRequestResult           | Queries the details of a task      |
| DescribeRoMinScale           | Queries the minimum specification for read-only instance purchase or upgrade          |

