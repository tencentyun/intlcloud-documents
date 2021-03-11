## Overview

Topic is a category name where messages are stored and published. With CKafka, producers write messages to topics, and consumers read messages from topics. To enable horizontal scaling, a topic is divided into multiple [partitions](https://intl.cloud.tencent.com/document/product/597/32275). This allows you to horizontally scale your resources by adding more partitions in case of performance bottlenecks.

This document describes how to manage the topics under an existing instance in the CKafka console.

## Prerequisites
You have created an instance and a topic. For detailed instructions, see [Resource Preparation](https://intl.cloud.tencent.com/document/product/597/32543).

## Directions

### Creating a topic

1. In the **Instance List**, click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management**, and click **Create**.
3. In the **Create Topic** window, set the number of partitions and replicas and other parameters.
   ![](https://main.qcloudimg.com/raw/b7d7b48c3c552cb3e6205fb00cd5015b.png)
  - Name: the topic name, which cannot be changed once entered and can contain only letters, digits, “_”, “-” and “.”.
  - Partition Count: partition is the actual unit of storage. A topic can contain one or multiple partitions. CKafka allocates resources by partition.
  - Replica Count: the number of partition replicas, which ensure the availability of partitions. For data reliability concerns, CKafka does not support single-replica topics currently. 2 replicas are created by default.
    Replicas are counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas, then you have a total of 1 x 6 x 2=12 partitions.
  - Allowlist: if the allowlist is enabled, the topic can be accessed only from IP addresses in the allowlist, which ensures data security. You can enable allowlist in either the **Create Topic** or **Edit Topic** window.
4. Click **Submit** to complete the creation.
   ![](https://main.qcloudimg.com/raw/c98395f94e8a2b366f1543d9020030a7.png)

### Viewing a topic

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** in the left navigation pane and then the **ID/Name** of your instance to enter the instance details page.
3. On the instance details page, click **Topic Management** to view the topic information.
   ![](https://main.qcloudimg.com/raw/a5e634388b760cf7443488e680fa31ec.png)

### Deleting a topic

1. In the instance list, click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Delete** in the **Operation** column.
3. In the window that pops up, click **Confirm** to delete the topic.
   > !
   >- Deleting a topic will delete the messages stored in the topic too. Please do so with caution.
   >- Topic deletion is an async operation. After you finish the steps required to delete a topic, it takes 1 minute for the configuration to take effect with ZooKeeper. During this period, if you try to create a topic with the same name as the deleted one, the system will return the error code `[4000]10011`. Please wait and try again later.

 

 
 
 
    

### Configuring advanced topic parameters

1. In the instance list, click the **ID/Name** of your instance to enter the instance details page.
2. On the instance details page, select **Topic Management**.
3. In the **Operation** column, click **Edit** > **Show advanced configuration**, and set the following parameters:
   ![](https://main.qcloudimg.com/raw/5c2442c7a9fea573b4d58a542981283d.png)

Parameter description:

| Parameter                         | Default Value                   | Valid Values         | Note                                                         |
| :----------------------------- | :----------------------- | :--------------- | :----------------------------------------------------------- |
| cleanup.policy                 | delete                   | delete/compact   | Logs can be deleted by saving time or compacted by key. The compact mode is used for Kafka Connect. |
| min.insync.replicas            | 1                        | -                | When the producer sets `request.required.acks`, `min.insync.replicas` specifies the minimum number of replicas. |
| unclean.leader.election.enable | true                     | true/false       | Whether to allow the setting of a replica not in the ISR set as the leader            |
| segment.ms                     | -                        | 1-90 days    | The period (ms) after which a segment is rolled, the minimum value being 86,400,000 ms.       |
| retention.ms                   | The message retention time of the instance | 60000 ms-90 days | Message retention time at the topic level                                   |
| max.message.bytes              | -                        | 0-8 MB         | Maximum message size at the topic level. If it is not set, the instance-level maximum message size (1 MB) is used by default. |

