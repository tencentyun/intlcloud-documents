## Overview

In scenarios such as offline data processing, sometimes it is necessary to reset the offset to consume earlier messages.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Consumer Group** and click **Offset Settings** in the **Operation** column.
4. In the **Offset Settings** window, select **Topic** or **Partition** as the dimension of settings and click **Next**.
5. Select the topic or partition for which to reset the offset (if no topic is selected, the offset will be reset for all topics by default) and click **Next**.
6. Specify the offset.
   ![](https://main.qcloudimg.com/raw/3a8511972c57dff28b7203fd285da2e3.png)

>!
>- The offset value should be between the minimum offset and the maximum offset. If it is configured to be smaller than the minimum offset, the consumption will start from the minimum offset; if it is larger than the maximum offset, the consumption will start from the maximum offset.
>- Make sure that there are no consumers in a consumer group before resetting the group.
