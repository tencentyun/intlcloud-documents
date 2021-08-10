## Background
Traditionally, there are three methods of data replication:
- Async replication: An application initiates an update request. After completing the corresponding operation, the source node (source) responds to the application immediately and replicates data to the replica node (replica) asynchronously.
- Strong sync replication: An application initiates an update request. After completing the operation, the source replicates data to the replica immediately. After receiving the data, the replica returns a success message to the source. Only after receiving the message from the replica will the source respond to the application. The data is replicated synchronously from the source to the replica.
- Semi-sync data replication: when an update request is initiated by an application, the primary node replicates data to the secondary node as soon as the update operation is executed on the primary node. After receiving the data and writing into the relay log (which is not necessary to execute), the secondary node returns a message to the primary node. Only after the message is successfully returned can the primary node respond to the application with a request success.

## Known Issues
When the source or replica is unavailable, there is a chance of data inconsistency for the above three methods.

As the core of system data storage and service, a database should be highly available. In production systems, high availability solutions are often required to ensure uninterrupted system operations, and the data sync technology serves as the foundation of such solutions.

## Solution
In Tencent Cloud's proprietary parallel multi-thread asynchronous replication (MAR, aka strong sync) scheme based on the MySQL protocol, only after a secondary node successfully synchronizes data (logs) can the primary node respond to the application layer, ensuring that the primary and the secondary nodes have completely the same data.

Below is how it works:
![](https://main.qcloudimg.com/raw/9d9629407461c460de1e04e4c88a4830.png)
In the MAR scheme, when a request is initiated at the application layer, only after a secondary node successfully returns a message can the primary node respond to the application layer with a request success, ensuring that the primary and the secondary nodes have completely the same data.
MAR strong sync scheme outperforms other mainstream sync schemes. For more information, see [Performance Comparison Data for Strong Sync](https://intl.cloud.tencent.com/document/product/1042/33377). It has the following features:
- Consistent synchronous replication ensures strong consistency of data between nodes.
- Complete imperceptibility to the business means that read-write separation and sync enhancement are not required at the business side.
- Asynchronization of serial sync threads and introduction of thread pool boost a substantial increase in performance.
- Cluster architecture is supported.
- Automatic member control is supported and faulty nodes are automatically removed from the cluster.
- Automatic node join is supported without human intervention required.
- Each node contains a complete replica of the data and can be switched at any time.
- There is no need to share storage devices.
