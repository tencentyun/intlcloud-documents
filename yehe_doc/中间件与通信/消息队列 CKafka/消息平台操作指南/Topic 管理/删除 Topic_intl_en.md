## Overview

This document describes how to delete a topic in the CKafka console.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Topic Management** and click **Delete** in the **Operation** column.
4. In the window that pops up, click **OK** to delete the topic.


> !
> - Deleting a topic will also delete the messages stored in the topic. Do so with caution.
> - Topic deletion is an async operation. After you finish the steps required to delete a topic, it takes 1 minute for the configuration to take effect with ZooKeeper. During this period, if you try to create a topic with the same name as the deleted one, the system will return the error code `[4000]10011`. Wait and try again later.
