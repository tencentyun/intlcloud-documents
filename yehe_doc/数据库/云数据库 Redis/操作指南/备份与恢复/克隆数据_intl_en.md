## Operation Scenarios
TencentDB for Redis Memory Edition (excluding v2.8) supports instance clone, i.e., creating a complete instance based on a backup file. The data of the instance is the same as that in the backup file. You can use the clone feature to analyze previous data. You can also roll back an instance by swapping the IPs of the new instance and the original one.

## Prerequisites
The instance data has been backed up. For backup directions, please see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Directions
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and click an instance ID in the instance list to enter the instance management page.
2. On the instance management page, select the instance you want to clone and click **Clone Instance**.
![](https://main.qcloudimg.com/raw/e7a2efc796c7682829c9568b2f81fc32.png)
3. On the pop-up purchase page, specify the instance information based on your needs and click **Buy Now**.
4. After the purchase is completed, you will be redirected to the instance list. After the status of the instance changes to **Running**, the instance can be used normally.
>?After the instance is cloned, the original instance can be retained or terminated based on your needs.

