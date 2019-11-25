
## Introduction
CLS uses Ckafka instances to consume log topic data. This section describes how to enable Ckafka consumption feature for a log topic.

## Prerequisites

Tencent Cloud's Cloud Message Queue (CKafka) has been activated, and a Ckafka consumption instance and a message queue topic have been created in the same region with the log topic.

>For details about how to create a Ckafka instance, see [Creating Instances and Topics](https://cloud.tencent.com/document/product/597/30931).

## Directions

1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Logset Management** in the left sidebar.
3. Click the ID/name of the logset for which Ckafka consumption needs to be configured to go to its details page.
4. Locate the log topic to be consumed, and click **Configure** > **Real-Time Consumption** to go to the Ckafka consumption page.
![1](https://main.qcloudimg.com/raw/85294af3a9d71265e5cc535b17a58057.png)
5. Click **Edit** on the right of the page to configure Ckafka consumption.
6. Enable Ckafka consumption, and select the Ckafka instance for consumption and the relevant message queue topic.
![2](https://main.qcloudimg.com/raw/ebfac8224553db1011d0d14a3a812cb3.png)
7. Click **Save** to enable Ckafka consumption. If the status of Ckafka consumption is displayed as "Enabled", this means that it has been enabled successfully.
![](https://main.qcloudimg.com/raw/1ac6ee333d54e068451a68fbcf71af18.png)


