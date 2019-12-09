### Online Scaling
TDSQL supports real-time online scaling. There are two scaling modes: adding new shards and scaling up existing shards.

- **Adding new shards**: This refers to add a new physical shard. Currently, when adding shards, you can split data across the specified shards (the configurations of existing shards stay unchanged), and the data will be automatically distributed to new shards with no manual operation required.
- **Scaling up shards**: This refers to upgrade the configuration of a physical shard. After the upgrade, the data will not be automatically balanced. This mode is mainly used to solve the problem of high load and capacity pressure on a single shard.

>?Shard scaling supports scheduled switch, i.e., you can initiate a task in advance and set the switch time to be during off-hours so as to reduce the impact on your business. For more information on how this works, see [Upgrade Principle and Scheduled Switch](https://cloud.tencent.com/document/product/237/3259).

<font color=#FF0000>To avoid global business interruption caused by simultaneous upgrade of all shards, TDSQL currently only supports scaling one shard online at a time. You need to upgrade the current shard first before upgrading the next one.</font> Although this scheme is more complicated, according to the principle described in the "Automatic Rebalancing" section below, this scheme only affects a part of the entire business with no global interruption caused, because only the involved shard will become read-only (or interrupted) for just seconds during scaling, while the read and write services of other shards will not be affected.


### Automatic Rebalancing
TDSQL ensures the stability of automatic scaling with its proprietary automatic rebalancing technology. Taking adding a new shard as an example, the scaling process is as shown below:

![](https://main.qcloudimg.com/raw/5298e1579dd27b760e6fae4d549f4d87.png)
 
1. After you click scale in the console, the system will calculate the bottleneck of node A (multiple nodes may actually be affected) based on the load and capacity;
2. According to the configuration of new node G, some data of node A will be migrated (from the slave) to node G (the value automatically calculated by the system or allocated manually can be used);
3. After the data is completely synced, nodes A and G will check the database (read-only status for one to tens of seconds), but the entire service will not be suspended.
4. The scheduling system notifies the proxy to switch route.

In order to ensure business continuity and data consistency, the entire migration process of TDSQL is looped in six steps: migrate existing data, sync incremental data, check migrated entries, sync changes again, switch route, and clear, as shown below:
 
![](https://main.qcloudimg.com/raw/1b473bb278d078509cd2be6959b9d3e6.png)
