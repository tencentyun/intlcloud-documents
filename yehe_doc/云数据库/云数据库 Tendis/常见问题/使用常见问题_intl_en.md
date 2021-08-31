### How do I use the hash algorithm of TencentDB for Tendis Cluster Edition?
The hash algorithm of the Tendis Cluster Edition is the same as that in the Redis Cluster Community Edition, i.e., `HASH_SLOT = CRC16(key) mod 16384`. For more information, please see [Redis Cluster Specification](https://redis.io/topics/cluster-spec).

### Can TencentDB for Tendis be managed with visual tools?
TencentDB for Tendis supports the [data management console (DMC)](https://bj-dmc.cloud.tencent.com/v2/qcloudLogin/login) for visual management.

### Will my business be interrupted during instance scaling?
TencentDB for Tendis Storage Edition and Hybrid Storage Edition support expansion without storage capacity loss. Disk capacity expansion takes less than 1 minute if the resources are sufficient, while capacity reduction needs data migration and causes a short disconnection.

### Does TencentDB for Tendis support Lua?
- Storage Edition: Lua is currently not supported but will be supported in the future.
- Hybrid Storage Edition: Lua is supported. However, like Redis Cluster, Tendis Hybrid Storage Edition does not support multi-key operations across slots when Lua is enabled.

### Does TencentDB for Tendis support subscribing to the cache invalidation event?
Yes.
