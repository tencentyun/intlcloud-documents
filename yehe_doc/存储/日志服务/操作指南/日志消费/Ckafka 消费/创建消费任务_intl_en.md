
## Overview
CLS uses Ckafka instances to consume log topic data. This section describes how to enable Ckafka consumption feature for a log topic.

## Prerequisites

Tencent Cloud CKafka has been activated, and a Ckafka consumption instance and a message queue topic have been created in the same region as the log topic.

>For details about how to create a Ckafka instance, see [Creating Instances](https://intl.cloud.tencent.com/document/product/597/40039).

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset** in the left sidebar.
3. Click the logset name/ID for which Ckafka consumption needs to be configured to go to its details page.
4. Find the log topic to be consumed, and click **Manage** on the right to enter the log topic management page.
![](https://main.qcloudimg.com/raw/04759d7e7f2d6db0b0249c4393b5edd5.png)
5. Select the **Ckafka Consumption** tab.
6. Click **Edit** on the right. Toggle the switch to enable **Ckafka Consumption**, and select a Ckafka instance for consumption and a corresponding message queue topic.
![](https://main.qcloudimg.com/raw/43a9878b5bf8f0500c1ba19b668b7766.png)
7. Click **Save** to enable Ckafka consumption. If the status of Ckafka consumption is displayed as "Enabled", it has been enabled successfully.
![](https://main.qcloudimg.com/raw/f964f0a141123a7926b8fd1a1eb1b5ba.png)




