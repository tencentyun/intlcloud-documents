
Terminated instances will be put into the recycle bin and can be restored.

## Background
Tencent Cloud recycle bin offers a mechanism for repossessing cloud resources. If your account balance is sufficient, you can restore terminated instances that are still in the recycle bin.

## Version description
Currently, all TencentDB for SQL Server versions support instance repossession.

## Notes
Instance repossession is as described below:
- **For pay-as-you-go instances in the recycle bin:**
 - **Retention period:** If your account has no overdue payments, terminated instances will be retained in the recycle bin for 24 hours.
 - **Expiration processing**: Instances that are not renewed before the retention period of 24 hours ends will be released and cannot be restored.

## Prerequisites
- The TencentDB for SQL Server instance has been terminated.
- Your Tencent Cloud account balance is sufficient.

## Restoring an instance from the recycle bin
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. On the left sidebar, select **SQL Server** > **Recycle Bin**.
3. Select the region at the top of the recycle bin page.
4. Select the target instance and click **Restore** in its **Operation** column or at the top.
![](https://qcloudimg.tencent-cloud.cn/raw/9d756037402f4d4df2aec75f65836435.png)
5. In the pop-up window, confirm the instance information and click **OK**.

## Eliminating an instance
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. On the left sidebar, select **SQL Server** > **Recycle Bin**.
3. Select the region at the top of the recycle bin page.
4. Find the target instance and click **Eliminate Now** in its **Operation** column.
5. In the pop-up window, confirm the instance information and click **OK**.
>!The instance will be completely eliminated, and its data will not be recoverable. Therefore, you need to back up the data in advance.

