## Overview

This document describes how to create a consumer group directly in the CKafka console.

> ? We recommend you limit the number of consumer groups in each instance to 50 or less, since excess consumer groups will result in certain constraints.

## Directions

### Creating consumer group

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Consumer Group** and click **Create**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/ef4f61dd7ece6194858d084326e746d5.png)
4. In the pop-up window, enter the consumer group name and select the topic to subscribe to.
   <dx-alert infotype="explain" title="">
   You can select multiple topics.
   </dx-alert>
5. Click **Submit**, and you can see the just created consumer group in the consumer group list.



### Disabling automatic consumer group creation

CKafka allows you to disable automatic consumer group creation in the console. After it is disabled, only existing consumer groups in the console can be used for consumption, while new data sync tasks cannot be created normally.

![](https://qcloudimg.tencent-cloud.cn/raw/294107dd0591e3a0d9c46c8a9e9df61d.png)
<dx-alert infotype="explain" title="">
Only Pro Edition 2.4.1 and later are supported.
</dx-alert>
