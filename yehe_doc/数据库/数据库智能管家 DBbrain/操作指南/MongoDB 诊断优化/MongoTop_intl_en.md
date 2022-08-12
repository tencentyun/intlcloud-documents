## Overview
To facilitate daily database Ops, DBbrain provides the TencentDB for MongoDB MongoTop tool. Like MongoDB's official tool, this tool allows you to view the monitoring data of top tables at the node level in real time.

## Directions
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/performance/monitor) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Performance Trends** tab.
2. Select **Mongod Node** > **MongoTop**.
3. Select a node in the drop-down list.
4. Click **Pause** in the top-right corner to pause and view the data.
![](https://qcloudimg.tencent-cloud.cn/raw/e6fd5fffae929639c5367ef3a0a5d467.png)

## MongoTop table monitoring fields
MongoTop fields are as described below:
- **Time:**
Current time of the database.

- **ns:**
Namespace of the database.

- **total:**
The total time mongod spent in the namespace.

- **read:**
The time spent by mongod performing read operations in the namespace.

- **write:**
The time spent by mongod performing write operations in the namespace.

  
