## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to ES for the storage and search of massive amounts of data and real-time log analysis.

## Prerequisites

Currently, this feature relies on the SCF and ES services which should be activated first before you can use this feature.

## Directions

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **EventBridge** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/74ec4768fadd95496c41b15fd031ba2b.png)
> ?Before using SCF and EventBridge to process data, you need to read and agree to [SCF Description](https://intl.cloud.tencent.com/document/product/583) and [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).
4. On the **Configure Task** page, enter the task details.
   ![](https://qcloudimg.tencent-cloud.cn/raw/456abbefa1e2efd620c7c4194bca8cdd.png)
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic.
   - Delivery Target: Select **ES**.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - On-Premises Cluster: If your Elasticsearch cluster is an on-premises cluster, toggle on this option and enter the instance IP. If your Elasticsearch cluster is an ES cluster, directly select the relevant cluster.
   - Instance Cluster: Select an ES instance cluster.
   - Instance Username: Enter the ES instance username, which is `elastic` and cannot be modified.
   - Instance Password: Enter the ES instance password.
   - SCF Authorization: Indicate your consent to activating SCF and EventBridge and create a function. Then, you need to go to the function settings to set more advanced configuration items and view monitoring information.
4. Click **Submit**.

### Viewing monitoring data

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.



## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings.
- The `CKafkaToES` scheme uses the CKafka trigger. For more information on related settings such as retry policy and maximum number of messages, see [CKafka Trigger Description](https://intl.cloud.tencent.com/document/product/583/17530).
- When the dump to ES feature is used, the dumped messages are the `msgBody` data of the CKafka trigger by default. If you want to process the logic by yourself, see [CKafka Trigger Description](https://intl.cloud.tencent.com/document/product/583/17530). 
- This feature is provided based on the SCF service that offers a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
