## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to COS for data analysis and download. The process and architecture are as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/632ca05c1fa3c65507f1a89388427bc3.jpg)



## Prerequisites

Currently, this feature relies on the SCF and COS services, which should be activated first.

## Directions

### Creating task

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **EventBridge** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d05e333c479553515b07ee03292801ac.png)
> ?Before using SCF and EventBridge to process data, you need to read and agree to [SCF Description](https://intl.cloud.tencent.com/document/product/583) and [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
4. On the **Configure Task** page, enter the task details.
 ![](https://qcloudimg.tencent-cloud.cn/raw/33f48b5b33add35f1b94e73409b9d35d.png)  
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic.
   - Delivery Target: Select **COS**.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - Target Bucket: Select a COS bucket for the specific topic, where a file path named `instance-id/topic-id/date/timestamp` will be automatically created for message storage. If this path cannot meet your business needs, modify it under `CkafkaToCosConsumer` after completing the creation.
   - Aggregation Mode: Select either or both of the aggregation modes for the files to be aggregated to the COS bucket. For example, if you specify that files are aggregated once every hour and once every 1 GB, files will be aggregated every time either of the conditions is met.
   - Role Authorization: You need to grant permissions to a third-party role to access SCF and EventBridge.
   - SCF Authorization: Indicate your consent to activating SCF and EventBridge and create a function. Then, you need to go to the function settings to set more advanced configuration items and view monitoring information.
4. Click **Submit**.



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
- This feature is provided based on the SCF service that offers a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
- The fees of the dumping scheme is subject to the number of CKafka partitions, which is currently the same as the number of concurrent functions. If you want to modify the number of concurrent functions, check the logic of the `schedule` function.
