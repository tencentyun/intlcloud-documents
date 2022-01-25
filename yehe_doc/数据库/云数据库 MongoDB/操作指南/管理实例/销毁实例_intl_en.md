If you no longer need a TencentDB for MongoDB instance, you can directly terminate and return it in the console.

## Background
If you no longer need an instance, you can terminate it. The terminated instance will be put into the recycle bin. For instances in the recycle bin, you can restore or release them as needed based on different scenarios. 

## Version Description
- Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance termination.

## Notes
- After a pay-as-you-go instance is returned, it will be directly terminated without a retention period; therefore, proceed with caution.
- After an instance is completely terminated, its data will be cleared and cannot be recovered. You need to back up the data in advance.

## Notes
- When an instance is terminated, its read-only instances will not be terminated simultaneously.
- When an instance is terminated, its IP resources will be released simultaneously, and its disaster recovery instance will stop the sync connection and be automatically promoted to primary instance.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB instance is in **Running** status.

## Directions

 ### Pay-as-You-Go instance
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **More** > **Terminate**.
6. In the pop-up window, read the prompt message carefully, confirm the instance to be terminated, and click **OK**.
>!A pay-as-you-go instance will be directly terminated without a retention period, and all its data will be cleared and cannot be recovered. Therefore, proceed with caution.
>
![](https://main.qcloudimg.com/raw/b0d642108a455149b47158c059521ea2.png)

