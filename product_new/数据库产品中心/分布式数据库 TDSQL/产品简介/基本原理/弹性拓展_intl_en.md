## Overview
TDSQL supports real-time online scaling. There are two scaling methods: adding new shards and scaling up existing shards. The entire scaling process is completely imperceptible to the business with no business interruption caused. Only the involved shards will become read-only (or interrupted) for just seconds during scaling, while the entire cluster will not be affected.

## Scaling Process
TDSQL ensures the stability of automatic scaling with its proprietary automatic rebalancing technology.

### Adding a new shard
1. After you click scale in the console, the system will calculate the bottleneck of node A (multiple nodes may actually be affected) based on the load and capacity.
2. According to the configuration of new node G, some data of node A will be migrated (from the slave) to node G.
3. After the data is completely synced, nodes A and G will check the database (read-only status for one to tens of seconds), but the entire service will not be suspended.
4. The scheduling system notifies the proxy to switch route.
![](https://mc.qcloudimg.com/static/img/d407c9bf2740c3ceb803392448856cf2/image.png)

### Scaling up an existing shard
Scaling up an existing shard is actually replacing it with a larger physical shard.
>This does not add any new shards and will not change the logic rules of sharding or number of shards.

1. Assign a new physical shard (the "new shard") based on the required configuration.
2. Sync the data and configuration of the physical shard to be upgraded (the "old shard") to the new shard.
3. After the data sync is completed, switch the route in the Tencent Cloud gateway to the new shard for continued use.
![](https://mc.qcloudimg.com/static/img/d30e97c05742feccf7728e6a326e826f/image.png)
