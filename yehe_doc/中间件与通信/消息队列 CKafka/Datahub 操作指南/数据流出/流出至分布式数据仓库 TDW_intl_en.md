

## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to TDW for data storage, query, and analysis.

## Prerequisites

Currently, this feature relies on the TDW service, which should be activated first.

## Directions

### Creating task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **Tencent Distributed Data Warehouse (TDW)** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/dd4438d05ea94348d2d4f62baf34662b.png)
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic.
   - Source Data: The source data can be pulled.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - TDW BID: Enter the TDW BID.
   - TDW TID: Enter the TDW TID.
4. Click **Submit**.



### Viewing monitoring data

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.


### Changing data source and data target

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. Click **Change Data Source** in the top-right corner of the **Data Source** module to modify the data source information.
4. Click **Change Data Target** in the top-right corner of the **Data Target** module to modify the data target information.

>?
>- The consumer group offset will not be reset after the data target is changed.
>- The data source and target cannot be modified if the task is paused.


## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings or increase the number of CKafka partitions.
- The dump speed is subject to the size of a single CKafka file. A file exceeding 500 MB in size will be automatically split for multipart upload.
