Database instance replication means to sync data by configuring one or more backup databases for the server in order to distribute the data in MySQL to multiple systems. TencentDB for MySQL supports three data replication modes:

>
>- "Master" refers to the master database instance, while "Slave" the backup database instance.
> - MySQL v5.6 and v5.7 support three replication modes: async, semi-sync, and strong sync. Only async mode is available in MySQL v5.5.

Async### Async Replication
An application initiates a data update request (i.e., INSERT, UPDATE, or DELETE). After completing the update operation, the master sends a response to the application immediately and then replicates the data to the slave.

During data update, the master does not need to wait for a response from the slave, so the database instance replicated asynchronously often has a higher performance, and slave unavailability will not affect the provision of services by the master. However, as the data is not synced to the slave in real time, if the master fails when a delay occurs on the slave, there is a slight chance of data inconsistency.
TencentDB for MySQL uses a one-master-one-slave architecture for async replication.

### Semi-sync Replication
An application initiates a data update request (i.e., INSERT, UPDATE, or DELETE) request. After completing the update operation, the master replicates the data to the slave immediately. After **receiving the data and writing it into relay log (bypassed)**, the slave returns a success message to the master. Only after receiving the message from the slave will the master return a response to the application.

Only when an exception occurs with data replication (e.g., the slave becomes unavailable or an exception occurs with the network used for replication), the master will suspend the response to the application (for 10 seconds by default in MySQL), and the replication will be downgraded to async replication. When the data replication returns to a normal state, semi-sync replication will be restored.
TencentDB for MySQL uses a one-master-one-slave architecture for semi-sync replication.

### Strong Sync Replication
An application initiates a data update request (i.e., INSERT, UPDATE, or DELETE). After completing the update operation, the master replicates the data to the slave immediately. After **receiving and updating the data**, the slave returns a success message to the master. Only after receiving the message from the slave will the master return a response to the application.

As the data is replicated synchronously from the master to the slave, successful update on the slave must be guaranteed for each update operation on the master. Therefore, strong sync replication can maximize master-slave data consistency. However, the master cannot process an update request until it gets a response from the slave, so slave unavailability can greatly affect the operations on the master.

TencentDB for MySQL uses a one-master-two-slave architecture for strong sync replication. The master can receive the success message as long as either of the two slaves updates the data successfully, preventing the unavailability of a single slave from affecting the operations on the master and improving the availability of the strong sync replication cluster.
