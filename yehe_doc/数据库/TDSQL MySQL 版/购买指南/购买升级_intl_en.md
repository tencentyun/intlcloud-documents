## Instance Purchase
You can purchase instances on the [TDSQL for MySQL purchase page](https://console.cloud.tencent.com/tdsqld/tdmysql-buy). For each instance node (for example, one source and one replica are 2 nodes), you can purchase up to 8 shards at a time.
Initialization is required for the purchased instances to run normally.


## Instance Upgrade
Instance upgrade refers to upgrading the current TDSQL for MySQL instance to a higher specification. As a distributed database is composed of multiple shards, instance upgrade can be divided into "adding shards" and "expanding shards". The service will not stop during the upgrade, but some shards may become read-only for several seconds. Therefore, we recommend you upgrade your instances during off-peak hours.
>?To ensure the optimal distributed performance, we recommend you use a maximum of 8 shards. When upgrading the configuration, expand the shards first and consider adding more shards only when further expansion is impossible.

### Adding shard
1. Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/tdsqld). In the instance list, click an instance ID or **Manage** in the **Operation** column to access the instance management page.
2. On the instance management page, select the **Shard Management** tab and click **Add Shard** in the **Operation** column.
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)
3. In the pop-up window, select the specification of the new shard.

### Expanding shard
This operation upgrades the specification of a single shard to a higher level without adding new shards.
Go to the instance management page, select the **Shard Management** tab, and click **Adjust Shard Configuration** in the **Operation** column to make adjustments.

**Upgrade fees = (price of target specification - price of original specification) * remaining validity period**

