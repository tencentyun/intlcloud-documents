
### Metrics

| Metric Name | Unit | Description |
| -------------------------- | ---- | -------------------------------------- |
| tcp                        | -   | Number of TCP server connections                      |
| http                       | -   | Number of HTTP server connections                     |
| watches                    | -   | Number of ZooKeeper event subscriptions                           |
| ephemeralNode              | -   | Number of ephemeral nodes retained in ZooKeeper            |
| backgroundPoolTask         | -   | Number of active tasks in `BackgroundProcessingPool` |
| backgroundSchedulePoolTask | -   | Number of active tasks in `BackgroundSchedulePool`   |
| contextLockWait            | -   | Number of threads waiting for lock in `Context`              |
| delayedInserts             | -   | Number of throttled INSERT queries                   |
| dictCacheRequests          | -   |  Number of requests in the data sources of the dictionaries in cache type        |
| distributedSend            | -   | Number of pending files to be inserted into distributed tables asynchronously     |
| global                     | -   | Number of threads in global thread pool                   |
| globalActive               | -   | Number of active threads in global thread pool               |
| local                      | -   | Number of threads in local thread pool                   |
| localActive                | -   | Number of active threads in local thread pool               |
| leaderElection             | -   | Number of replicas participating in leader election               |
| leaderReplica              | -   | Number of replicated tables that are leaders     |
| readonlyReplica            | -   | Number of replicated tables in read-only status   |
| memoryTracking             | GB   | Total size of memory assigned to currently executing queries       |
| backgroundProcessingPool   | GB   | Total size of memory assigned to background processing pool             |
| backgroundSchedulePool     | GB   | Total size of memory assigned to background schedule pool           |
| memoryTrackingForMerges    | GB   | Total size of memory assigned for background merges             |
| merge                      | -   | Number of executing background merges                |
| read                       | -   | Number of opened readable files                   |
| write                      | -   | Number of opened writable files                   |
| partMutation               | -   | Number of table mutations                           |
| queryThread                | -   | Number of query processing threads                     |
| queryPreempted             | -   | Number of queries that are stopped or waiting                   |
| read                       | -   | Number of read system calls                       |
| write                      | -   | Number of write system calls                       |
| fetch                      | -   | Number of data blocks fetched from replicas                 |
| send                       | -   | Number of data blocks sent to replicas                 |
| check                      | -   | Number of data blocks for consistency check                 |
| revision                   | -   | Server modification                           |
| version                    | 1    | Version number                                 |
| waitingRead                | -   | Number of threads waiting for read on table read/write lock              |
| waitingWrite               | -   | Number of threads waiting for write on table read/write lock             |
| activeRead                 | -   | Number of threads with read lock in table read/write lock      |
| activeWrite                | -   | Number of threads with write lock in table read/write lock     |
| storageBufferRows          | -   | Number of rows in buffer tables                  |
| storageBufferBytes         | MB   | Number of bytes in buffer tables                |

### Events

| Metric Name | Unit | Description |
| ------------- | ---- | ----------------------------------------------------- |
| total         | -   | Number of queries that may be executed                                    |
| select        | -   | Number of SELECT queries that may be executed                                |
| insert        | -   | Number of INSERT queries that may be executed                                |
| insertedRows  | -   | Number of rows inserted into all tables                                |
| insertedBytes | -   | Number of bytes inserted into all tables                              |
| read          | µs | Total time for waiting for read system calls                                |
| write         | µs | Total time for waiting for write system calls                                |
| fileOpen      | -   | Number of opened files                                        |
| read          | -   | Number of reads from file descriptors                                |
| write         | -   | Number of writes into file descriptors                                |
| read          | MB   | Number of bytes read from file descriptors                              |
| write         | MB   | Number of bytes written into file descriptors                                |
| realtime      | µs | Total time for processing threads                                  |
| user          | µs | Total time for processing threads executing CPU instructions in user space         |
| system        | µs | Total time for processing threads executing CPU instructions in OS kernel space |
| regexpCreated | -   | Number of compiled regular expressions                                    |

### Asynchronous_metrics

| Metric Name | Unit | Description |
| ------------------------ | ---- | ----------------------------------- |
| markCacheBytes           | MB   | Size of cache of marks of StorageMergeTree   |
| markCacheFiles           | -   | Number of cache files of marks of StorageMergeTree |
| maxPartCountForPartition | -   | Maximum number of active data blocks in partitions  |
| databaseCount            | -   | Number of databases                          |
| tableCount               | -   | Number of tables                          |
| absolute                 | ms | Maximum replica queue latency               |
| relative                 | µs |  Maximum difference of the absolute latency from another replica  |
| insert                   | -   | Number of INSERT operations of data blocks that need to be performed            |
| merge                    | -   | Number of merges to be completed                     |
| replicasMaxQueueSize     | -   | Size of the queue for the operations to be performed              |
