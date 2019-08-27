## Scenario
TencentDB for Redis Standard Edition (Community) supports restoration of an entire instance from a backup file.
	
>- Only Redis Standard Edition (Community) supports instance restoration, and Redis Cluster Edition (Community) supports [data clone](https://intl.cloud.tencent.com/document/product/239/31897).
>- Restoring an instance will interrupt the services provided by the instance.
>- After the instance is restored, the existing data will be overwritten and cannot be recovered.
>- If your instance has been ever degraded, you need to make sure that the instance specification is higher than the restored data capacity; otherwise, the restoration will fail.

## Prerequisites
The instance data has been backed up. For backup directions, see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Directions

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis) and click an instance name in the instance list to enter the instance details page.
2. On the **Backup and Restore** tab, select the backup you want to restore and click **Restore Instance**.
3. In the instance restoration window that pops up, enter the instance password and click **OK**.
> The password to be entered here is the instance password you set rather than the connection password in the format of "Instance ID:instance password" used for instance access.

![](https://main.qcloudimg.com/raw/9fbe5715735d89a93bf2cd36d5cde7df.png)
4. Return to the instances. The status of the instance is displayed as **Restoring backup by backup ID**. After the status changes to **Running**, it can be used normally.



