Terminated instances will be put into the recycle bin and can be restored.

## Background
Tencent Cloud recycle bin is a cloud service repossession mechanism. When your account balance is sufficient, if you need to restore terminated instances, you can do so during the retention period.

## Version Description
Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance repossession.

## Notes
The repossession of pay-as-you-go instances is as described below:

<dx-tabs>
::: Pay-as-You-Go instances in the recycle bin

- **Retention period:** if your account has no overdue payments, terminated instances will be retained in the recycle bin for 3 days.
- **Expiration processing**: instances that are not renewed before the retention period ends will be released and cannot be restored.
>! 
>- If your account has overdue payments, pay-as-you-go instances will not be put into the recycle bin.
>- You cannot restore pay-as-you-go instances in the recycle bin if your account has overdue payments. You need to top up your account first.
>- Pay-as-You-Go instances are retained in the recycle bin for a maximum of 3 days. Pay attention to the release time and top up your account in time to restore the instances.
:::
</dx-tabs>

## Prerequisites
- Your TencentDB for MongoDB instance has been terminated.
- Your Tencent Cloud account balance is sufficient.

## Directions
Instances in the recycle bin can be **renewed**, **restored**, or **eliminated**.

### Viewing instance in recycle bin
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. On the left sidebar, select **MongoDB** > **Recycle Bin**.
3. Above the instance list on the right, select the region.
4. On the **Recycle Bin** page on the right, you can see the list of instances in the recycle bin.
![](https://qcloudimg.tencent-cloud.cn/raw/432ff053e452a206313e04031caab3f2.png)

### Restoring one instance
1. In the instance list in the recycle bin, find the target instance and click **Restore** in the **Operation** column.
2. In the **Restore Instance** window, confirm the instance information and click **OK**.
The instance will return to the instance list in the replica set or sharded cluster from the recycle bin.

### Batch restoring instances
1. In the instance list in the recycle bin, select the target instances.
2. Click **Batch Restore** above the list, confirm the instance information in the **Restore Instance** window, and click **OK**.
The instances will return to the instance list in the replica set or sharded cluster from the recycle bin.

### Eliminating instance
1. In the instance list in the recycle bin, find the target instance and click **Eliminate Now** in the **Operation** column.
2. In the **Instance Elimination** window, confirm the instance information and click **OK**.
> !The instance will be completely eliminated, and its data will not be recoverable. Therefore, you need to back up the data in advance.

