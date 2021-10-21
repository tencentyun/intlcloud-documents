## Overview

If the current instance specifications cannot meet your business needs, you can upgrade them in the console.

> ?
> - The instance specifications you can upgrade include peak bandwidth, disk capacity, and the number of topics/partitions. You can also increase the disk capacity only. The upgrade is smooth without suspending your services.
> - A topic currently consists of up to 24 partitions. To increase the partition limit (which can be increased to 500 at most), please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Prerequisites

Please check the following before upgrading:

1. Check whether the instance has unavailable public network routes, supporting networks, VPC networks, etc. For more information, please see [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
2. Check whether the instance has unsynced replicas. For more information, please see [Topic Management](https://intl.cloud.tencent.com/document/product/597/32554).
3. Check whether the instance has unfinished tasks (data migration), exceptionally created topics, exceptionally deleted topic data, etc.

If there are unfinished tasks, we recommend you wait for all the tasks to be completed before upgrading. If task execution is exceptional, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Directions

### Standard Edition

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Operation** column on the instance list page, select **More** > **Upgrade** to enter the upgrade page.
3. Select the target specifications for the instance.
   ![](https://main.qcloudimg.com/raw/1856e04396a4228368329885bc766e9d.png)
4. Click **Submit** to complete the instance upgrade.

### Pro Edition

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Operation** column on the instance list page, select **More** > **Upgrade** to enter the upgrade page.
3. Select the target specifications for the instance.
   ![](https://main.qcloudimg.com/raw/80704895f876dddeee2fecb6496dcf94.png)
	- Product Specs: select an appropriate model based on the peak bandwidth and disk capacity.
	- Instance Price: you need to pay for the upgrade based on the number of days.
	- Rebalance Time:
		- If the backend recognizes that data migration is required during the upgrade, you can choose to upgrade right away or at specified time (upgrade at night is recommended to reduce the impact on your business). The estimated upgrade duration is calculated by backend APIs.
			![](https://main.qcloudimg.com/raw/98f3c20193e67fdb65799739b2cc234c.png)
		- If the backend recognizes that data migration is not required during the upgrade, you will see the note "Rebalancing will not occur during the upgrade".
			![](https://main.qcloudimg.com/raw/e0d6ebe815789cb0827a021c1f40d548.png)
	- Upgrade Mode: if the backend recognizes that instance migration is required during the upgrade, you can select an upgrade mode as needed. Otherwise, you do not need to select an upgrade mode.
		- Stable: CKafka will limit the speed of data migration during the downgrade to ensure that instances have optimal bandwidth performance. This option is recommended if you do not want to affect business operations.
		- High-Speed: CKafka will not limit the speed of data migration during the upgrade, thus affecting the bandwidth available for data production and consumption of instances. This option is recommended for off-peak hours or when service suspension is allowed.
4. Click **Submit** to complete the instance upgrade. You can view the upgrade progress in the **Status** column.
5. If you choose to upgrade at the specified time, you can modify the time you specified in the **Status** column.


## Possible Causes of Upgrade Failures

1. The disk resources in the current AZ cannot meet the requirements of this upgrade. We recommend you contact the Tencent Cloud customer service to check whether there are sufficient resources.

2. If the high-speed mode is selected during instance upgrade, and there are production tasks that use a lot of bandwidth resources in the cluster, the data migration delay will increase. You can view the [monitoring data](https://intl.cloud.tencent.com/document/product/597/12167) to see whether there are excessive peaks of the production and consumption traffic during the upgrade.

3. The upgrade process takes too long. The maximum acceptable message byte size of the migrated server configuration is 1 MB, but the broker configuration that needs to be migrated is 8 MB, so the broker cannot receive oversized message migration, resulting in prolonged data migration. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

4. During the upgrade or migration between the new and old clusters, the broker IP update is exceptional, causing the broker IP of the new cluster to fail to pull data. You can view the [monitoring data](https://intl.cloud.tencent.com/document/product/597/12167) to see that there is no monitoring data for a period of time. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
