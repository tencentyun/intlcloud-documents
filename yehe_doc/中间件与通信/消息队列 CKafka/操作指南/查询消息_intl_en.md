## Overview

When encountering a consumption exception, you can troubleshoot the problem by querying the message in the CKafka console. This document describes how to query messages in the CKafka console.

The console supports query by offset and time, which are used in different scenarios:

- Query by offset: you know the ID of a topic's partition to which the message is sent and the offset of the message.
- Query by time: you are not sure about the offset of the message but know when the message is sent.

>! 
>- The console does not list all the messages after the specified time or offset. You can query at most 20 messages at a time.
>- Refrain from frequently querying as message querying also consumes bandwidth.

## Directions

### Query by offset

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/index?rid=1).
2. Select **Instance List** on the left sidebar, select a region, and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Topic Management** and click **More**> **Message Query** in the **Operation** column on the right of the target topic.
4. Select **Query by offset**, enter the partition ID and starting offset, and click **Query** to view the message details.
   ![](https://main.qcloudimg.com/raw/195ca10f4a0868b12a03c7c831eff1fd.png)
   - Partition ID: topic partition to which the message is sent
   - Offset: consumer offset of the message
   - Timestamp: `timestamp` in `ProducerRecord`
   - Operation: click **Message Details** to view the key and value of the message.
    ![](https://main.qcloudimg.com/raw/2d7d204213d422228a4a892a94496fe8.png)

   

### Query by time

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/index?rid=1).
2. Select **Instance List** on the left sidebar, select a region, and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, select **Topic Management** and click **More**> **Message Query** in the **Operation** column on the right of the target topic.
4. Select **Query by starting time**, enter the partition ID and time, and click **Query** to view the message details.
   If you select all partitions, messages of all partitions will be displayed; if you specify a partition, messages of the specified partition will be displayed.
   ![](https://main.qcloudimg.com/raw/7a2410794186b47c9126dbe8b878228d.png)
   - Partition ID: topic partition to which the message is sent
   - Offset: consumer offset of the message
   - Timestamp: `timestamp` in `ProducerRecord`
   - Operation: click **Message Details** to view the key and value of the message.
   ![](https://main.qcloudimg.com/raw/f033408d8698fbd24bab907cbc2af85a.png)



