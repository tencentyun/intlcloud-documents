## Instance Purchase
Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb) and click **Create** to purchase an instance. You can purchase up to 64 shards at a time, and if you need more, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
Initialization is required for the purchased instance to function normally.

## Instance Upgrade
An instance upgrade operation will upgrade the current TDSQL instance to a higher specification; however, as a distributed database is composed of multiple shards, instance upgrade schemes actually include "adding new shards" and "scaling up shards". During upgrade, the service will not be interrupted, but some shards may become read-only for just seconds, so you are recommended to upgrade your instance during off-hours.

### Adding new shards
1. In the TDSQL Console, click the instance name or **Manage** in the "Operation" column to enter the instance management page.
![](https://main.qcloudimg.com/raw/2d971c5208429a4fcd5620bfd8e9c8a0.png)
2. Select the **Shard Management** tab, click **Add Shard** in the "Operation" column, and select the specification and quantity of new shards in the pop-up dialog box.
![](https://main.qcloudimg.com/raw/d9a2e9b9261b3252a0db00472b1c3c92.png)

### Scaling up shards
This operation upgrades a single shard to a higher specification without adding new shards.
Enter the instance management page, select the **Shard Management** tab, and click **Expand Shard** in the "Operation" column.
![](https://main.qcloudimg.com/raw/4e28cc10867d73661ed688ba3240fe18.png)

**Upgrade fee = (unit price of target specification - unit price of original specification) x remaining validity period**

