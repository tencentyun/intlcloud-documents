>As TDSQL was formerly known as DCDB, its API keyword in CAM is "dcdb". For more information, see [Product Name Change](https://intl.cloud.tencent.com/document/product/1042/33376).

Resource-level permission can be used to specify which resources a user can manipulate. TencentDB supports certain resource-level permission. This means that for some TencentDB operations, you can control the time when a user is allowed to perform operations (based on mandatory conditions) or to use specified resources. The following table describes the types of resources that can be authorized in TencentDB.

Types of resources that can be authorized in CAM:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- |:-------------- |
| TencentDB instance-related   `qcs::dcdb:$region:$account:instance/*`<br>`qcs::dcdb:$region:$account:instance/$instanceId`

The table below lists the TencentDB API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

> Any TencentDB API operation not listed here does not support resource-level permission. If a TencentDB API operation does not support resource-level permission, you can still authorize a user to perform this operation, but you must specify * for the resource element of the policy statement.

#### The following operations support resource-level permission control

| Operation Name | API Name | Effective in Console After Configuration |
| -------------------- | ------------------------------ | -------------------- |
| Recovering a dedicated instance         | ActiveDedicatedDBInstance      | Yes                  |
| Binding security groups           | AssociateSecurityGroups        | Yes                  |
| Checking IP status           | CheckIpStatus                  | Yes                  |
| Cloning an account             | CloneAccount                   | Yes                  |
| Disabling public network access for an instance       | CloseDBExtranetAccess          | Yes                  |
| Copying account permission         | CopyAccountPrivileges          | Yes                  |
| Creating an account             | CreateAccount                  | Yes                  |
| Creating an instance             | CreateDCDBInstance             | Yes                  |
| Deleting an account             | DeleteAccount                  | Yes                  |
| Querying account permission         | DescribeAccountPrivileges      | Yes                  |
| Querying the account list         | DescribeAccounts               | Yes                  |
| Querying audit logs         | DescribeAuditLogs              | Yes                  |
| Querying audit rule details     | DescribeAuditRuleDetail        | Yes                  |
| Querying the audit rule list     | DescribeAuditRules             | Yes                  |
| Querying audit policies         | DescribeAuditStrategies        | Yes                  |
| Querying the price for batch instance renewal | DescribeBatchDCDBRenewalPrice  | Yes                  |
| Querying instance objects         | DescribeDatabaseObjects        | Yes                  |
| Querying instance database names         | DescribeDatabases              | Yes                  |
| Querying column information of an instance table   | DescribeDatabaseTable          | Yes                  |
| Getting the log list         | DescribeDBLogFiles             | Yes                  |
| Querying monitoring information         | DescribeDBMetrics              | Yes                  |
| Viewing database parameters       | DescribeDBParameters           | Yes                  |
| Querying security group information of an instance   | DescribeDBSecurityGroups       | Yes                  |
| Getting slow log recording details   | DescribeDBSlowLogAnalysis      | Yes                  |
| Getting the slow log list   | DescribeDBSlowLogs             | Yes                  |
| Querying instance sync mode     | DescribeDBSyncMode             | Yes                  |
| Getting instance details     | DescribeDCDBInstanceDetail     | Yes                  |
| Viewing the instance list         | DescribeDCDBInstances          | Yes                  |
| Querying price             | DescribeDCDBPrice              | Yes                  |
| Querying the renewal price of an instance     | DescribeDCDBRenewalPrice       | Yes                  |
| Querying purchasable AZs       | DescribeDCDBSaleInfo           | Yes                  |
| Querying instance shards     | DescribeDCDBShards             | Yes                  |
| Querying the upgrade price of an instance     | DescribeDCDBUpgradePrice       | Yes                  |
| Querying dedicated cluster specification     | DescribeFenceShardSpec         | Yes                  |
| Querying flow status         | DescribeFlow                   | Yes                  |
| Querying the latest DBA check result  | DescribeLatestCloudDBAReport   | Yes                  |
| Viewing backup log settings     | DescribeLogFileRetentionPeriod | Yes                  |
| Querying order information         | DescribeOrders                 | Yes                  |
| Querying projects             | DescribeProjects               | Yes                  |
| Querying security group information of a project   | DescribeProjectSecurityGroups  | Yes                  |
| Querying instance specification         | DescribeShardSpec              | Yes                  |
| Getting SQL logs          | DescribeSqlLogs                | Yes                  |
| Unbinding security groups from Tencent Cloud resources in batches | DisassociateSecurityGroups     | Yes                  |
| Setting account permission         | GrantAccountPrivileges         | Yes                  |
| Initializing instances           | InitDCDBInstances              | Yes                  |
| Isolating a dedicated instance         | IsolateDedicatedDBInstance     | Yes                  |
| Modifying database account remarks   | ModifyAccountDescription       | Yes                  |
| Setting auto-renewal in batches     | ModifyAutoRenewFlag            | Yes                  |
| Renaming an instance         | ModifyDBInstanceName           | Yes                  |
| Modifying security groups bound to a TencentDB instance   | ModifyDBInstanceSecurityGroups | Yes                  |
| Modifying instance project         | ModifyDBInstancesProject       | Yes                  |
| Modifying database parameters       | ModifyDBParameters             | Yes                  |
| Modifying instance sync mode     | ModifyDBSyncMode               | Yes                  |
| Modifying instance network     | ModifyInstanceNetwork          | Yes                  |
| Modifying instance VIP          | ModifyInstanceVip              | Yes                  |
| Modifying backup log settings     | ModifyLogFileRetentionPeriod   | Yes                  |
| Enabling public network access             | OpenDBExtranetAccess           | Yes                  |
| Renewing an instance             | RenewDCDBInstance              | Yes                  |
| Resetting account password         | ResetAccountPassword           | Yes                  |
| Enabling smart DBA          | StartSmartDBA                  | Yes                  |
| Scaling an instance             | UpgradeDCDBInstance            | Yes                  |
| Upgrading a dedicated instance     | UpgradeDedicatedDCDBInstance   | Yes                  |


