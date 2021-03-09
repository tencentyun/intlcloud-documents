Database instance replication means to sync data by configuring one or more backup databases for the server in order to distribute the data in MySQL to multiple systems. TencentDB for MySQL supports three data replication modes:

>?
>- "Source" refers to the source database instance, while "replica" the backup database instance.
>- Currently, MySQL v5.6, v5.7, and v8.0 support three replication modes: async, semi-sync, and strong sync. Only async mode is available in MySQL v5.5.


### Async Replication
An application initiates a data update (including INSERT, UPDATE and DELETE operations) request. After completing the update operation, the source sends a response to the application immediately, and then replicates the data to the replica.

During data update, the source does not need to wait for a response from the replica, so the database instance replicated asynchronously often has a higher performance, and replica unavailability will not affect the provision of services by the source. However, as the data is not synced to the replica in real time, if the source fails when a delay occurs on the replica, there is a slight chance of data inconsistency.
Async replication of TencentDB for MySQL uses a one-source-one-replica architecture.

### Semi-sync Replication
An application initiates a data update (including INSERT, UPDATE, and DELETE operations) request. After completing the update operation, the source replicates the data to a replica immediately. After **receiving and writing the data into relay log (bypassed)**, the replica returns success message to the source. Only after receiving the message from the replica, the source can return a response to the application.

Only when an exception occurs with the data replication (a replica node becomes unavailable or an exception occurs with the network used for data replication), the source will suspend the response to the application (for about 10 seconds by default in MySQL), and the replication will be downgraded to async replication. When the data replication returns to a normal state, semi-sync replication will be restored.
Semi-sync replication of TencentDB for MySQL uses a one-source-one-replica architecture.

### Strong Sync Replication
An application initiates a data update (including INSERT, UPDATE, and DELETE operations) request. After completing the update operation, the source replicates the data to a replica immediately. After **receiving and updating the data**, the replica returns success message to the source. Only after receiving the message from the replica the source can return a response to the application.

As the data is replicated synchronously from the source to the replica, successful update on the replica must be guaranteed for each update operation on the source. Therefore, strong sync replication can maximize source-replica data consistency. However, the source cannot process an update request until it gets a response from the replica, so replica unavailability can greatly affect the operations on the source.

Strong sync replication of TencentDB for MySQL uses a one-source-two-replica architecture. The source can receive the success message as long as either of the two replicas updates the data successfully, preventing the unavailability of a single replica from affecting the operations on the source, and improving the availability of strong sync replication cluster.


