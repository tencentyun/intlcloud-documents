
Tencent Cloud Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for MongoDB supports data migration on different versions of MongoDB and in various network scenarios.

| Term | Description |
| -------- | -------------------------------------------------- |
| Source instance | Source instance to be migrated from. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for MongoDB. |
| CVM-based MongoDB instance | MongoDB service deployed on a CVM instance. |
| Public network-based MongoDB instance | MongoDB service deployed on the public network. |

## Migration Support Description
**Supported features**
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync by combining full migration and incremental sync.
- Table migration: migration at the table level is supported.
- Migration availability: automatic retry and checkpoint restart are supported.
- Latency display: latency display is supported for incremental sync.
- Cross-architecture: migration between replica set instance and sharded cluster instance is supported.

**Supported versions**
- DTS supports MongoDB 3.0, 3.2, 3.4, 3.6, and 4.0.
- DTS supports migration from replica set instance to replica set instance, from replica set instance to sharded cluster instance, from sharded cluster instance to replica set instance, and from sharded cluster instance to sharded cluster instance.

**Supported networks**
DTS supports data migration and data sync based on the public network, CVM instances, Direct Connect gateways, VPN gateways, and CCN.

**Supported scenarios**
- Migration to cloud: DTS supports migrating your MongoDB instance in a traditional IDC to TencentDB for MongoDB, moving your businesses to the cloud in an efficient and convenient manner.
- VM-based MongoDB instance migration: DTS supports migrating your MongoDB service created with virtual machines on Tencent Cloud or other clouds to TencentDB for MongoDB.
- Migration of MongoDB data from other cloud vendors: DTS supports migrating MongoDB data from other cloud vendors to TencentDB for MongoDB.
- Migration between instances on Tencent Cloud: DTS supports data migration or real-time sync between instances on Tencent Cloud.

**Notes on migration**
- To ensure migration efficiency, cross-region migration is not supported for CVM-based MongoDB instances.
- To migrate instances over a public network, make sure that the source instance is accessible from the public network.
- Before the migration is initiated, please create a read-only account in the source instance for the migration; otherwise, the verification before migration will fail.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.
- If the MongoDB instance deployed by yourself is single-node, online migration is not supported for it as it has no oplog.

## Migration Directions
1. Log in to the [DTS console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page, select a **Linkage Region**, and click **Buy at 0 USD**.
>?
>- Currently, MongoDB database migration is free of charge.
>- Please select the region with caution as it cannot be changed once the migration task is created.
>
2. On the **Set source and target databases** page, select MongoDB as the source database type, and configure the instance and the corresponding account/password information.
>?Please create a read-only account in the source instance for the migration; otherwise, the verification before migration will fail.
>
![](https://main.qcloudimg.com/raw/5418854efa1cab777d217451f5fed550.png)
3. Test the connectivity between the source and target instances.
![](https://main.qcloudimg.com/raw/d789a0f2053b815f002a289bb3d845e3.png)
4. On the **Set migration options and select migration objects** page, set the migration options and migration objects (you can select specified tables).
![](https://main.qcloudimg.com/raw/a5dc2558be5db94f5121526e1690d72f.png)
5. On the task verification page, complete the verification before migration and click **Start Task**.
6. After the verification is passed, return to the data migration list. After the incremental sync is 100% complete, click **Complete** in the **Operation** column to finish the migration task.
![](https://main.qcloudimg.com/raw/86e30f0eba3671e4272a27bc1ac9ca97.png)

