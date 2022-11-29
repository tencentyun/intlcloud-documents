## Overview

You can set a traffic throttling policy for a topic to prevent its excessive traffic from affecting other topics.

<dx-alert infotype="explain" title="">
You can set topic traffic throttling policies only for instances with a broker on v1.1.1 and v2.4.x.
</dx-alert>

## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Topic Management**.
4. In the **Operation** column, click **More** > **Traffic Throttling** and set the threshold.
  ![](https://qcloudimg.tencent-cloud.cn/raw/3963798dd53c757c0a4f72f24e66d34b.png)
  - Max Topic Production Traffic: This value excludes replica traffic and ranges from 1 MB/s to the maximum bandwidth purchased for the instance / number of replicas of the topic.
  - Max Topic Consumption Traffic: This value ranges from 1 MB/s to the maximum bandwidth purchased for the instance.

> ?
> 
> - The underlying code throttles the broker traffic. The actual throttling threshold (which is an integral multiple of the broker count) may differ slightly from the threshold you set.
> - For more information on the soft traffic throttling mechanism, see [Traffic Throttling](https://intl.cloud.tencent.com/document/product/597/39874).
