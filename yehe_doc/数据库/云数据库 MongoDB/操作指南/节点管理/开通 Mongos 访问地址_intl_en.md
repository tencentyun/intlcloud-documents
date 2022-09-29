## Overview
After enabling the mongos access address of a sharded cluster instance, you can access the instance at this address. On the **Instance Details** page, you can see the mongos access connection string (for private network access).

## Notes
- Under the current VIP of the instance, different vports will be bound to different mongos nodes.
- After a mongos node fails, the system will bind its vport to a new mongos process, and the VIP and vport will remain unchanged.
- Enabling mongos access address won't affect the original CLB access address.

## Version requirements
TencentDB for MongoDB 4.0, 4.2 and 4.4 support enabling the mongos access address.

## Prerequisites
- Instance type: Sharded cluster instance.
- Instance status: Running.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Cluster Instance**.
3. Above the **Instance List** on the right, select the region.
4. In the **Instance List**, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Node Management** tab, click the **Mongos Node** tab.
7. On the **Mongos Node** tab, click **Enabling Mongos Access Address**.
8. In the pop-up window, confirm the impact of enabling the access address and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/5121594e7ee65fb519dafff43b662d14.png" style="zoom:80%;" />
7. On the left sidebar, select **Task Management**. In the task list, find the instance with the **Task Type** being **Enabling Node Access Address** by ID and wait for **Task Status** to become **Completed**.
8. On the left sidebar, select **Sharded Cluster Instance**. In the instance list, find the instance with the access address enabled, click its ID to enter the **Instance Details** page. In **Access Address** in the **Network Configuration** section, you can view the mongos access address. Hover over the connection string of the access address and click <img src="https://qcloudimg.tencent-cloud.cn/raw/036d66791d6ca5688900c92d7dc9a2cc.png" style="zoom:33%;" /> to copy it for mongos node access.
![](https://qcloudimg.tencent-cloud.cn/raw/5af9e87bc8812ef66990cd589efefe93.png)

