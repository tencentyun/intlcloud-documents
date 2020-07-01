### What is the maximum capacity of a single instance?

| Edition | Specification Range |
|--|--|
| Redis Standard Edition | 0.25 GB - 60 GB  |
| Redis Cluster Edition | 12 GB - 4 TB  |
| CKV Standard Edition | 4 GB - 384 GB  |
| CKV Cluster Edition | 12 GB - 48 TB  |

### Is the data stored in TencentDB for Redis reliable?
Redis Standard Edition (zero-replica) does not provide high availability. Other editions of Redis adopt a master/slave replication structure, where data reliability is ensured by hot backup plus daily cold backup of the data.

### Which persistence method does TencentDB for Redis use?
On the TencentDB for Redis backend, the backup cluster performs full and incremental data backup, and persistence is done on the slaves which is virtually imperceptible to the online business.

### Why is 2 MB of storage capacity used right after an instance is purchased?
That is used by the TencentDB for Redis instance in maintaining its data structure.

### Can TencentDB for Redis be managed with visual tools such as Redis Desktop Manager?
You can perform OPS and management operations in the TencentDB for Redis Console. If you need to use a visual tool, use a CVM instance as a jump server to provide an access address.

### Will my business be interrupted during instance scaling?
- In Redis Standard Edition (Community), CKV Standard Edition, and CKV Cluster Edition, if the physical machine has enough memory, the upgrade can be imperceptible; otherwise, data will be migrated across servers and lead to a momentary connection interruption lasting for just seconds.
- In Redis Cluster Edition (Community), scaling can be completely imperceptible to the business.

### How do I add a monitoring alarm?
This can be implemented through custom monitoring and alarming. For more information, please see [Monitoring and Alarming](https://intl.cloud.tencent.com/document/product/239/34589).

### Do I need to purchase different instances for selecting 0-15 databases?
No, you do not have to. Multiple databases can be set on a Standard or Cluster Edition instance.


### Does TencentDB for Redis support Lua?
- For Redis Standard Edition (Community) instances purchased before September 1, 2018, Lua is not enabled by default. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
Instances purchased after that have Lua enabled by default.
- Redis Cluster Edition (Community), CKV Standard Edition, and CKV Cluster Edition instances have Lua enabled by default.

