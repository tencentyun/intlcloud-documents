TencentDB for MongoDB allows you to adjust the instance maintenance time in the console to meet the changes in your business requirements.

## Overview
Maintenance time is a very important concept for TencentDB for MongoDB. To ensure the stability of your TencentDB for MongoDB instance, the backend system performs maintenance operations on the instance during the maintenance time. We highly recommend you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.

In addition, we also recommend you perform operations involving data migration, such as adjusting the memory specification or AZ of mongod or mongos nodes, during the maintenance time. Taking the database instance AZ change as an example, as the full and incremental data needs to be synced to from the original AZ to the new AZ, data migration will be involved. After the AZ is changed, a momentary disconnection from the database may occur. When the task is initiated, the **Switch Time** can be selected as **During maintenance time**, so that the instance data migration will be started during the next **maintenance time** after the data sync is completed.

>?Before maintenance is carried out for TencentDB for MongoDB during the maintenance time, notifications will be sent to the contacts configured in your Tencent Cloud account through SMS and email.

## Version requirements
- Currently, TencentDB for MongoDB 4.4, 4.2, 4.0, 3.6, and 3.2 support maintenance time configuration.

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded cluster instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID to enter the **Instance Details** page.
6. On the **Instance Details** page, click **Modify** on the right of **Maintenance Time**.
7. In the **Modify Maintenance Time** window, set **Start Time** and **Duration**.
![](https://main.qcloudimg.com/raw/250f3544f118368d715fd017a7357fb6.png)
8. Click **OK**. You can view the newly set maintenance time on the **Instance Details** page.

