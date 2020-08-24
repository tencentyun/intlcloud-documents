Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for MongoDB supports data migration on different versions of MongoDB and in multiple network scenarios.

| Term | Description |
| -------- | -------------------------------------------------- |
| Source instance | Source instance to be migrated. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for MongoDB. |
| CVM-based self-created database | MongoDB service deployed on a CVM instance. |
| Public network-based self-created database | MongoDB service deployed on the public network. |

## Migration Compatibility
**Supported features**
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync by combining full migration and incremental sync.
- Table migration: migration at the table level is supported.
- Migration availability: automatic retry and checkpoint restart are supported.
- Latency display: latency display is supported for incremental sync.

**Supported versions**
- DTS supports MongoDB 3.0, 3.2, 3.4, 3.6, and 4.0.
- Currently, DTS supports only MongoDB replica sets but not sharded clusters.

**Supported networks**
DTS supports data migration and data sync in common scenarios, such as public network-based, CVM-based self-created, Direct Connect-based, VPN-based, and CCN-based databases.

**Supported scenarios**
- Cloudification migration: DTS supports migrating your MongoDB instance in a traditional IDC to TencentDB for MongoDB, moving your businesses to the cloud in an efficient and convenient manner.
- Cloud-based self-created service migration: DTS supports migrating your MongoDB service created with a virtual machine in Tencent Cloud or other clouds to TencentDB for MongoDB.
- Migration of MongoDB data from other cloud vendors: DTS supports migrating MongoDB data from other cloud vendors to TencentDB for MongoDB.
- Migration between cloud instances: DTS supports data migration or real-time sync between cloud instances.

**Notes on migration**
- To ensure migration efficiency, cross-region migration of CVM-based self-created instances is not supported.
- To migrate instances over the public network, make sure that the source instance is accessible from the public network.
- Before the migration is initiated, please create a read-only account in the source instance for the migration; otherwise, the verification before migration will fail.
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.
- Online migration is not supported for self-created single-node instances as they have no oplogs.

## Migration Directions
1. Log in to the [DTS Console](https://console.cloud.tencent.com/dts) and click **Create Migration Task** on the data migration page. Select the corresponding region in **Linkage Region**, and click **Buy at 0 USD**.
>?
>- Currently, MongoDB data migration is free of charge.
>- Please select the region with caution as it cannot be changed once the migration task is created.
>
2. On the "Set source and target databases" page, select MongoDB as the source database type, and configure the instance and the corresponding account/password information.
>?Please create a read-only account in the source instance for the migration; otherwise, the verification before migration will fail.
>
![](https://main.qcloudimg.com/raw/5418854efa1cab777d217451f5fed550.png)
3. Test the connectivity between the source and target instances.

  ![](https://main.qcloudimg.com/raw/d789a0f2053b815f002a289bb3d845e3.png)

4. On the "Set migration options and select migration objects" page, set the migration options and migration objects (you can select specified tables).

  ![](https://main.qcloudimg.com/raw/a5dc2558be5db94f5121526e1690d72f.png)

5. On the task verification page, complete the verification before migration and click **Start Task**.
  

6. Return to the migration task list. After the incremental sync is 100% complete, click **Complete** in the "Operation" column to complete the migration task.
![](https://main.qcloudimg.com/raw/86e30f0eba3671e4272a27bc1ac9ca97.png)



