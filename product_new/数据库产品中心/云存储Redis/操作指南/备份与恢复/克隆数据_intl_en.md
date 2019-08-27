## Scenario
TencentDB for Redis Cluster Edition (Community) supports instance clone, i.e., creating a complete instance based on a backup file. The data of the instance is the same as that in the backup file. You can use the clone feature to analyze previous data. You can also roll back an instance by swapping the IPs of the new instance and the original instance.

## Prerequisites
The instance data has been backed up. For backup directions, see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Directions
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance name in the instance list to enter the instance details page.
2. On the **Backup and Restore** tab, select the instance you want to clone and click **Clone Instance**.

3. In the purchase windows that pops up, configure the relevant parameters and click **Buy Now**.
4. Return to the instance list. After the status of the instance changes to **Running**, it can be used normally.
> After the instance is cloned, the original instance can be retained or terminated based on your needs.



