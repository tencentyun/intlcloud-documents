Licensed by Microsoft, TencentDB for SQL Server continuously provides the latest features and helps you avoid risks with unauthorized software use. It features out-of-the-box usage, high stability, reliability, and security, high-availability architecture, data security protection, failover in a matter of seconds, enabling you to focus more on application development.

TencentDB for SQL Server operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|-------------|-----------|-------------------------------|
| Immediately completing instance expansion    | sqlserver | CompleteExpansion             |
| Creating account        | sqlserver | CreateAccount                 |
| Creating backup        | sqlserver | CreateBackup                  |
| Creating database       | sqlserver | CreateDB                      |
| Purchasing instance        | sqlserver | CreateDBInstances             |
| Creating migration task      | sqlserver | CreateMigration               |
| Creating publish-subscribe relationship    | sqlserver | CreatePublishSubscribe        |
| Deleting account        | sqlserver | DeleteAccount                 |
| Deleting database       | sqlserver | DeleteDB                      |
| Deleting publish-subscribe relationship    | sqlserver | DeletePublishSubscribe        |
| Querying account list      | sqlserver | DescribeAccounts              |
| Querying backup list      | sqlserver | DescribeBackups               |
| Querying instance list      | sqlserver | DescribeDBInstances           |
| Querying database list     | sqlserver | DescribeDBs                   |
| Querying process status      | sqlserver | DescribeFlowStatus            |
| Querying instance task      | sqlserver | DescribeInstanceTasks         |
| Querying maintainable time window    | sqlserver | DescribeMaintenanceSpan       |
| Querying migration task details    | sqlserver | DescribeMigrationDetail       |
| Querying migration task list    | sqlserver | DescribeMigrations            |
| Querying billing order      | sqlserver | DescribeOrders                |
| Querying sale specification configuration    | sqlserver | DescribeProductConfig         |
| Querying publish-subscribe relationship    | sqlserver | DescribePublishSubscribe      |
| Querying region information      | sqlserver | DescribeRegions               |
| Querying default weight in RO group | sqlserver | DescribeROGroupAutoWeight     |
| Querying RO replica in RO group | sqlserver | DescribeROGroupByRoInstance   |
| Querying RO group details  | sqlserver | DescribeROGroupInfo           |
| Querying RO group list     | sqlserver | DescribeROGroupList           |
| Querying the time range available for rollback     | sqlserver | DescribeRollbackTime          |
| Querying slow log list     | sqlserver | DescribeSlowlogs              |
| Querying AZ information     | sqlserver | DescribeZones                 |
| Querying the price for purchasing instance    | sqlserver | InquiryPriceCreateDBInstances |
| Querying the renewal price of instance    | sqlserver | InquiryPriceRenewDBInstance   |
| Querying the upgrade price of instance    | sqlserver | InquiryPriceUpgradeDBInstance |
| Modifying account permission      | sqlserver | ModifyAccountPrivilege        |
| Modifying account remarks      | sqlserver | ModifyAccountRemark           |
| Modifying the time for cold backup      | sqlserver | ModifyBackupStrategy          |
| Modifying database permission     | sqlserver | ModifyDatabasePrivilege       |
| Modifying instance name      | sqlserver | ModifyDBInstanceName          |
| Modifying instance project      | sqlserver | ModifyDBInstanceProject       |
| Modifying instance renewal flag    | sqlserver | ModifyDBInstanceRenewFlag     |
| Modifying database name     | sqlserver | ModifyDBName                  |
| Modifying database remarks     | sqlserver | ModifyDBRemark                |
| Modifying maintainable time window    | sqlserver | ModifyMaintenanceSpan         |
| Modifying the name of publish-subscribe relationship  | sqlserver | ModifyPublishSubscribeName    |
| Modifying RO group information    | sqlserver | ModifyROGroupInfo             |
| Immediately deactivating instance      | sqlserver | OfflineDBInstance             |
| Moving pay-as-you-go instance into recycle bin | sqlserver | RecoveryPostInstance          |
| Resetting account password      | sqlserver | ResetAccountPassword          |
| Restarting instance        | sqlserver | RestartDBInstance             |
| Restoring cold backup instance      | sqlserver | RestoreInstance               |
| Rolling back instance        | sqlserver | RollbackInstance              |
| Starting migration task      | sqlserver | RunMigration                  |
| Terminating instance        | sqlserver | TerminateDBInstance           |
| Upgrading instance        | sqlserver | UpgradeDBInstance             |
