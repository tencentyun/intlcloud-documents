Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs.

DTS operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|--------------|------|------------------------------|
| Completing data migration       | dts  | CompleteMigrateJob           |
| Configuring data comparison task     | dts  | ConfigDataComparisonJob      |
| Creating `AccessKey`  | dts  | CreateAccessKey              |
| Creating migration check task     | dts  | CreateMigrateCheckJob        |
| Creating data migration task     | dts  | CreateMigrateJob             |
| Creating data subscription       | dts  | CreateSubscribe              |
| Deleting migration task       | dts  | DeleteMigrateJob             |
| Querying access key | dts  | DescribeAccessKeys           |
| Querying data comparison result     | dts  | DescribeDataComparisonResult |
| Querying check task result     | dts  | DescribeMigrateCheckJob      |
| Viewing migration task       | dts  | DescribeMigrateJobs          |
| Viewing migration task details       | dts  | DescribeMigrateObject        |
| Querying subscription configuration       | dts  | DescribeSubscribeConf        |
| Querying whether the subscription instance can be returned | dts  | DescribeSubscribeReturnable  |
| Querying subscription instance list     | dts  | DescribeSubscribes           |
| Isolating subscription instance       | dts  | IsolateSubscribe             |
| Modifying migration task       | dts  | ModifyMigrateJob             |
| Modifying migration name       | dts  | ModifyMigrateName            |
| Modifying the consumption time point of subscription channel | dts  | ModifySubscribeConsumeTime   |
| Modifying subscription name       | dts  | ModifySubscribeName          |
| Modifying data subscription object     | dts  | ModifySubscribeObjects       |
| Modifying subscription service address     | dts  | ModifySubscribeVipVport      |
| Deactivating isolated instance     | dts  | OfflineIsolatedSubscribe     |
| Resetting data subscription channel     | dts  | ResetSubscribe               |
| Starting migration task       | dts  | StartMigrateJob              |
| Canceling migration task       | dts  | StopMigrateJob               |
