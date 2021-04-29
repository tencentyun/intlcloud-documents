This document describes how to upgrade instance deployment from single-AZ to multi-AZ in the [TencentDB for Redis console](https://intl.cloud.tencent.com/document/product/239/39812).

## Step 1. Upgrade the Redis version to support multi-AZ deployment
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID/name in the instance list, and enter the instance management page.
2. On the **Instance Details** tab, click **Upgrade to Support Multi-AZ Deployment** next to **AZ**.
>?The upgrade will migrate only the metadata but not the business data. Usually, the upgrade completes in 3 minutes.
>
![](https://main.qcloudimg.com/raw/524e7c466ce7f226e30fd39da05fe09a.png)

## Step 2. Add replicas to replica AZs
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Replica** in the **Operation** column.
2. In the pop-up dialog box, specify replica AZs, and deploy the master node and replica nodes to different AZs.
>?Currently, the replicas of a multi-AZ deployed instance cannot be deleted.
>
![](https://main.qcloudimg.com/raw/e7ded5e0331bc5630283cfdf5eb55b8f.png)
