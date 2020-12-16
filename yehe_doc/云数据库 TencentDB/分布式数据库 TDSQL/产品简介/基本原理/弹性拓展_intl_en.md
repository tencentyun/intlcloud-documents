## Overview
TencentDB for TDSQL supports real-time online expansion. There are two capacity expansion methods: adding shards and expanding the existing shards. The entire expansion process is completely imperceptible to your business without downtime. Only a fraction of shards become read-only for seconds (or are interrupted) during the expansion, while the entire cluster will not be affected.

## Capacity Expansion Process
TDSQL ensures automatic expansion and stability with Tencent's automatic rebalancing technology.

### Adding a new shard
1. Scale node A in the [console](https://console.cloud.tencent.com/dcdb).
2. According to the configuration of new node G, some data of node A will be migrated (from secondary) to node G.
3. After the data is completely synchronized, node A and node G will validate the database (read-only for one to tens of seconds), but the entire service is not suspended.
4. Schedule and notify proxy to switch routing.
![](https://main.qcloudimg.com/raw/50299d47e5a0ee8760e9bde16701148a.png)

### Expanding an existing shard
The expansion based on existing shards is actually replacing the old one with a larger physical shard.
>?The expansion based on existing shards does not add any shard and will not change the logic rules of sharding or the number of shards.

1. Assign a new physical shard (hereinafter referred to as "new shard") based on required configuration.
2. Synchronize the data and configuration of the physical shard to be upgraded (hereinafter referred to as "old shard") to the new shard.
3. After the data sync is completed, switch the route in the Tencent Cloud gateway to the new shard, then you can use the new shard.
![](https://main.qcloudimg.com/raw/7f29be1908e9452fbaf5264293cbe59c.png)


## Relevant Operations
A TDSQL instance contains multiple shards. To upgrade the specification of an existing TDSQL instance, please see [Purchase and Upgrade](https://intl.cloud.tencent.com/document/product/1042/33333).
