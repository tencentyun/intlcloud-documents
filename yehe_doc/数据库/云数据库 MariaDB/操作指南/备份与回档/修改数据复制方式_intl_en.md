
## Data Replication Mode
Data replication mode, aka data sync mode, is a mechanism for data replication of primary and replica nodes in the high availability scheme of database. Currently, TencentDB for MariaDB supports the following modes:
- **Async replication**: an application initiates an update request such as adding, deletion, or modification. After completing the corresponding operation, the primary node (primary) responds to the application immediately and replicates data to the replica node (replica) asynchronously. Therefore, in async replication mode, an unavailable replica does not affect operations on the primary, while an unavailable primary may cause data inconsistency.

- **Strong sync (non-downgradable) replication**: an application initiates an update request. After completing the operation, the primary replicates data to the replica immediately. After receiving the data, the replica returns a success message to the primary. Only after receiving the message from the replica will the primary respond to the application. The data is replicated synchronously from the primary to the replica. Therefore, an unavailable replica will affect operations on the primary, while an unavailable primary will not cause data inconsistency.
>!When you perform strong sync replication, the primary database will be hanged if it is disconnected from the replica database or the replica database fails. If there is only one primary or replica database, the high-availability scheme is unavailable, because if only one single server is used, part of data will be lost completely when a failure occurs, which does not meet the requirements for finance-level data security.

- **Strong sync (downgradable) replication**: batch processing and writing large amounts of transaction data in the business system may cause severe delay in the replica; moreover, in strong sync (non-downgradable) mode, the remaining node will be hanged. These mechanisms designed to ensure data consistency may cause exceptions in the business system.
To address this problem, TencentDB provides a scheme where the strong sync mechanism can be downgraded to async mode. When the replica delay is longer than or equal to 15 seconds, the system will automatically downgrade the strong sync mode to async mode; if it then becomes shorter than 15 seconds, the system will automatically upgrade the async mode to strong sync mode. In this way, strong sync (downgradable) replication is an efficient scheme to ensure eventual data consistency.
>?Different from the open-source semi-sync mechanism of Google, strong sync replication uses thread pools instead of the worker thread mode. Besides, the downgradable scheme is better than the semi-sync mode.

## Modifying Data Replication Mode
>?The one-primary-one-replica architecture of TencentDB for MariaDB provides only two schemes: strong sync (downgradable) replication and async replication. If data consistency is required, please purchase the three-node edition with one primary and two replicas.

1. Log in to the [TencentDB for MariaDB console](https://console.cloud.tencent.com/mariadb), click an instance ID in the instance list, and enter the instance details page.
2. Click the edit icon next to **Data Replication Mode** in the **Availability Info** section.
>?The modification will not affect normal operations of the instance and will take effect in up to five seconds.
>
![](https://main.qcloudimg.com/raw/6ecc6d4cf5a9221567ac103c8153c799.png)

