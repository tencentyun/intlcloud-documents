Database instance replication means to sync data by configuring one or more backup databases for the server in order to distribute the data in MySQL to multiple systems. TencentDB for MySQL supports three data replication modes:

>
>
>- "Master" refers to the master database instance, while "Slave" the backup database instance.
>- Currently, MySQL v5.6, v5.7 and v8.0 support three replication modes: async, semi-sync, and strong sync. Only async mode is available in MySQL v5.5.

### Async Replication
An application initiates a data update (including insert, update and delete operations) request. After completing the update operation, the Master sends a response to the application immediately, and then replicates the data to the Slave.

During data update, the master does not need to wait for a response from the slave, so the database instance replicated asynchronously often has a higher performance, and slave unavailability will not affect the provision of services by the master. However, as the data is not synced to the slave in real time, if the master fails when a delay occurs on the slave, there is a slight chance of data inconsistency.
Asynchronous replication of Tencent Cloud database for MySQL uses a "One Master, One Slave" architecture.

### Semisync replication

An application initiates a data update (including insert, update and delete operations) request. After completing the update operation, the Master replicates the data to a Slave immediately. After **receiving and writing the data into relay log (bypassed)**, the Slave returns success message to the Master. Only after receiving the message from the Slave, the Master can return a response to the application.

Only when an exception occurs with the data replication (a Slave node becomes unavailable or an exception occurs with the network used for data replication), the Master will suspend the response to the application (for about 10 seconds by default in MySQL), and the replication will be downgraded to asynchronous replication. When the data replication returns to a normal state, semisync replication will be restored.
Semi-synchronous replication of Tencent Cloud database for MySQL uses a "One Master, One Slave" architecture.

### Strong Sync Replication

An application initiates a data update request (i.e., INSERT, UPDATE, or DELETE). After completing the update operation, the master replicates the data to the slave immediately. After receiving and updating the data, the slave **returns a success message to the master**. Only after receiving the message from the slave will the master return a response to the application.

As the data is replicated synchronously from the master to the slave, successful update on the slave must be guaranteed for each update operation on the master. Therefore, strong sync replication can maximize master-slave data consistency. However, the master cannot process an update request until it gets a response from the slave, so slave unavailability can greatly affect the operations on the master.

TencentDB for MySQL uses a one-master-two-slave architecture for strong sync replication. The master can receive the success message as long as either of the two slaves updates the data successfully, preventing the unavailability of a single slave from affecting the operations on the master and improving the availability of the strong sync replication cluster.
