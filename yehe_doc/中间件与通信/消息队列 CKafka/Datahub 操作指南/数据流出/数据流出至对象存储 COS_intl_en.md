## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to COS for data analysis and download.

## Prerequisites

Currently, this feature relies on the COS service, which should be activated first.

## Directions

### Creating task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **Cloud Object Storage (COS)** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/38a38703ba6f352ff18e074e10414d2b.png)
4. On the **Configure Task** page, enter the task details.
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic. A data distribution task supports up to five source topics.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - Target Bucket: Select a COS bucket for the specific topic, where a file path named `instance-id/topic-id/date/timestamp` will be automatically created for message storage.
   - Aggregation Mode: Select either or both of the aggregation modes for the files to be aggregated to the COS bucket. For example, if you specify that files are aggregated once every hour and once every 1 GB, files will be aggregated every time either of the conditions is met.
> ! If the size of a single message exceeds the configured size of the aggregation file, the message may be truncated.
   - Storage Format: You can select CSV or JSON.
   - Role Authorization: You need to grant permissions to a third-party role to access COS.
5. Click **Submit**.



### Viewing monitoring data

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.


## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings or increase the number of CKafka partitions.
- The dump speed is subject to the size of a single CKafka file. A file exceeding 500 MB in size will be automatically split for multipart upload.
- Currently, you can only store messages to a COS bucket in the same region as the CKafka instance. For latency considerations, cross-region storage is not supported.
- For message dump to COS, the file content is composed by serializing the values in CKafka messages with UTF-8 strings. Binary data format is not supported currently.
- The operating account that enables message dump to COS must have write permission to the target COS bucket.
- You must have at least one VPC before you can dump messages to COS. If you choose the classic network during creation, bind a VPC as instructed in [Adding Routing Policy](https://intl.cloud.tencent.com/document/product/597/32555).
