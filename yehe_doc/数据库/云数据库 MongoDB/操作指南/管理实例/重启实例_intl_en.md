If the number of connections to an instance reaches the threshold or the instance has performance problems, you need to restart it manually. This document describes how to restart a replica set or sharded instance.

## Background
When the system becomes completely unavailable due to a high load, you can restart it to resume node operations. Due to the architecture of the TencentDB for MongoDB instance, instance restart divides into mongos restart and mongod restart.

- **mongos** is a routing service configured for MongoDB sharding. It processes query requests from the application layer and determines the location of data in a sharded cluster
- **mongod** is the primary daemon process for the MongoDB system. It handles data requests, manages data access, and performs background management operations.

## Version Description
- Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support instance restart.
- The architecture of MongoDB **4.0** replica set instance is simplified, where the mongos component is removed; therefore, instance restart doesn't involve mongos restart.

## Notes
- During restart, there may be one or two momentary disconnections for around 10s each. We recommend you configure an automatic reconnection feature for your application. 
- You cannot cancel an ongoing restart operation; therefore, proceed with caution.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB instance is in **Running** status.

## Directions 
**Restart one instance**
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. On the row of the target instance, click **Restart** in the **Operation** column.
![](https://main.qcloudimg.com/raw/5e704dbdbc5ab151bac6b57856a5f5e0.jpg)
6. In the **Restart MongoDB** window, click **View Details** to confirm the information of the instance to be restarted.
7. Select the components to be restarted and click **OK**.
8. In the instance list, you can see that the instance enters the **Restarting** status. Wait for the task to be completed.

**Batch restart instances**

1. In the instance list, select the instances to be restarted.
2. Above the instance list, click **Restart**.
3. In the **Restart MongoDB** window, click **View Details** to confirm the information of all the instances to be restarted.
4. Select the components to be restarted and click **OK**.
