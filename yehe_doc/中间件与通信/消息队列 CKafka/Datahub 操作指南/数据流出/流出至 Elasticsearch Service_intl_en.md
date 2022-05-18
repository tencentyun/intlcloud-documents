## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to ES for the storage and search of massive amounts of data and real-time log analysis.
>?Only ES 7.0 and later are supported.

## Prerequisites

Currently, this feature relies on the ES service, which should be activated first.

## Directions

### Creating data distribution task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **Elasticsearch Service (ES)** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/da6a3b99adf759d3d5c8726bb6a0e7f5.png)
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic.
   - Source Data: The source data can be pulled.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - Instance Cluster: Select an ES instance cluster.
   - Instance Username: Enter the ES instance username, which is `elastic` and cannot be modified.
   - Instance Password: Enter the ES instance password.
   - Discard Message with Parsing Failure: A message parsing failure may occur if the message size exceeds 32 KB or if the message schema differs from that of the target index. If you don't discard the message that can't be parsed, exceptions may occur and data dumping will be stopped.
4. Click **Submit**.

### Viewing monitoring data

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.



## Restrictions and Billing

The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings.

  
