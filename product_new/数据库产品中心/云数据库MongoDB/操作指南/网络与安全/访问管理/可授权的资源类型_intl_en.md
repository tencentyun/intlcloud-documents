Resource-level permission can be used to specify which resources a user can manipulate. MongoDB supports certain resource-level permission. This means that for MongoDB operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| ------------------------------ | ------------------------------------------------------------ |
| [MongoDB instance](#xiangguan) | `qcs::mongodb:$region::instance/*`<br>`qcs::mongodb:$region:$account:instanceId/$instanceId` |

The table below lists the MongoDB API operations which currently support resource-level permission control as well as the resources supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

<span id="xiangguan"></span>
#### MongoDB instance

| API Operation | Resource Path |
| ------------------------- | ------------------------------------------------------------ |
| BackupDBInstance          | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| CreateAccountUser         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| CreateDBInstance          | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| CreateDBInstanceHour      | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DeleteAccountUser         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeAccountUsers      | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeBackupAccess      | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeBackupRules       | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeClientConnections | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeDBBackups         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeDBInstances       | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeInstanceDB        | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeInstanceTaskInfo  | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeSlowLog           | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeSlowLogPattern    | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| DescribeSpecInfo          | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| ExchangeInstance          | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| IsolateDBInstance         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| ModifyDBInstanceSpec      | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| OfflineIsolatedDBInstance | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| RemoveCloneInstance       | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| RenameInstance            | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| RenewInstance             | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| ResizeOplog               | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| RestartInstance           | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| RestoreDBInstance         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetAccountUserPrivilege   | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetAutoRenew              | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetBackupRules            | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetInstanceFormal         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetInstanceMaintenance    | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetPassword               | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| SetReadOnlyToNormal       | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| TerminateDBInstance       | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| TerminateDBInstanceHour   | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| UpgradeDBInstance         | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
| UpgradeDBInstanceHour     | `qcs::mongodb:$region:$account:instanceId/*`    `qcs::mongodb:$region:$account:instanceId/$instanceId` |
