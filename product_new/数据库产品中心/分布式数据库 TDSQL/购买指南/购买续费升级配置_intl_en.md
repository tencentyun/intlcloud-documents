## Instance Purchase
Log in to the [TDSQL Purchase Page](https://console.cloud.tencent.com/dcdb/buy) to purchase an instance. You can purchase up to 64 shards at a time, and if you need more, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
Initialization is required for the purchased instance to function normally.

## Instance Upgrade
An instance upgrade operation will upgrade the current TDSQL instance to a higher specification; however, as a distributed database is composed of multiple shards, instance upgrade schemes actually include "adding new shards" and "scaling up shards". During upgrade, the service will not be interrupted, but some shards may become read-only for just seconds, so you are recommended to upgrade your instance during off-hours.

### Adding new shards
1. Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb/instance/index). In the instance list, click an instance name or **Manage** in the "Operation" column to go to the instance management page.

2. Select the **Shard Management** tab, click **Add Shard** in the "Operation" column.
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)
3. In the pop-up dialog box, select specifications for the new shard.

### Scaling up shards
This operation upgrades a single shard to a higher specification without adding new shards.
Go to the instance management page, select the **Shard Management** tab, and click **Adjust Shard Configuration** in the "Operation" column.


**Upgrade fee = (unit price of target specification - unit price of original specification) x remaining validity period**

