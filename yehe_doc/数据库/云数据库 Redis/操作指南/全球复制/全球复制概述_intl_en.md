TencentDB for Redis supports global replication for consistent data sync across regions. 

## Why Global Replication
When the native code of Redis performs cross-region replication, if the local instance is written excessively or is disconnected from replication for a long time, the `backlog` of the master node may not be able to resume the replication, resulting in mandatory full replication by the remote instance. This will block access to and seriously affect the normal business of the remote instance. For more information, see [Replication](https://redis.io/topics/replication).

In addition, Redis' native replication scheme does not mark written nodes in the `backlog`, which tends to cause replication loops and data inconsistency when two-way replication is required between the local and remote instances.

## Implementation Mechanism
Global replication is a new feature added to the open-source version of the kernel by Tencent Cloud. It is fully compatible with Redis 4.0 and Redis 5.0 commands. Based on the original leader-follower replication scheme, a new log file is added for remote replication to ensure the eventual data consistency for instances in any region in the replication group.
- Before the log file is replicated by the remote node, the local node will keep it to ensure the continuity of remote replication.
- The log file contains the `ServerID` to identify the ID of the node to which the log file is written and supports two-way replication to avoid replication loops.
- The log file contains the command execution timestamp and the version number of the operation `KEY` to resolve command conflicts.

![](https://qcloudimg.tencent-cloud.cn/raw/03cc44b805ae54db35c0627091cbb42f.png)


> !Global replication records a version number for each `KEY`. Each `KEY` will occupy 4 bytes of memory overheads, taking up more memory.

## Use Cases
### Read-only instance and disaster recovery
In the global replication scheme of TencentDB for Redis, a master instance is configured in a replication group, while read-only instances are deployed in multiple regions and replicate data from the master instance. The data version is based on the master instance, and the data consistency level is eventual consistency. This allows you to access data locally with a quicker response, better experience, higher data availability, and greater data security.
![](https://qcloudimg.tencent-cloud.cn/raw/3023873423bc126eca8b76d0e421ea3b.png)

### Multi-master architecture
If you need to roam and merge data across regions, you need to distribute the same copy of data in multiple regions, read and update data in any region, or merge data from multiple regions. In this case, the database should have the ability to write data in multiple regions. In a global replication group, you can configure a multi-master architecture, so data written to one master instance will be synced to other master instances in other regions.
![](https://qcloudimg.tencent-cloud.cn/raw/8455e41f886cd09a342c8516e735d2ee.png)
> !TencentDB for Redis master instances do not perform version detection and write time check for data written by the application and by other master instances in the replication group; instead, they execute the commands chronologically in the order they are received. If the same data is updated in different master instances at the same time, the globally replicated data may be misaligned and fail to be consistent.
> Therefore, in multi-master scenarios, avoid updating the same data in different master instances at the same time. As the multi-instance architecture may cause data inconsistency, carefully evaluate whether it is suitable for your business.

