## Overview

**CKafka Pro Edition** supports advanced Ops features. You can view the number of TCP connections, unsynced replica details, and topic/consumer group rankings in the console, making it easier for you to troubleshoot CKafka issues.


## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the instance list, select a region and click the **ID/Name** of the target instance to enter the instance details page.
3. At the top of the instance details page, click **Dashboard** and set the time range to view related ranking information.
   - TCP Connections: it displays the total number of TCP connections to the current broker. It allows you to view the connections to each server more easily when the number of instance connections is about to be used up.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ab57a66654eac5ceea9de5aebddaf858.png)
   - Details of Unsynced Replicas: it displays the details of unsynced replicas.
     ![](https://qcloudimg.tencent-cloud.cn/raw/be1818c8e76394851da1e0507f86e3b1.png)
   - Ranking:
     - Topic: it displays the top 10 topics in terms of production and consumption traffic as well as disk usage.
       ![](https://qcloudimg.tencent-cloud.cn/raw/405243f8a514f985c33c18807cc44c97.png)
     - Consumer Group: it displays the top 10 consumer groups in terms of consumption speed.
         ![](https://qcloudimg.tencent-cloud.cn/raw/03f6ec784d56e2893851dc6afbb8711f.png)
