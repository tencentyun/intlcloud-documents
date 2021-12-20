
## Overview
TencentDB for Redis supports [read/write separation](https://intl.cloud.tencent.com/document/product/239/33132) for business scenarios with more reads but less writes, which can well cope with read requests concentrating on frequently read data. It supports up to 1-master 5-replica mode to offer 5x read performance.
>!
>- Enabling read/write separation may cause data read inconsistency (the data on replica nodes are older than that on the master node). Therefore, you need to check whether your business can tolerate data inconsistency first.
>- Disabling read/write separation may interrupt existing connections momentarily, so you are recommended to do so during off-peak hours.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Node Management** tab and click **Read-Only Replica** in the top-right corner to enable read/write separation.
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
3. In the pop-up window, select **Master Node** and/or **Replica Node**. If you select **Master Node**, the **Read-Only Replica** switch will be toggled on.
![](https://qcloudimg.tencent-cloud.cn/raw/518ee9eda54a17fa431dfc419cc2a899.png)
4. After confirming that everything is correct, click **OK**.
