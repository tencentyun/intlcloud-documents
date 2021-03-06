## Overview
TDSQL supports real-time online scaling. There are two scaling methods: adding new shards and scaling up existing shards. The entire scaling process is completely imperceptible to the business with no business interruption caused. Only the involved shards will become read-only (or interrupted) for just seconds during scaling, while the entire cluster will not be affected.

## Scaling Process
TDSQL ensures the stability of automatic scaling with its proprietary automatic rebalancing technology.

### Adding a new shard
1. Scale node A in the [console](https://console.cloud.tencent.com/dcdb).
2. According to the configuration of new node G, some data of node A will be migrated (from the slave) to node G.
3. After the data is completely synced, nodes A and G will check the database (read-only status for one to tens of seconds), but the entire service will not be suspended.
4. The scheduling system notifies the proxy to switch route.
![](https://main.qcloudimg.com/raw/50299d47e5a0ee8760e9bde16701148a.png)

### Scaling up an existing shard
Scaling up an existing shard is actually replacing it with a larger physical shard.
>?This does not add any new shards and will not change the logic rules of sharding or number of shards.

1. Assign a new physical shard (the "new shard") based on the required configuration.
2. Sync the data and configuration of the physical shard to be upgraded (the "old shard") to the new shard.
3. After the data sync is completed, switch the route in the Tencent Cloud gateway to the new shard for continued use.
![](https://main.qcloudimg.com/raw/7f29be1908e9452fbaf5264293cbe59c.png)
