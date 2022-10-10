## Instance Purchase
You can purchase instances on the [TDSQL for MySQL purchase page](https://console.cloud.tencent.com/tdsqld/tdmysql-buy). For each instance node (for example, one source and one replica are counted as 2 nodes), you can purchase up to 8 shards at a time.

## Instance Upgrade
Instance upgrade refers to the process of upgrading an existing TDSQL for MySQL instance to a higher specification. As a distributed database is composed of multiple shards, instance upgrade can be divided into "adding shards" and "expanding shards". The service will not stop during the upgrade, but some shards may become read-only for several seconds. Therefore, we recommend that you upgrade your instances during off-peak hours.
>?To ensure the optimal distributed performance, we recommend that you use a maximum of 8 shards. When upgrading the configuration, you must first expand the shards until their specifications cannot be increased any more, at which point you can consider adding more shards.

### Adding shard
1. Log in to the [TDSQL for MySQL console] (https://console.cloud.tencent.com/tdsqld). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Shard Management** tab and click **Add Shard**.
>?You do not need to select any existing shards when adding new ones. All shards are automatically expanded by using a proprietary automatic rebalancing technology to ensure the expansion stability. For more information on the expansion process, see [Elastic Expansion](https://intl.cloud.tencent.com/document/product/1042/33317).
>
![](https://qcloudimg.tencent-cloud.cn/raw/f8c2b73090d194089fa13d1fcdec9339.png)
3. In the pop-up window, select the specification of the new shard.

### Expanding shard
This operation upgrades the specification of a single shard to a higher level without adding new shards.
Go to the instance management page, select the **Shard Management** tab, and click **Adjust Shard Configuration** in the **Operation** column to make adjustments.

**Upgrade fee = (price of target specification - price of original specification) x remaining validity period**