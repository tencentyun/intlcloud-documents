TencentDB for MySQL provides secure, reliable, and easy-to-maintain database services based on MySQL, the most popular open-source database in the world. It enables you to implement database deployment and auto scaling within minutes, which is not only cost-effective, but also stable, reliable, and easy to maintain. As a complete database solution with various features such as backup and restoration, monitoring, disaster recovery, fast scaling, and data transfer, it simplifies your database OPS and allows you to focus more on business development.

TencentDB for MySQL operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|--------------------|------|--------------------------------|
| Adding maintenance window to TencentDB instance     | cdb  | AddTimeWindow                  |
| Binding security groups in batches            | cdb  | AssociateSecurityGroups        |
| Balancing load in RO group          | cdb  | BalanceRoGroupLoad             |
| Canceling task               | cdb  | CancelDBInstanceTask           |
| Disabling public network access for instance           | cdb  | CloseWanService                |
| Creating TencentDB account          | cdb  | CreateAccounts                 |
| Creating TencentDB instance backup           | cdb  | CreateBackup                   |
| Creating data import task           | cdb  | CreateDBImportJob              |
| Creating TencentDB instance           | cdb  | CreateDBInstance               |
| Creating pay-as-you-go TencentDB instance       | cdb  | CreateDBInstanceHour           |
| Creating monitoring template item          | cdb  | CreateMonitorTemplate          |
| Creating parameter template             | cdb  | CreateParamTemplate            |
| Binding independent VIP to RO instance        | cdb  | CreateRoInstanceIp             |
| Deleting TencentDB account          | cdb  | DeleteAccounts                 |
| Deleting TencentDB backup           | cdb  | DeleteBackup                   |
| Deleting monitoring template item          | cdb  | DeleteMonitorTemplate          |
| Deleting parameter template             | cdb  | DeleteParamTemplate            |
| Deleting time window related to TencentDB instance   | cdb  | DeleteTimeWindow               |
| Querying the permission information of TencentDB account      | cdb  | DescribeAccountPrivileges      |
| Querying the information of all TencentDB accounts      | cdb  | DescribeAccounts               |
| Querying the execution result of the async task of TencentDB instance  | cdb  | DescribeAsyncRequestInfo       |
| Querying the configuration information of TencentDB instance backup       | cdb  | DescribeBackupConfig           |
| Querying the list of backup databases          | cdb  | DescribeBackupDatabases        |
| Querying the backup log of TencentDB instance      | cdb  | DescribeBackups                |
| Querying the backup table list of specified database    | cdb  | DescribeBackupTables           |
| Getting the binary log of TencentDB instance     | cdb  | DescribeBinlogs                |
| Querying TencentDB instance database       | cdb  | DescribeDatabases              |
| Querying databases of TencentDB instances in batches     | cdb  | DescribeDatabasesForInstances  |
| Querying import task operation log         | cdb  | DescribeDBImportRecords        |
| Querying the character set of TencentDB instance       | cdb  | DescribeDBInstanceCharset      |
| Querying TencentDB instance configuration        | cdb  | DescribeDBInstanceConfig       |
| Querying the estimated restart time of TencentDB instance    | cdb  | DescribeDBInstanceRebootTime   |
| Querying instance list             | cdb  | DescribeDBInstances            |
| Querying TencentDB instance route          | cdb  | DescribeDBRoutes               |
| Querying the security group information of instance          | cdb  | DescribeDBSecurityGroups       |
| Getting instance switch log           | cdb  | DescribeDBSwitchRecords        |
| Querying the list of default configurable parameters       | cdb  | DescribeDefaultParams          |
| Getting error log details of TencentDB instance    | cdb  | DescribeErrLogInfo             |
| Querying instance parameter modification records        | cdb  | DescribeInstanceParamRecords   |
| Querying the list of configurable parameters for instance       | cdb  | DescribeInstanceParams         |
| Querying monitoring template item          | cdb  | DescribeMonitorTemplate        |
| Querying parameter template details           | cdb  | DescribeParamTemplateInfo      |
| Querying parameter template list           | cdb  | DescribeParamTemplates         |
| Querying the security group information of project          | cdb  | DescribeProjectSecurityGroups  |
| Querying the execution result of async task        | cdb  | DescribeRequestResult          |
| Querying RO group details         | cdb  | DescribeRoGroupInfo            |
| Querying the RO group information of specified source instance      | cdb  | DescribeRoGroups               |
| Querying the time range available for rollback           | cdb  | DescribeRollbackRangeTime      |
| Getting the minimum purchasable specification of read-only instance      | cdb  | DescribeRoMinScale             |
| Getting the slow query analysis log of TencentDB instance   | cdb  | DescribeSlowLogInfo            |
| Getting the slow query log of TencentDB instance     | cdb  | DescribeSlowLogs               |
| Querying the information of supported TencentDB instance permissions    | cdb  | DescribeSupportedPrivileges    |
| Querying database table column           | cdb  | DescribeTableColumns           |
| Querying database table             | cdb  | DescribeTables                 |
| Querying the task list of TencentDB instance      | cdb  | DescribeTasks                  |
| Querying time window related to instance       | cdb  | DescribeTimeWindow             |
| File import: getting uploaded file     | cdb  | DescribeUploadedFiles          |
| Unbinding security groups in batches            | cdb  | DisassociateSecurityGroups     |
| Initializing TencentDB instance          | cdb  | InitDBInstances                |
| Isolating TencentDB instance           | cdb  | IsolateDBInstance              |
| Terminating TencentDB instance execution thread        | cdb  | KillDBProcessByIds             |
| Modifying the remarks of TencentDB instance account    | cdb  | ModifyAccountDescription       |
| Modifying the password of TencentDB instance account      | cdb  | ModifyAccountPassword          |
| Modifying the permission of TencentDB instance account      | cdb  | ModifyAccountPrivileges        |
| Modifying the auto-renewal flag of TencentDB instance    | cdb  | ModifyAutoRenewFlag            |
| Modifying the backup configuration information of TencentDB instance       | cdb  | ModifyBackupConfig             |
| Modifying TencentDB instance name          | cdb  | ModifyDBInstanceName           |
| Modifying the project of TencentDB instance      | cdb  | ModifyDBInstanceProject        |
| Modifying security group bound to instance         | cdb  | ModifyDBInstanceSecurityGroups |
| Modifying the VIP and Vport of TencentDB instance | cdb  | ModifyDBInstanceVipVport       |
| Modifying instance parameter             | cdb  | ModifyInstanceParam            |
| Modifying parameter template             | cdb  | ModifyParamTemplate            |
| Updating RO group information           | cdb  | ModifyRoGroupInfo              |
| Modifying the VIP and Vport of RO group    | cdb  | ModifyRoGroupVipVport          |
| Updating time window related to instance        | cdb  | ModifyTimeWindow               |
| Enabling database instance encryption          | cdb  | OpenDBInstanceEncryption       |
| Enabling TencentDB instance GTID     | cdb  | OpenDBInstanceGTID             |
| Enabling public network access for instance           | cdb  | OpenWanService                 |
| Desolating TencentDB instance          | cdb  | ReleaseIsolatedDBInstances     |
| Restarting TencentDB instance           | cdb  | RestartDBInstances             |
| Viewing MySQL execution thread       | cdb  | ShowProcessList                |
| Starting batch rollback task           | cdb  | StartBatchRollback             |
| Stopping data import task           | cdb  | StopDBImportJob                |
| Switching disaster recovery TencentDB instance to source instance      | cdb  | SwitchDrInstanceToMaster       |
| Upgrading switch VIP            | cdb  | SwitchForUpgrade               |
| Upgrading TencentDB instance           | cdb  | UpgradeDBInstance              |
| Upgrading TencentDB instance version         | cdb  | UpgradeDBInstanceEngineVersion |
