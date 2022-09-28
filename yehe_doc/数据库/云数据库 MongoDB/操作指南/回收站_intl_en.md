Terminated instances will be put into the recycle bin and can be restored.

## Background
Tencent Cloud recycle bin offers a mechanism for repossessing cloud services. If your account balance is sufficient, you can restore terminated instances that are still in the recycle bin.

## Version Requirement
Currently, TencentDB for MongoDB 4.4, 4.2, 4.0, 3.6, and 3.2 support instance repossession.

## Notes
For pay-as-you-go instances in the recycle bin:

- **Retention period:** If your account has no overdue payments, terminated instances will be retained in the recycle bin for three days.
- **Expiration processing**: Instances that are not renewed before the retention period ends will be released and cannot be restored.
>! 
>- After the account balance becomes 0, instances will be automatically shut down and moved from the instance list to the recycle bin, and the billing will stop in 24 hours.
>- You cannot restore pay-as-you-go instances from the recycle bin if your account has overdue payments. You need to top up your account first.
>- Pay-as-you-go instances are retained in the recycle bin for a maximum of three days. You need to top up your account in time to restore the instances.
:::
</dx-tabs>

## Prerequisites
- The TencentDB for MongoDB instance has been terminated.
- Your Tencent Cloud account balance is sufficient.

## Directions
You can **renew**, **restore**, or **eliminate** instances in the recycle bin.

### Viewing instance in recycle bin
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. On the left sidebar, select **MongoDB** > **Recycle Bin**.
3. Above the instance list on the right, select the region.
4. On the **Recycle Bin** page on the right, you can see the list of instances in the recycle bin.
![](https://qcloudimg.tencent-cloud.cn/raw/432ff053e452a206313e04031caab3f2.png)

### Restoring one instance
1. In the instance list in the recycle bin, find the target instance and click **Restore** in the **Operation** column.
2. In the **Restore Instance** window, confirm the instance information and click **OK**.
The instances will return to the instance list in the replica set or sharded cluster from the recycle bin.

### Batch restoring instances
1. In the instance list in the recycle bin, select the target instances.
2. Click **Batch Restore** above the list, confirm the instance information in the **Restore Instance** window, and click **OK**.
The instances will return to the instance list in the replica set or sharded cluster from the recycle bin.

### Eliminating instance
1. In the instance list in the recycle bin, find the target instance and click **Eliminate Now** in the **Operation** column.
2. In the **Instance Elimination** window, confirm the instance information and click **OK**.
> !The instance will be completely eliminated, and its data will not be recoverable. Therefore, you need to back up the data in advance.

