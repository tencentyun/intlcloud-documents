## Overview

DataHub offers data distribution capabilities. You can distribute CKafka data to CLS for business problem locating, metric monitoring, and security audit.

## Prerequisites

Currently, this feature relies on the SCF and CLS services, which should be activated first.

## Directions

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar, select the region, and click **Create Task**.
3. Select **EventBridge** as the **Target Type** and click **Next**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/165add1957b06dbd7684fe9f68658fd3.png)

> ?Before using SCF and EventBridge to process data, you need to read and agree to [SCF Description](https://intl.cloud.tencent.com/document/product/583) and [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).

4. On the **Configure Task** page, enter the task details.
   ![](https://qcloudimg.tencent-cloud.cn/raw/8041c40a6129d2b325cd2346272d0e5c.png)
   - Task Name: It can only contain letters, digits, underscores, or symbols ("-" and ".").
   - CKafka Instance: Select the source CKafka instance.
   - Source Topic: Select the source topic.
   - Delivery Target: Select **CLS**.
   - Starting Position: Select the topic offset of historical messages when dumping.
   - Logset: Select a logset. A logset is a project management unit in CLS and is used to distinguish between logs in different projects.
   - Log Topic: You can select **Auto-create log topic** or **Select from existing log topics**. One [logset](https://intl.cloud.tencent.com/document/product/614/32849) can contain multiple log topics, and one log topic corresponds to one type of applications or services. We recommend you collect similar logs on different machines into the same log topic.
   - Role Authorization: You need to grant permissions to a third-party role to access EventBridge.
4. Click **Submit**.

### Viewing monitoring data

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Data Distribution** on the left sidebar and click the **ID** of the target task to enter its basic information page.
3. At the top of the task details page, click **Monitoring**, select the resource to be viewed, and set the time range to view the corresponding monitoring data.



## Restrictions and Billing

- The dump speed is subject to the limit of the peak bandwidth of the CKafka instance. If the consumption is too slow, check the peak bandwidth settings or increase the number of CKafka partitions.
- The dump speed is subject to the size of a single CKafka file. A file exceeding 500 MB in size will be automatically split for multipart upload.
- This feature is provided based on the SCF service that offers a [free tier](https://intl.cloud.tencent.com/document/product/583/12282). For more information on the fees for excessive usage, see the [billing rules](https://intl.cloud.tencent.com/document/product/583/17299) of SCF.
