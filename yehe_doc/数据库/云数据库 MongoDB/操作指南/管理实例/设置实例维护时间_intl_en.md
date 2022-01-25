TencentDB for MongoDB allows you to adjust the instance maintenance time in the console to meet the changes in your business requirements.

## Background
Maintenance time is a very important concept for TencentDB for MongoDB. To ensure the stability of your TencentDB for MongoDB instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

## Version Description
- Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support maintenance time configuration.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. In the **Configuration** section on the **Instance Details** page, click **Modify** on the right of **Maintenance Time**.
![](https://main.qcloudimg.com/raw/250f3544f118368d715fd017a7357fb6.png)
7. In the **Modify Maintenance Time** window, set **Start Time** and **Duration**.
8. Click **OK**. In the **Configuration** section on the **Instance Details** page, you can view the newly set maintenance time.

