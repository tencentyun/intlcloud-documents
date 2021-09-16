## Overview
This document describes how to create a tracking set and ship logs in the CloudAudit console.

## Directions

1. Log in to the CloudAudit console and select **[Tracking Set](https://console.cloud.tencent.com/cloudaudit/audit)** on the left sidebar.
2. On the **Tracking Set** page, click **Create** as shown below:
![](https://main.qcloudimg.com/raw/af55c793d8045210b777fde74bb3b486.png)
3. On the **Create Tracking Set** page, enter the following main information as shown below:
![](https://main.qcloudimg.com/raw/1355e3ac456af9f5d63218ee454fa605.png)
 - **Basic Info**: enter a custom tracking set name.
 - **Manage Event**: you can filter events by **event type** and **resource type** or further select **All events** or **Some events** for filtering and shipping.
 - **Shipping Location**:
    - Ship the event to CLS: you can directly create a new log topic or select an existing one for log shipping. For more information on how to use CLS, please see [Getting Started in 5 Minutes](https://intl.cloud.tencent.com/document/product/614/31592).
    - Ship the event to a COS bucket: you can directly create a new bucket or select an existing one for log shipping. For more information on how to use buckets, please see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/38493).
4. Click **Creation completed** to create the tracking set. After about 10 minutes, logs will be shipped normally.


