## Purchasing an Instance
You can log in to the [TDSQL purchase page](https://console.cloud.tencent.com/dcdb/buy) to purchase a TDSQL instance. For a single-node instance (for example, a one-primary-one-secondary instance is considered as a double-node instance), up to eight shards can be purchased.
Initialization is required for the purchased instances to function normally.

## Upgrading an Instance
Upgrade operation will upgrade current TDSQL instances to a higher specification. Since a distributed database is composed of multiple shards, instance upgrade solutions include "Add Shard" and "Upgrade Shard". Your business does not stop during the upgrade process, but some of the shards may become read-only for seconds, so it is recommended to upgrade your instances during off-peak business hours.
>?Up to 64 shards can be added to a single-node instance. If you need more than 64 shards, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

### Adding a shard
1. Log in to the [TDSQL console](https://console.cloud.tencent.com/dcdb/instance/index), click the instance name/ID or **Manage** in the **Operation** column in the instance list, and enter the instance management page.

2. Select the **Shard Management** tab, locate the desired shard in the shard list, and click **Add Shard** in the **Operation** column.
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)
3. On the displayed **Add Shard** page, specify the new shard specification.

### Expanding a shard
This operation upgrades the specification of a single shard to a higher level without adding new shards.
On the instance management page, select the **Shard Management** tab, locate the desired shard in the shard list, and click **Adjust Shard Configuration** in the **Operation** column.

**Upgrade fee = (price of target specification - price of original specification) x remaining validity period**

