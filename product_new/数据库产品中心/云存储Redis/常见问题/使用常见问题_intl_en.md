### What is the maximum capacity of a single instance?

| Edition | Specification Range |
|--|--|
| Redis Standard Edition | 0.25 GB - 60 GB |
| Redis Cluster Edition | 12 GB - 4 TB |


### Is the data stored in TencentDB for Redis reliable?
Redis Standard Edition (zero-replica) does not provide high availability. Other editions of Redis adopt a master/slave replication structure, where data reliability is ensured by hot backup plus daily cold backup of the data.

### Which persistence method does TencentDB for Redis use?
On the TencentDB for Redis backend, full and incremental data backup is performed by the backup cluster, and persistence is done on the slaves which is virtually imperceptible to the online business.

### Why is 2 MB of storage capacity used just after an instance is purchased?
That is used by the data structure of the TencentDB for Redis instance.

### Can TencentDB for Redis be managed with visual tools such as Redis Desktop Manager?
You can perform OPS and management operations in the TencentDB for Redis Console. If you need to use a visual tool, use a CVM instance as a jump server to provide an access address.

### Will my business be interrupted during instance scaling?
- In Redis Standard Edition (Community), if the physical machine has enough memory, the upgrade can be imperceptible; otherwise, data will be migrated across servers and lead to a momentary connection interruption lasting for just seconds.
- In Redis Cluster Edition (Community), scaling can be completely imperceptible to the business.

### How do I add a monitoring alarm?
This can be implemented through custom monitoring and alarming. For more information, see [Monitoring and Alarming](https://intl.cloud.tencent.com/document/product/239/31949).

### Do I need to purchase different instances for selecting 0-15 databases?
- One Cluster Edition instance can provide only one database, so only `select 0` is available.
- Multiple databases can be set on one Standard Edition instance.

### Can the password authentication step be removed?
Currently, password-free login is not supported.

### Does TencentDB for Redis support Lua?
- For Redis Standard Edition (Community) instances purchased before September 1, 2018, Lua was not enabled by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
Instances purchased after that have Lua enabled by default.
- Redis Cluster Edition (Community) instances have Lua enabled by default.

