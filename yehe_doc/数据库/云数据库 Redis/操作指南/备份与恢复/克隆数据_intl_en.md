
## Overview
TencentDB for Redis Memory Edition master and replica instances (except v2.8) allow you to clone a complete instance from a backup file in both single-AZ and multi-AZ deployments. The clone instance has the same data as the backup file. You can use the clone feature to analyze historical data. You can also roll back an instance by swapping the IPs of the clone and original instances.

## Prerequisites
The instance data has been backed up. For backup directions, see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the instance management page, select the **Backup and Restoration** tab and click **Clone Instance** in the **Operation** column of the target instance.
![](https://main.qcloudimg.com/raw/e7a2efc796c7682829c9568b2f81fc32.png)
3. In the purchase window that pops up, configure relevant parameters and click **Buy Now**.
4. After the purchase is completed, you will be redirected to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.
>?After the instance is cloned, the original instance can be retained or terminated based on your needs.

