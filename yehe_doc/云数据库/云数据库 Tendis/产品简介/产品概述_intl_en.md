
Redis is an open source in-memory data structure store, which features ultra-high concurrency and ultra-low delay in computing and caching. However, Redis is unreliable and costs much when used as a storage database. To solve this issue, you can use TencentDB for Tendis developed by Tencent Cloud, which is compatible with the Redis protocols and stores key-value (KV) data on disks.

TencentDB for Tendis (Tendis) is a KV storage database compatible with the Redis v4.0 protocols, supporting tens of millions of concurrent requests and meeting the needs of different KV storage scenarios. TencentDB for Tendis provides a storage edition and a hybrid storage edition.

- Storage Edition: TencentDB for Tendis Storage Edition stores all data on disks, supports the standard architecture (i.e., primary-secondary architecture), and is compatible with all data structures and most commands of Redis v4.0. It offers a low-cost storage solution for massive KV data.

- Hybrid Storage Edition: TencentDB for Tendis Hybrid Storage Edition is comprised of distributed cache (Redis) and distributed storage (RocksDB), and is 100% compatible with the Redis v4.0 protocols. In this Edition, all data is stored on the disk engine (Tendis), hot data is cached in Redis, and cold data is automatically transitioned and cached.


## Features
- Hybrid storage: Tendis provides a hybrid storage edition, where cold data is automatically transitioned and cached to achieve a better balance between cost and performance.
- Primary/secondary hot backup: Tendis supports primary/secondary hot backup, automatic failure monitoring, automatic disaster recovery, and data storage on six replicas.
- Elastic expansion: Tendis supports elastic expansion through the entire lifecycle of your business, including horizontal expansion (adding more shards) and vertical expansion (increasing the capacity of a shard).
- Distributed storage: your data is distributed across multiple physical machines, helping you get rid of standalone capacity and resource constraints.

