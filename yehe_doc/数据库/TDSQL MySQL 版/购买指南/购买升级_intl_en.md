## Instance Purchase
You can log in to the [TDSQL for MySQL purchase page](https://console.cloud.tencent.com/tdsqld/tdmysql-buy) to purchase a TDSQL for MySQL instance. For a single-node instance (for example, a one-primary-one-secondary instance is considered as a double-node instance), up to eight shards can be purchased.
Initialization is required for the purchased instances to function normally.

## Instance Upgrade
Upgrade operation will upgrade an existing TDSQL for MySQL instance to a higher specification. Since a distributed database is composed of multiple shards, you can add new shards or expand existing shards to upgrade an instance. Your business does not stop during the upgrade process, but a few shards may become read-only for seconds, so we recommend that you upgrade instances during off-peak hours.
>?Up to 64 shards can be added to a single-node instance. If you need more than 64 shards, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

### Adding a shard
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld). In the instance list, click the instance name/ID or **Manage** in the **Operation** column, and enter the instance management page.

2. On the **Shard Management** tab, locate the desired shard in the shard list, and click **Add Shard** in the **Operation** column.
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)
3. On the displayed **Add Shard** page, specify the new shard specification.

### Expanding a shard
This operation upgrades the specification of a single shard to a higher level without adding new shards.
On the instance management page, select the **Shard Management** tab, locate the desired shard in the shard list, and click **Adjust Shard Configuration** in the **Operation** column.

**Upgrade fee = (price of target specification - price of original specification) x remaining validity period**

