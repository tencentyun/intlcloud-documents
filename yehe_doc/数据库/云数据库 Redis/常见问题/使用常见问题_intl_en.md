### How do I use the hash algorithm of TencentDB for Redis Cluster Edition?
The hash algorithm of the Redis Cluster Edition is the same as that in the a Redis Community Edition cluster, i.e., `HASH_SLOT = CRC16(key) mod 16384`. For more information, see [Redis Cluster Specification](https://redis.io/topics/cluster-spec).

### What is the maximum capacity of a single instance?

| Edition | Specification Range |
|--|--|
| Memory Edition (Standard Architecture) | 0.25–64 GB  |
| Memory Edition (Cluster Architecture) | 12 GB–20 TB  |
| CKV Edition (Standard Architecture) | 4–384 GB  |
| CKV Edition (Cluster Architecture) | 12 GB–48 TB  |

### Is the data stored in TencentDB for Redis reliable?
Redis Standard Architecture (zero-replica) does not provide high availability. Other editions of Redis adopt a master/replica replication structure, where data reliability is ensured by hot backup plus daily cold backup of the data.

### Which persistence method does TencentDB for Redis use?
On the TencentDB for Redis backend, the backup cluster performs full and incremental data backup, and persistence is done on the replicas which is virtually imperceptible to the online business.

### Why is 2 MB of storage capacity used right after an instance is purchased?
That is used by the TencentDB for Redis instance in maintaining its data structure.

### Can TencentDB for Redis be managed with visual tools such as Redis Desktop Manager?
You can perform OPS and management operations in the TencentDB for Redis console. If you need to use a visual tool, use a CVM instance as a jump server to provide an access address for Redis Desktop Manager.

### Will my business be interrupted during scaling?
Momentary disconnections during scaling of different editions of TencentDB for Redis are as describe below:
- During scale-up, if the expanded capacity exceeds the remaining capacity of a single server, the cluster will perform sharding or migrate nodes, and a momentary business disconnection will occur; otherwise, no disconnections will occur.
- During scale-out, the number of nodes in the cluster will be increased, and a momentary business disconnection will occur.
- During scale-in, node repossession will cause node migration in the cluster, and a momentary business disconnection will occur.
- During scale-down, no momentary business disconnections will occur.

### How do I add a monitoring alarm?
This can be implemented through custom monitoring and alarming. For more information, see [Monitoring and Alarming](https://intl.cloud.tencent.com/document/product/239/34589).

### Do I need to purchase different instances for selecting 0-15 databases?
No. Multiple databases can be set on one Standard Architecture or Cluster Architecture instance.

### Does TencentDB for Redis support Lua?
- For Redis Memory Edition (Standard Architecture) instances purchased before September 1, 2018, Lua is not enabled by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
Instances purchased after that have Lua enabled by default.
- Redis Memory Edition (Cluster Architecture), CKV Edition (Standard Architecture), and CKV Edition (Cluster Architecture) instances have Lua enabled by default.

### Does TencentDB for Redis support caching invalidated subscription events?
Yes.

### What should I do if I accidentally deleted an account or forgot the password?
- If you accidentally deleted an account, you can log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID to enter the instance management page, and select **Manage Account** > **Create Account** to create a new account.
- If you forgot the password of the default account, you can reset it by locating the corresponding account on the **Manage Account** page.

### What should I do if the data on a replica node is out of sync with the data on the master node in TencentDB for Redis?
Updates of the TencentDB for Redis master node will be automatically replicated to its associated replica node. Due to Redis' async replication mechanism, replica node updates may lag behind the master node updates. Possible reasons are as follows:
-The I/O write volume of the master node exceeds the sync speed of the replica node.
- There is a network delay between the master node and the replica node.

### How do I check the port connectivity of TencentDB for Redis?
You can use the `telnet` command to check the port connectivity.

### How do I set a caching policy in TencentDB for Redis?
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list to enter the parameter configuration page, and configure a caching policy through the `maxmemory-policy` parameter, whose default value is `noeviction`.

### How do I download a client for TencentDB for Redis?
Clients compatible with the Redis protocol can access TencentDB for Redis. You can choose an appropriate client as needed. For the download addresses, see [Clients](http://redis.io/clients?spm=a2c4g.11186623.2.5.c3a25c83nYgvqS).

### How do I upgrade the version of TencentDB for Redis?
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the **Instance Details** page, where you can upgrade the instance version. For more information, see [Upgrading Instance Version](https://intl.cloud.tencent.com/document/product/239/37710).

### How do I upgrade the architecture of TencentDB for Redis?
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the **Instance Details** page, where you can upgrade the instance architecture. For more information, see [Upgrading Instance Architecture](https://intl.cloud.tencent.com/document/product/239/37860).
