## Overview

MongoDB uses change streams to track changes. However, to better search for change logs, you usually need to sync them to Elasticsearch or CLS.

![](https://qcloudimg.tencent-cloud.cn/raw/4689f690f7d5753e0fcdbe7142fca6ea.jpg)

This document uses connecting MongoDB to CKafka and distributing CKafka data to CLS as an example to describe how to use the data dump service of DataHub to analyze change logs tracked by change streams in MongoDB.

## How It Works

For more information on data access configuration items for MongoDB, see [Source Connector](https://docs.mongodb.com/kafka-connector/current/source-connector/). You can set different configuration items to perform corresponding data processing tasks on the accessed change logs and then write them to a topic in the CKafka instance.

## Prerequisites

- TencentDB for MongoDB has been activated, or CLB is used to listen on the self-built MongoDB instance.
![](https://qcloudimg.tencent-cloud.cn/raw/1386958ceb6ad238cde997d2c53eb722.png)
The TCP:27017 port has been opened in the security group.
![](https://qcloudimg.tencent-cloud.cn/raw/3a7a7593ecdedf07de2e087d0687d258.png)
- The CKafka service has been activated.
- The CLS service has been activated.

## Directions

### Step 1. Create a data access task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Access** on the left sidebar, select the region, and click **Create Task**.
3. In the pop-up window, select **Asynchronously pulled data** > **MongoDB** for **Data Source Type**.
![](https://qcloudimg.tencent-cloud.cn/raw/2733ca5e5b966bac82f1858962cc960c.png)
4. Click **Next** and enter the task details.
![](https://qcloudimg.tencent-cloud.cn/raw/a5647a8d101714a982858ff81c827f10.png)
5. Click **Submit** and wait for the task status to become **Healthy**.
![](https://qcloudimg.tencent-cloud.cn/raw/c3de44cecf13ba331b78914ebb100f53.png)
6. When MongoDB data changes, you can see that there will be incremental messages in the selected topic in the CKafka instance.
![](https://qcloudimg.tencent-cloud.cn/raw/94494e70d68682da95a83a3c3f56d124.png)

### Step 2. Create a data distribution task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **Cloud Log Service (CLS)** as the **Target Type** and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/49edecde6642832c3d7c2d57322ed672.png)
4. Enter the task details and select the same CKafka instance and topic as those used in the data access task, so that produced messages can be directly consumed.
![](https://qcloudimg.tencent-cloud.cn/raw/3d0e8a13995fcd325cf8e32a9b8dbbda.png)
5. Click **Submit** and wait for the task status to become **Healthy**.
![](https://qcloudimg.tencent-cloud.cn/raw/8f4ff805167b1b84d7dacc8c8dc4a333.png)
<dx-alert infotype="explain" title="">
When a task is in **Healthy** status and incremental messages are written to the topic, they will be directly consumed to the specified CLS log topic.
</dx-alert>



### Step 3. View the distributed data

1. Log in to the [CLS](https://console.intl.cloud.tencent.com/cls/overview?region=ap-guangzhou) console.
2. Select **Search and Analysis** on the left sidebar, select the logset ID and log topic ID entered during distribution task creation, and you can view the change logs of MongoDB.
![](https://qcloudimg.tencent-cloud.cn/raw/bb814dba5eac4aa46e9ad3f8732a7951.png)
3. You can search by keyword to directly get the required logs.
![](https://qcloudimg.tencent-cloud.cn/raw/f4d1f65187e45a9c40d92f590d192029.png)

