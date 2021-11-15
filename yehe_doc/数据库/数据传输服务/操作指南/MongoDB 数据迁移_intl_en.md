Tencent Cloud Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for MongoDB supports data migration on different versions of MongoDB and in various network scenarios.

| Term | Description |
| -------- | -------------------------------------------------- |
| Source instance | Source instance to be migrated from. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for MongoDB. |
| CVM-created instance | MongoDB service deployed on a CVM instance. |
| Public network-created instance | MongoDB service deployed on the public network. |

## Migration Support Description
**Supported features**
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync by combining full migration and incremental sync.
- Table migration: DTS supports table migration.
- Migration availability: DTS supports auto-retry and checkpoint restart.
- Latency monitoring: DTS displays the latency of incremental sync in the console.

**Supported versions**
- DTS supports MongoDB 3.0, 3.2, 3.4, 3.6, and 4.0.
- Currently, DTS supports only MongoDB replica sets but not sharded clusters.

**Supported networks**
DTS supports data migration and data sync across a public network, CVM-created instances, Direct Connect gateways, VPN gateways, and CCN.

**Supported scenarios**
- Migration to cloud: DTS supports migrating your MongoDB instance in a traditional IDC to TencentDB for MongoDB, moving your businesses to the cloud in an efficient and convenient manner.
- Self-built service migration: DTS supports migrating your MongoDB service created with virtual machines in Tencent Cloud or other clouds to TencentDB for MongoDB.
- Migration of MongoDB data from other cloud vendors: DTS supports migrating MongoDB data from other cloud vendors to TencentDB for MongoDB.
- Migration between instances on Tencent Cloud: DTS supports data migration or real-time sync between instances on Tencent Cloud.

**Notes on migration**
- To ensure migration efficiency, cross-region migration is not supported for self-built instances on CVM.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- Before migration, please create a read-only account for the source instance; otherwise, the migration verification will fail.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.
- Online migration is not supported for self-built single-node instances as they have no oplog.

## Migration Directions
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page, select a **Linkage Region**, and click **Buy at 0 USD**.
>?
>- Currently, MongoDB database migration is free of charge.
>- Please select the region with caution as it cannot be changed once the migration task is created.
>
2. On the "Set source and target databases" page, select MongoDB as the source database type, and specify instance and account information.
>?Before migration, please create a read-only account for the source instance; otherwise, the migration verification will fail.
>

3. Test the connectivity between the source and target instances.

4. On the "Set migration options and select migration objects" page, set migration options and select migration objects (you can select some tables).

5. On the "Verify task" page, verify the migration task and click **Start Task**.

6. After the verification is passed, return to the data migration list. After the incremental sync is 100% complete, click **Complete** in the "Operation" column to finish the migration task.




