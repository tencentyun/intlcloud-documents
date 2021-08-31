Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business and build a high-availability database architecture for remote disaster recovery through real-time sync channels. Its data subscription feature grants you real-time access to incrementally updated data in your TencentDB instance, so that you can consume such data based on your business needs. Currently, DTS for MongoDB supports data migration on different versions of MongoDB and in various network scenarios.

| Term | Description |
| -------- | -------------------------------------------------- |
| Source instance | Source instance to be migrated. |
| Target instance | Target instance to be migrated to, i.e., user-purchased TencentDB for MongoDB. |
| CVM-based self-created database | MongoDB service deployed on a CVM instance. |
| Public network-based self-created database | MongoDB service deployed on the public network. |

## Migration Support Description
**Supported features**
- Data migration: DTS supports one-time migration of all data to the cloud.
- Data sync: DTS supports real-time data sync by combining full migration and incremental sync.

**Supported versions**
- DTS supports MongoDB 3.2, 3.4, and 3.6.
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
- After the successfully migrated data is verified by your business, the connection to the source instance can be closed and then switched to the target instance.
- Online migration is not supported for self-created single-node instances as they have no oplogs.
