## Overview

This document describes how to create a consumer group directly in the CKafka console.

> ? We recommend that you limit the number of consumer groups in each instance to 200 or less, since excess consumer groups will result in certain constraints.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Consumer Group** and click **Create**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ef4f61dd7ece6194858d084326e746d5.png)
4. In the pop-up window, enter the consumer group name and select the topic to subscribe to.
<dx-alert infotype="explain" title="">
You can select multiple topics.
</dx-alert>
5. Click **Submit**, and you can see the just created consumer group in the consumer group list.
