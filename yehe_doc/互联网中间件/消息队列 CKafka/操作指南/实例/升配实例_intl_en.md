## Overview

If the current instance specifications cannot meet your business needs, you can upgrade them in the console.

> ?
> - The instance specifications you can upgrade include peak bandwidth, disk capacity, and the number of topics/partitions. You can also increase the disk capacity only. The upgrade is smooth, without suspending your services.
> - A topic currently consists of up to 24 partitions. To increase the partition limit (which can be increased to 500 at most), please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Directions

### Standard edition

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the “Operation” column on the instance list page, select **More** > **Upgrade** to go to the **Upgrade Configuration** page.
3. Select the target specifications for the instance.
   ![](https://main.qcloudimg.com/raw/7ea4106988f184ee748138d5c7119937.png)
4. Click **Submit**.

### Pro edition

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the “Operation” column on the instance list page, select **More** > **Upgrade** to go to the **Upgrade Configuration** page.
3. Select the target specifications for the instance.
	 ![](https://main.qcloudimg.com/raw/7a834daee8c91b3b18ebbc8b9c9bbf3c.png)
	- Product Specification: select a model based on the peak bandwidth and disk capacity.
	- Instance Price: the price difference caused by the upgrade is made up by day. For details, see [Monthly Subscription and Product Configuration Upgrade](https://cloud.tencent.com/document/product/555/13001).
	- Rebalance Time:
		- If the backend recognizes that data migration is required during the upgrade, you can choose to upgrade right away or at specified time (upgrade at night is recommended to reduce the impact on your business). The estimated upgrade duration is calculated by backend APIs.
    ![](https://main.qcloudimg.com/raw/9bd0835122811c8617f5e51ecf43a8f9.png)
   - If the backend recognizes that data migration is not required during the upgrade, you will see the note “Rebalancing will not occur during the upgrade”.
    ![](https://main.qcloudimg.com/raw/5f665e54bc758196ddb414e793cb8d58.png)
	- Upgrade Mode: if the backend recognizes that instance migration is required during the upgrade, you can select an upgrade mode as needed. Otherwise, you do not need to select an upgrade mode.
  - Stable: CKafka will limit the speed of data migration during the downgrade to ensure that instances have optimal bandwidth performance. This option is recommended if you do not want to affect business operations.
  - High-speed: CKafka will not limit the speed of data migration during the upgrade, thus affecting the bandwidth available for data production and consumption of instances. This option is recommended for off-peak hours or when service suspension is allowed.
4. Click **Submit** to complete the instance upgrade. You can view the upgrade progress in the “Status” column.
   ![](https://main.qcloudimg.com/raw/0314f6f20bb7ea1b975a37d3af8c9e9e.png)
5. If you choose to upgrade at specified time, you can modify the time you specified in the “Status” column.
	 ![](https://main.qcloudimg.com/raw/d16c5d9313a23be5e8ba623c6487420f.png)
