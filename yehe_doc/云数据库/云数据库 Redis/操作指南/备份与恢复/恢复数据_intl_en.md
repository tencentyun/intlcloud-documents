
## Overview
TencentDB for Redis Memory Edition (v2.8) and CKV Edition support restoration of an entire instance from a backup file.
	
>?
>- Only TencentDB for Redis Memory Edition (v2.8) and CKV Edition support instance restoration. TencentDB for Redis Memory Edition excluding v2.8 supports [cloning data](https://intl.cloud.tencent.com/document/product/239/31897) instead.
>- Restoring an instance will interrupt the services provided by the instance.
>- After the instance is restored, the existing data will be overwritten and cannot be recovered.
>- If your instance has been ever downgraded, you need to make sure that the instance specification is higher than the restored data capacity; otherwise, the restoration will fail.

## Prerequisites
The instance data has been backed up. For backup directions, see [Backing up Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Backup and Restore** tab, locate the desired backup in the backup list, and click **Restore Instance** in the **Operation** column.
3. In the pop-up dialog box, confirm that everything is correct and click **OK**.
>!If the instance is password-protected, you need to enter the instance password on this page, which is the password you set on the instance purchase page rather than the connection password in the format of "instance ID:instance password" used for instance access.
>
4. Return to the instance list, where the status of the instance is displayed as **Restoring backup by backup ID**. After the status changes to **Running**, it can be used normally.

