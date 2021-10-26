## Overview

Topic is a category name where messages are stored and published. With CKafka, producers write messages to topics, and consumers read messages from topics. To enable horizontal scaling, a topic is divided into multiple [partitions](https://intl.cloud.tencent.com/document/product/597/32275). This allows you to horizontally scale your resources by adding more partitions in case of performance bottlenecks.

This document describes how to manage the topics under an existing instance in the CKafka console.

## Directions

### Creating a topic

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the **Instance List**, click the **ID/Name** of your instance to enter the instance details page.
3. On the instance details page, select **Topic Management** and click **Create**.
4. In the **Create Topic** dialog box, set parameters as needed.
   ![](https://main.qcloudimg.com/raw/b059e7bddbb29b16b9449e1dbbcf1b4d.png)

- Name: topic name, which cannot be changed once entered and can contain only letters, digits, underscores (_), hyphens (-), and dots (.).
- Partition Count: partition is the actual unit of storage. A topic can contain one or multiple partitions. CKafka allocates resources by partition.
- Replica Count: the number of partition replicas, which ensure the availability of partitions. For data reliability concerns, CKafka does not support single-replica topics currently. 2 replicas are created by default.
  Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
- Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.

5. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/e7bc2169b2d7985f287854f509f330c0.png)

### Viewing topic details

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** to view the topic information and enter the topic list page.
4. On the topic list page, click the right triangle icon on the left of the topic name to view the topic details.
   ![](https://main.qcloudimg.com/raw/6fea6378fa2710a6f8083723e1849601.png)

| Item      | Description                                                         |
| ----------- | ------------------------------------------------------------ |
| Partition Name   | Partition name                                              |
| Leader     | The leader processes all read/write requests in the partition, and the follower passively and periodically copies the data on the leader. |
| Replica       | Replica list                                                     |
| ISR        | Replicas with synced messages                                             |
| Start Offset | The last position of message consumption                                           |
| End Offset | The last position of message write. If the end offset is greater than the start offset, there are messages that have not been consumed yet |
| Messages     | Number of stored messages                                               |
| Unsynced Replicas | Number of unsynced replicas. You can filter partitions with unsynced replicas          |

### Deleting a topic

> !
>
>- Deleting a topic will delete the messages stored in the topic too. Please do so with caution.
>- Topic deletion is an async operation. After you finish the steps required to delete a topic, it takes 1 minute for the configuration to take effect with ZooKeeper. During this period, if you try to create a topic with the same name as the deleted one, the system will return the error code `[4000]10011`. Please wait and try again later.

1. In the instance list, click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Delete** in the **Operation** column.
3. In the window that pops up, click **Confirm** to delete the topic.



### Configuring advanced topic parameters

1. In the instance list, click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management**.
3. In the **Operation** column, click **Edit** > **Show advanced configuration** and set the following parameters:
   ![](https://main.qcloudimg.com/raw/52c8c0c4e99edd52247c1152129e5ddd.png)

The parameters are described as follows:

| Parameter                         | Default Value                   | Valid Values         | Note                                                         |
| :----------------------------- | :----------------------- | :--------------- | :----------------------------------------------------------- |
| cleanup.policy                 | delete                   | delete/compact   | Logs can be deleted by saving time or compacted by key. The compact mode is used for Kafka Connect. |
| min.insync.replicas            | 1                        | -                | When the "producer" sets `request.required.acks` to 1, `min.insync.replicas` will specify the minimum number of replicas. |
| unclean.leader.election.enable | true                     | true/false       | Whether to allow the setting of a replica not in the ISR set as the leader            |
| segment.ms                     | -                        | 1-90 days    | The period (ms) after which a segment is rolled, the minimum value being 86,400,000 ms.       |
| retention.ms                   | The message retention time of the instance | 60000 ms-90 days | Message retention time at the topic level                                   |
| max.message.bytes              | -                        | 1 KB - 12 MB         | Maximum message size at the topic level. If it is not set, the instance-level maximum message size (1 MB) is used by default. |

