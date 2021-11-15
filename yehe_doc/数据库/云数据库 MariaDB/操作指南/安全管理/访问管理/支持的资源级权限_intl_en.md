>The API keyword in CAM of TencentDB for MariaDB is "mariadb".

Resource-level permission can be used to specify which resources a user can manipulate. TencentDB supports certain resource-level permission. This means that for some TencentDB operations, you can control the time when a user is allowed to perform operations (based on mandatory conditions) or to use specified resources. The following table describes the types of resources that can be authorized in TencentDB.

Types of resources that can be authorized in CAM:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- |:-------------- |
| TencentDB instance-related |  `qcs::mariadb:$region:$account:instance/*`<br>`qcs::mariadb:$region:$account:instance/$instanceId`

The table below lists the TencentDB API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

#### The following operations support resource-level permission control

| Operation Name | API Name | Effective in Console After Configuration |
| ----------------------- | ------------------------------ | -------------------- |
| Recovering dedicated instance         | ActiveDedicatedDBInstance      | Yes                  |
| Binding security group           | AssociateSecurityGroups        | Yes                  |
| Checking IP status           | CheckIpStatus                  | Yes                  |
| Cloning account             | CloneAccount                   | Yes                  |
| Disabling public network address       | CloseDBExtranetAccess          | Yes                  |
| Copying permission                | CopyAccountPrivileges          | Yes                  |
| Creating account             | CreateAccount                  | Yes                  |
| Creating parameter template            | CreateConfigTemplate           | Yes                  |
| Creating instance                | CreateDBInstance               | Yes                  |
| Rolling back instances                | CreateTmpInstances             | Yes                  |
| Deleting account             | DeleteAccount                  | Yes                  |
| Deleting parameter template            | DeleteConfigTemplate           | Yes                  |
| Deleting temp instance            | DeleteTmpInstance              | Yes                  |
| Getting the list of permissions            | DescribeAccountPrivileges      | Yes                  |
| Querying the list of accounts         | DescribeAccounts               | Yes                  |
| Querying audit logs         | DescribeAuditLogs              | Yes                  |
| Querying audit rule details     | DescribeAuditRuleDetail        | Yes                  |
| Querying list of audit rules     | DescribeAuditRules             | Yes                  |
| Querying audit policies         | DescribeAuditStrategies        | Yes                  |
| Getting custom backup time      | DescribeBackupTime             | Yes                  |
| Querying price for batch instance renewal | DescribeBatchRenewalPrice      | Yes                  |
| Querying binlog time          | DescribeBinlogTime             | Yes                  |
| Querying parameter configuration history        | DescribeConfigHistories        | Yes                  |
| Querying parameter template            | DescribeConfigTemplate         | Yes                  |
| Querying the list of parameter templates        | DescribeConfigTemplates        | Yes                  |
| Querying instance objects         | DescribeDatabaseObjects        | Yes                  |
| Querying instance database names         | DescribeDatabases              | Yes                  |
| Querying the column information of instance table   | DescribeDatabaseTable          | Yes                  |
| Querying monitoring information details         | DescribeDBDetailMetrics        | Yes                  |
| Querying the key information of instance        | DescribeDBEncryptAttributes    | Yes                  |
| Querying instance details            | DescribeDBInstanceDetail       | Yes                  |
| Querying the HA information of instance   | DescribeDBInstanceHAInfo       | Yes                  |
| Querying instance specification              |DescribeDBInstanceSpecs           | Yes |
| Querying the list of instances            | DescribeDBInstances            | Yes                  |
| Getting the list of logs         | DescribeDBLogFiles             | Yes                  |
| Querying monitoring information         | DescribeDBMetrics              | Yes                  |
| Viewing database parameters       | DescribeDBParameters           | Yes                  |
| Viewing instance performance data        | DescribeDBPerformance          | Yes                  |
| Viewing instance performance data details    | DescribeDBPerformanceDetails   | Yes                  |
| Viewing instance resource usage    | DescribeDBResourceUsage        | Yes                  |
| Viewing instance resource usage details   | DescribeDBResourceUsageDetails | Yes                  |
| Querying the security group information of instance   | DescribeDBSecurityGroups       | Yes                  |
| Getting slow query log details   | DescribeDBSlowLogAnalysis      | Yes                  |
| Querying the list of slow logs   | DescribeDBSlowLogs             | Yes                  |
| Querying instance sync mode     | DescribeDBSyncMode             | Yes                  |
| Querying temp instances            | DescribeDBTmpInstances         | Yes                  |
| Querying default parameter template            | DescribeDefaultConfigTemplate         | Yes                  |
| Querying dedicated cluster specification     | DescribeFenceDBInstanceSpecs         | Yes                  |
| Querying flow status         | DescribeFlow                   | Yes                  |
| Querying the proxy configuration of instance        | DescribeInstanceProxyConfig    | Yes                  |
| Querying the SSL status of instance         | DescribeInstanceSSLAttributes  | Yes                  |
| Querying latest DBA check result  | DescribeLatestCloudDBAReport   | Yes                  |
| Viewing backup log settings     | DescribeLogFileRetentionPeriod | Yes                  |
| Querying order information         | DescribeOrders                 | Yes                  |
| Querying price             | DescribePrice              | Yes                  |
| Querying projects             | DescribeProjects               | Yes                  |
| Querying the security group information of project   | DescribeProjectSecurityGroups  | Yes                  |
| Querying the renewal price of instance        | DescribeRenewalPrice           | Yes                  |
| Querying purchasable AZs          | DescribeSaleInfo               | Yes                  |
| Getting SQL logs          | DescribeSqlLogs                | Yes                  |
| Querying the list of sync tasks        | DescribeSyncTasks              | Yes                  |
| Querying the upgrade price of instance        | DescribeUpgradePrice           | Yes                  |
| Querying the information of user tasks        | DescribeUserTasks              | Yes                  |
| Unbinding security groups from Tencent Cloud resources in batches | DisassociateSecurityGroups     | Yes                  |
| Setting permissions                | GrantAccountPrivileges         | Yes                  |
| Initializing instances           | InitDBInstances              | Yes                  |
| Isolating dedicated instance         | IsolateDedicatedDBInstance     | Yes                  |
| Modifying account remarks            | ModifyAccountDescription       | Yes                  |
| Setting auto-renewal in batches     | ModifyAutoRenewFlag            | Yes                  |
| Setting custom backup time      | ModifyBackupTime               | Yes                  |
| Modifying parameter template            | ModifyConfigTemplate           | Yes                  |
| Modifying instance encryption information        | ModifyDBEncryptAttributes      | Yes                  |
| Renaming instance         | ModifyDBInstanceName           | Yes                  |
| Modifying security groups bound to TencentDB instance   | ModifyDBInstanceSecurityGroups | Yes                  |
| Modifying instance project         | ModifyDBInstancesProject       | Yes                  |
| Modifying database parameters       | ModifyDBParameters             | Yes                  |
| Modifying instance sync mode     | ModifyDBSyncMode               | Yes                  |
| Modifying instance network            | ModifyInstanceNetwork          | Yes                  |
| Modifying remarks            | ModifyInstanceRemark           | Yes                  |
| Modifying SSL information             | ModifyInstanceSSLAttributes    | Yes                  |
| Modifying instance VIP          | ModifyInstanceVip              | Yes                  |
| Modifying backup log settings     | ModifyLogFileRetentionPeriod   | Yes                  |
| Enabling public network address            | OpenDBExtranetAccess           | Yes                  |
| Renewing instance             | RenewDBInstance              | Yes                  |
| Resetting account password         | ResetAccountPassword           | Yes                  |
| Enabling smart DBA          | StartSmartDBA                  | Yes                  |
| Switching instance HA              | SwitchDBInstanceHA             | Yes                  |
| Replacing original instance with temp instance      | SwitchRollbackInstance         | Yes                  |
| Terminating dedicated instance            | TerminateDedicatedDBInstance   | Yes                  |
| Scaling up instance                | UpgradeDBInstance              | Yes                  |
| Upgrading dedicated instance            | UpgradeDedicatedDBInstance     | Yes                  |
