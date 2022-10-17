## Overview
During daily maintenance, you can place your TencentDB for MongoDB and [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instances in the same AZ to lower the network latency. TencentDB for MongoDB multi-AZ instances support free AZ switch, and single-AZ instances support upgrade to multi-AZ instances.

## Billing
AZ modification doesn't affect instance billing.

## Notes
AZ modification may lead to primary-replica switch and a momentary disconnection for about 10 seconds; therefore, proceed during the off-peak hours of your business.

## Instructions
- All attributes, configurations, and connection addresses of the instance will stay unchanged after AZ modification. The private IP of the database will change after network switch, so you need to reconnect to the instance.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The instance is in **Running** status.
- The target AZ and the current instance AZ are in the same region.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the instance ID to enter the **Instance Details** page.
6. On the **Instance Details** page, click **Modify AZs after **AZ**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4629db162ff14b969af068b603b91a.png)
7. In the **Modify AZs** pop-up window, read the notes on AZ modification. For a multi-AZ deployed instance, configure different AZs for the primary and replica nodes respectively. For a single-AZ deployed instance, configure the same AZ for both the primary and replica nodes.
![](https://qcloudimg.tencent-cloud.cn/raw/d63435cb2498412a261bbc92d78baf9d.png)
> !
>- AZ modification may lead to primary-replica switch and a momentary disconnection of about 10 seconds; therefore, proceed during the off-peak hours of your business.
>-  To avoid increasing latency, after modifying the AZ of the primary node, you need to change the network of the primary node to one in the new AZ and modify its private IP as soon as possible.
8. Set AZs in the drop-down lists after **Primary Node** and **Replica Node** respectively.
9. Select the time for executing the AZ switch task after **Switch Time**. You can click **Learn more about switch time** and change the instance maintenance time to the off-peak hours of your business. For detailed directions, see [Setting Instance Maintenance Time](https://intl.cloud.tencent.com/document/product/240/31190).
> !If you have selected **During maintenance time**, do not select **Upon modification completion** to immediately execute the task before the configured maintenance time; otherwise, a program exception will occur. An initiated task cannot be stopped manually. To stop it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
> - **Upon modification completion**: The task will be executed immediately after the configuration is completed.
> - **During maintenance time**: The task will be executed during the maintenance time period.  
10. Click **OK**.
The instance status becomes **Modifying AZ**. Wait for the task to be completed, and you can see that the AZ has been modified.

## Subsequent operations
After modifying the AZ, switch the VPC subnet to avoid a high access latency. For detailed directions, see [Switching Instance Network](https://intl.cloud.tencent.com/document/product/240/44180).

