## Overview

In some cases, a consumer group may not consume for a long time before consuming again. You can delete it, so that when the consumers in it establish a connection again, the offset will be reset, and consumption will start from the beginning.

>?Only empty consumer groups with a broker version not below v1.1.1 can be deleted.

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Delete** in the **Operation** column of the consumer group to be deleted.
   ![](https://main.qcloudimg.com/raw/3c6499bf9e1aafd1f365fb084329f022.png)

