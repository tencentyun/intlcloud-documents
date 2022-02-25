You can flexibly switch the AZ in the TencentDB for MongoDB console based on your business needs.

## Background
During daily maintenance, you can place your TencentDB for MongoDB and [CVM](https://intl.cloud.tencent.com/document/product/213/10517) instances in the same AZ to lower the network latency. TencentDB for MongoDB multi-AZ instances support free AZ switch, and single-AZ instances support upgrade to multi-AZ instances.

## Version Description
TencentDB for MongoDB 4.2 doesn't support AZ modification.

## Billing Description
AZ modification doesn't affect instance billing.

## Precautions
- AZ modification may lead to primary/secondary switch and a momentary disconnection of about 10 seconds; therefore, proceed during the off-peak hours of your business.
- After AZ modification, you must change the network to the IP of the new AZ; otherwise, the request latency will increase.

## Notes
All instance attributes, configurations, and connection address will stay unchanged after AZ modification.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The instance is in **Running** status.
- The target AZ and the current instance AZ are in the same region.
- The instance version is TencentDB for MongoDB 4.0, 3.6, or 3.2.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the instance ID to enter the **Instance Details** page.
6. In the **Basic Info** section on the **Instance Details** page, click **Modify AZs** after **AZ**.
![](https://qcloudimg.tencent-cloud.cn/raw/7e4629db162ff14b969af068b603b91a.png)
7. In the **Modify AZs** window, read the prompt carefully and confirm AZ modification.
> !
>-  AZ modification may lead to primary/secondary switch and a momentary disconnection of about 10 seconds; therefore, proceed in off-peak hours of your business.
>-  To avoid increasing latency, after modifying the AZ of the primary node, you need to change the network of the primary node to one in the new AZ and modify its private IP as soon as possible.
8. Set AZs in the drop-down lists after **Primary Node** and **Secondary Node** respectively.
9. Select the time for executing the AZ switch task after **Switch Time**.
  - **Upon modification completion**: the task will be executed immediately after the configuration is completed.
  - **During maintenance time**: the task will be executed during the maintenance time period.
11. Click **OK**.
The **Instance Status** in **Basic Info** becomes **Switching AZ**. Wait for the task to be completed, and you can see that the AZ has been modified.


