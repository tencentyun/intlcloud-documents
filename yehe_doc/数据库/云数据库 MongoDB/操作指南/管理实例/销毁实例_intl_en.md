If you no longer need a TencentDB for MongoDB instance, you can directly terminate and return it in the console.

## Background
You can terminate an instance if you no longer need it. The terminated instance will be put into the recycle bin. For instances in the recycle bin, you can restore or release them as needed based on different scenarios. 

## Version Requirement
- Currently, TencentDB for MongoDB 4.4, 4.2, 4.0, 3.6, and 3.2 support instance termination.

## Billing
- After a pay-as-you-go instance is returned, it will be moved to the recycle bin and retained there for three days. During the retention period, the instance cannot be accessed, but it can be restored after [top-up](https://intl.cloud.tencent.com/zh/document/product/555/7425).


## Notes
After an instance is completely terminated, its data will be cleared and cannot be recovered. You need to back up the data in advance.

## Instructions
- When an instance is terminated, its read-only instances will not be terminated simultaneously.
- After an instance is terminated, it will be moved to the recycle bin. During the retention period, the instance cannot be accessed, but it can be restored as instructed in [Recycle Bin](https://intl.cloud.tencent.com/document/product/240/44553).
- When an instance is terminated, its IP resources will be released simultaneously, and its disaster recovery instance will stop the sync connection and be automatically promoted to primary instance.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB instance is in **Running** status.

## Directions

 ### Pay-as-you-go instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **More** > **Terminate**.
6. In the pop-up window, read the prompt message carefully, confirm the instance to be terminated, and click **OK**.

## Recycle Bin
Terminated instances will be put into the recycle bin and can be restored during the retention period as instructed in [Recycle Bin](https://intl.cloud.tencent.com/document/product/240/44553).
