This document describes how to upgrade instance deployment from single-AZ to multi-AZ in the [TencentDB for Redis console](https://intl.cloud.tencent.com/document/product/239/39812).

## Step 1. Upgrade the Redis version to support multi-AZ deployment
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance management page.
2. On the **Instance Details** page, click **Upgrade to Support Multi-AZ Deployment** next to **AZ**.
>?The upgrade will migrate only the metadata but not the business data. Usually, the upgrade can be completed in 3 minutes.
>
![](https://main.qcloudimg.com/raw/1fb0cc13e207c84446d64a3a725c5c1c.png)

## Step 2. Add replicas to replica AZs
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configuration Modification** > **Add Replica** in the **Operation** column.
2. In the pop-up window, specify replica AZs, and deploy the master node and replica nodes to different AZs.

![](https://main.qcloudimg.com/raw/d568fb5da499a4825a1e8fb516ea48db.png)
