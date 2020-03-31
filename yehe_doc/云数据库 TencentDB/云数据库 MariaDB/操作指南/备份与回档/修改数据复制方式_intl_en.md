## Data Replication Mode
Data replication mode, aka data sync mode, is a mechanism for data replication of master and slave nodes in the high availability scheme of database. Currently, TencentDB for MariaDB supports the following modes:
- **Async replication**: an application initiates an update request such as adding, deletion, or modification. After completing the corresponding operation, the master node (master) responds to the application immediately and replicates data to the slave node (slave) asynchronously. Therefore, in async replication mode, an unavailable slave does not affect operations on the master database, while an unavailable master may cause data inconsistency.

- **Strong sync (non-downgradable) replication**: an application initiates an update request. After completing the operation, the master replicates data to the slave immediately. After receiving the data, the slave returns a success message to the master. Only after receiving the message from the slave will the master respond to the application. The data is replicated synchronously from the master to the slave. Therefore, an unavailable slave will affect operations on the master database, while an unavailable master will not cause data inconsistency.
>When you perform strong sync replication, the master database will be hanged if it is disconnected from the slave database or the slave database fails. If there is only one master or slave database, the high-availability scheme is unavailable, because if only one single server is used, part of data will be lost completely when a failure occurs, which does not meet the requirements for finance-level data security.

- **Strong sync (downgradable) replication**: batch processing and writing large amounts of transaction data in the business system may cause severe delay in the slave; moreover, in strong sync (non-downgradable) mode, the remaining node will be hanged. These mechanisms designed to ensure data consistency may cause exceptions in the business system.
To address this problem, TencentDB provides a scheme where the strong sync mechanism can be downgraded to async mode. When the slave delay is longer than or equal to 15 seconds, the system will automatically downgrade the strong sync mode to async mode; if it then becomes shorter than 15 seconds, the system will automatically upgrade the async mode to strong sync mode. In this way, strong sync (downgradable) replication is an efficient scheme to ensure eventual data consistency.
>Different from the open-source semi-sync mechanism of Google, strong sync replication uses thread pools instead of the worker thread mode. Besides, the downgradable scheme is better than the semi-sync mode.

## Modifying Data Replication Mode
>The one-master-one-slave architecture of TencentDB for MariaDB provides only two schemes: strong sync (downgradable) replication and async replication. If data consistency is required, please purchase the three-node edition with one master and two slaves.
>
You can set the data replication mode during **instance initialization** or modify it in **Instance Details** > **Data Replication Mode**.
>The modification will not affect normal operations of the instance and will take effect in up to five seconds.
>
![](https://main.qcloudimg.com/raw/cd3595021681315c7214bfad25a2ca83.png)

