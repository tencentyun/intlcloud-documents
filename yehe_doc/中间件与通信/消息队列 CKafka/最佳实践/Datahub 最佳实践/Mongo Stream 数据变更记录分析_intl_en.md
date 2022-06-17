## Overview

MongoDB uses change streams to track changes. However, to better search for change logs, you usually need to sync them to Elasticsearch or CLS.

![](https://qcloudimg.tencent-cloud.cn/raw/a808d4924bf5f10c029caa5f1bc7f81a.png)

This document uses connecting MongoDB to CKafka and distributing CKafka data to CLS as an example to describe how to use the data dump service of DataHub to analyze change logs tracked by change streams in MongoDB.

## How It Works

For more information on data access configuration items for MongoDB, see [Source Connector](https://docs.mongodb.com/kafka-connector/current/source-connector/). You can set different configuration items to perform corresponding data processing tasks on the accessed change logs and then write them to a topic in the CKafka instance.

## Prerequisites

- TencentDB for MongoDB has been activated, or CLB is used to listen on the self-built MongoDB instance.
The TCP:27017 port has been opened in the security group.
- The CKafka service has been activated.
- The CLS service has been activated.

## Directions

### Step 1. Create a data access task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Access** on the left sidebar, select the region, and click **Create Task**.
3. In the pop-up window, select **Asynchronously pulled data** > **MongoDB** for **Data Source Type**.
4. Click **Next** and enter the task details.
5. Click **Submit** and wait for the task status to become **Healthy**.
6. When MongoDB data changes, you can see that there will be incremental messages in the selected topic in the CKafka instance.

### Step 2. Create a data distribution task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **Cloud Log Service (CLS)** as the **Target Type** and click **Next**.
4. Enter the task details and select the same CKafka instance and topic as those used in the data access task, so that produced messages can be directly consumed.
5. Click **Submit** and wait for the task status to become **Healthy**.
<dx-alert infotype="explain" title="">
When a task is in **Healthy** status and incremental messages are written to the topic, they will be directly consumed to the specified CLS log topic.
</dx-alert>



### Step 3. View the distributed data

1. Log in to the [CLS](https://console.intl.cloud.tencent.com/cls/overview?region=ap-guangzhou) console.
2. Select **Search and Analysis** on the left sidebar, select the logset ID and log topic ID entered during distribution task creation, and you can view the change logs of MongoDB.
3. You can search by keyword to directly get the required logs.

