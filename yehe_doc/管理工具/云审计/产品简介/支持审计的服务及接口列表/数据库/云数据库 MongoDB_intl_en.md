TencentDB for MongoDB is a high-performance distributed data storage service created by Tencent Cloud based on MongoDB, an open-source non-relational database. It is fully compatible with the MongoDB protocol and applicable to various non-relational database-oriented scenarios.

TencentDB for MongoDB operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|---------------|---------|-----------------------------|
| Assigning project          | mongodb | AssignProject               |
| Manually back up instance        | mongodb | BackupDBInstance            |
| Creating user          | mongodb | CreateAccountUser           |
| Creating instance          | mongodb | CreateDBInstance            |
| Creating pay-as-you-go instance      | mongodb | CreateDBInstanceHour        |
| Deleting account          | mongodb | DeleteAccountUser           |
| Querying user          | mongodb | DescribeAccountUsers        |
| Getting backup download permission      | mongodb | DescribeBackupAccess        |
| Querying backup rule        | mongodb | DescribeBackupRules         |
| Pulling instance list        | mongodb | DescribeDBInstances         |
| Querying instance rollback list      | mongodb | DescribeInstanceCollections |
| Querying oplog information     | mongodb | DescribeOplogInfo           |
| Querying latency between primary and secondary read-only instances    | mongodb | DescribeReadonlyDelay       |
| Isolating TencentDB instance      | mongodb | IsolateDBInstance           |
| Modifying the configuration of TencentDB instance    | mongodb | ModifyDBInstanceSpec        |
| Deactivating isolated TencentDB instance | mongodb | OfflineIsolatedDBInstance   |
| Deleting temp instance        | mongodb | RemoveCloneInstance         |
| Renaming instance         | mongodb | RenameInstance              |
| Renewing instance          | mongodb | RenewInstance               |
| Adjusting instance oplog size   | mongodb | ResizeOplog                 |
| Restarting instance          | mongodb | RestartInstance             |
| Rolling back database instance       | mongodb | RestoreDBInstance           |
| Setting user permission        | mongodb | SetAccountUserPrivilege     |
| Setting auto-renewal        | mongodb | SetAutoRenew                |
| Setting auto-renewal rule      | mongodb | SetBackupRules              |
| Transforming temp instance to formal instance        | mongodb | SetInstanceFormal           |
| Setting instance maintenance window     | mongodb | SetInstanceMaintenance      |
| Setting password          | mongodb | SetPassword                 |
| Setting read-only instance as formal instance   | mongodb | SetReadonlyToNormal         |
| Terminating pay-as-you-go instance      | mongodb | TerminateDBInstance         |
| Upgrading instance          | mongodb | UpgradeDBInstance           |
