## Overview

This document describes how to send a message and view its record in message query after creating a topic in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Topic Management** and click **Send Message** in the **Operation** column.
   ![](https://qcloudimg.tencent-cloud.cn/raw/1f0c4e65ded79440077b0ddb9f8b843a.png)
   - Message Content: Enter the content of the message to be sent, which is required.
   - Message Key: Enter the sending key, which is optional.
   - Send to Specified Partition: This parameter supports sending messages to the specified partition, which is disabled by default.
4. Click **OK** to send the message. In the **Sent the message successfully** pop-up window, click **Message Query** to view the message just sent.

