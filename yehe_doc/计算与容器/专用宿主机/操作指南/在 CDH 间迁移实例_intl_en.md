## Overview
This document describes how to migrate instances among dedicated hosts.

## Notes
To migrate an instance, note the following:
- The instance to migrate is shut down.
- An instance with local disks cannot be migrated.
- Use VPC for the migiration. If you need to migrate an instance in the classic network, [switch to VPC](https://intl.cloud.tencent.com/document/product/213/20278)

The destination CVM Dedicated Host (CDH) should meet the following requirements:
- Both the source and destination CDHs are in the same availability zone of a single region under the same account.
- The destination CDH has sufficient available resources. The available CPU and memory resources should be no less than that of the instances to migrate.


## Directions
1. Log in to the CVM console and click [**Dedicated Hosts**](https://console.cloud.tencent.com/cvm/cdh) on the left sidebar.
2. Select the region where the CDH resides.
3. Click the **ID/Host Name** of the CDH that hosts the instance to migrate to enter the details page. Select the **Instance List** tab.
4. Migrate one or multiple instances in the list as needed:
<dx-tabs>
::: Migrating\sa\ssingle\sinstance
Select the instance to migrate, and click **More** > **Change Host** under the **Operation** column.
![](https://main.qcloudimg.com/raw/21c285344c30738735080c3354a4897c.png)
:::
::: Batch\smigrating\sinstances
Select instances to migrate, and select **More Actions** > **Change Host** above the list.
![](https://main.qcloudimg.com/raw/1f82b3601ce7c933f174e1f0f48a105c.png)
:::
</dx-tabs>
5. In the pop-up window, select a destination host.
![](https://main.qcloudimg.com/raw/5fb36c2f82c0262a2be95460feb5fbbf.png)
6. Click **OK**.
Refresh the [**Dedicated Hosts**](https://console.cloud.tencent.com/cvm/cdh) page. You can see that the instances reside in another host after the migration, and they are shut down.
