## Background
Traditionally, there are three methods of data replication:
- Async replication: An application initiates an update request. After completing the corresponding operation, the master node (master) responds to the application immediately and replicates data to the slave node (slave) asynchronously.
- Strong sync replication: An application initiates an update request. After completing the operation, the master replicates data to the slave immediately. After receiving the data, the slave returns a success message to the master. Only after receiving the message from the slave will the master respond to the application. The data is replicated synchronously from the master to the slave.
- Semi-sync replication: Generally, strong sync replication is employed. When an exception occurs with the data replication from the master to the slave (e.g., the slave becomes unavailable or an exception occurs with the network connection between the two nodes), the replication will be downgraded to async replication. When the replication returns to a normal state, strong sync replication will be restored from async replication.

## Known Issues
When the master or slave is unavailable, there is a chance of data inconsistency for the above three methods.

As the core of system data storage and service, a database should be highly available. In production systems, high availability solutions are often required to ensure uninterrupted system operations, and the data sync technology serves as the foundation of such solutions.

## Solution
Multi-Thread Asynchronous Replication (MAR) is Tencent's proprietary MySQL-based multi-thread strong sync replication solution. Only after the slave data is completely synced (with log) can the master respond to the application transaction, which prevents data loss and errors.

Below is how it works:
![](https://main.qcloudimg.com/raw/9d9629407461c460de1e04e4c88a4830.png)

MAR strong sync scheme outperforms other mainstream sync schemes. For more information, see [Performance Comparison Data for Strong Sync](https://intl.cloud.tencent.com/document/product/1042/33377). It has the following features:
- Consistent synchronous replication ensures strong consistency of data between nodes.
- Complete imperceptibility to the business means that read-write separation and sync enhancement are not required at the business side.
- Asynchronization of serial sync threads and introduction of thread pool boost a substantial increase in performance.
- Cluster architecture is supported.
- Automatic member control is supported and faulty nodes are automatically removed from the cluster.
- Automatic node join is supported without human intervention required.
- Each node contains a complete replica of the data and can be switched at any time.
- There is no need to share storage devices.
