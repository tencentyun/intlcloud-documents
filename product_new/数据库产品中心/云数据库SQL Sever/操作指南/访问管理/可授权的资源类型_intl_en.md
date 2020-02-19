Resource-level permission can be used to specify which resources a user can manipulate. TencentDB for SQL Server supports certain resource-level permissions. This means that for TencentDB for SQL Server operations that support resource-level permission, you can control the time when a user is allowed to perform operations or to use specified resources. The following table describes the types of resources that can be authorized in CAM.

| Resource Type | Resource Description Method in Authorization Policy |
| :--------------- | :----------------------------------------------------------- |
| TencentDB instance-related resource | `qcs::sqlserver:$region:$account:instance/*`<br>`qcs::sqlserver:$region:$account:instance/$instanceId` |

TencentDB for SQL Server supports resource-level authorization. You can allow a sub-account to have API permissions for specific resources. The table below lists the TencentDB API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. When specifying a resource path, you can use the "*" wildcard in the path.

>?Any TencentDB API operation not listed in the table does not support resource-level permission. For such an operation, you can still authorize a user to perform it, but you must specify `*` as the resource element in the policy statement.

| API Name | Description | Six-segment Example of Resource |
| :---------------------------- | :--------------- |  :----------------------------------------------------------- |
| CreateAccount                 | Creates an account         | ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| CreateBackup                  | Creates a backup         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| CreateDB                      | Creates a database       |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DeleteAccount                 | Deletes an account         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DeleteDB                      | Drops a database       |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeAccounts              | Queries the account list     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeBackups               | Queries the backup list     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDatabaseNames         | Queries database names   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDBInstances           | Queries the instance list     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeDBs                   | Queries the database list   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeInstanceTasks         | Queries instance tasks     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeRollbackTime          | Queries the time range available for rollback   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| DescribeSlowlogs              | Queries the slow log list   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| InquiryPriceRenewDBInstance   | Queries the renewal price of an instance |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| InquiryPriceUpgradeDBInstance | Queries the upgrade price of an instance |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyAccountPrivilege        | Modifies account permissions     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyAccountRemark           | Modifies account remarks     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyBackupStrategy          | Modifies the time for cold backup     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDatabasePrivilege       | Modifies database permissions  |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBInstanceName          | Renames an instance     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBInstanceProject       | Modifies an instance project     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBName                  | Renames a database   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ModifyDBRemark                | Modifies database remarks   |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RenewDBInstance               | Renews an instance        |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| ResetAccountPassword          | Resets an account password     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RestartDBInstance             | Restarts an instance         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RestoreInstance               | Restores a cold backup instance     |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| RollbackInstance              | Rolls back an instance         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| TerminateDBInstance           | Terminates an instance         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
| UpgradeDBInstance             | Upgrades an instance         |  ```qcs::sqlserver:$region:$account:instance/$instanceId```<br>```qcs::sqlserver:$region:$account:instance/*``` |
