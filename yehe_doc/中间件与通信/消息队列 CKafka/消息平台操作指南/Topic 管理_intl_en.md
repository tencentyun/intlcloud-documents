## Overview

Topic is a category name where messages are stored and published. With CKafka, producers write messages to topics, and consumers read messages from topics. To enable horizontal scaling, a topic is divided into multiple [partitions](https://intl.cloud.tencent.com/document/product/597/32275). This allows you to horizontally scale your resources by adding more partitions in case of performance bottlenecks.

This document describes how to manage the topics under an existing instance in the CKafka console.

## Directions

### Creating topic

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** at the top and click **Create**.
4. In the **Create Topic** window, set the number of partitions and replicas and other parameters.
     ![](https://main.qcloudimg.com/raw/b059e7bddbb29b16b9449e1dbbcf1b4d.png)
   - Name: The topic name. It cannot be changed once entered and can contain only letters, digits, underscores, hyphens, and periods.
   - Partition Count: It is a concept in physical partition, where one topic can contain one or more partitions. CKafka uses partition as an allocation unit.
   - Replica Count: The number of partition replicas is used to ensure the high availability of the partition. To ensure data reliability, creating a single-replica topic is not supported. Two replicas are enabled by default.
     Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions, and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
   - **Tag**: Set a resource tag. For more information, see [Tag Overview](https://intl.cloud.tencent.com/document/product/597/41600).
   - Preset ACL Policy: Select the preset ACL policy. For more information on ACL policy, see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).
5. Click **Submit**.
   ![](https://main.qcloudimg.com/raw/e7bc2169b2d7985f287854f509f330c0.png)

### Viewing topic details

1. Log in to the [CKafka console](https://console.intl.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** to view the topic information and enter the topic list page.
4. On the topic list page, click the right triangle icon on the left of the topic name to view the topic details.
   ![](https://main.qcloudimg.com/raw/6fea6378fa2710a6f8083723e1849601.png)

<table>
    <thead>
    <tr>
        <th>Item</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Partition Name</td>
        <td>Partition name</td>
    </tr>
    <tr>
        <td>Leader</td>
        <td>The leader processes all read/write requests in the partition, and the follower passively and periodically copies the data on the leader</td>
    </tr>
    <tr>
        <td>Replica</td>
        <td>Replica list</td>
    </tr>
    <tr>
        <td>ISR</td>
        <td>Replicas with synced messages</td>
    </tr>
    <tr>
        <td>Start Offset</td>
        <td>The last position of message consumption</td>
    </tr>
    <tr>
        <td>End Offset</td>
        <td>The last position of message write</td>
    </tr>
    <tr>
        <td>Messages</td>
        <td>Number of stored messages</td>
    </tr>
    <tr>
        <td>Unsynced Replicas</td>
        <td>Number of unsynced replicas. You can filter partitions with unsynced replicas</td>
    </tr>
    </tbody>
</table>



### Sending messages

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Send Message** in the **Operation** column.
<<<<<<< HEAD
    ![](https://qcloudimg.tencent-cloud.cn/raw/1f0c4e65ded79440077b0ddb9f8b843a.png)
=======
>>>>>>> 4c0ee768bf0276e04d7ad55207e181473466eaf0
   - Message Content: Enter the content of the message to be sent, which is required.
   - Message Key: Enter the sending key, which is optional.
   - Send to Specified Partition: This parameter supports sending messages to the specified partition, which is disabled by default.
3. Click **OK** to send the message. In the **Sent the message successfully** pop-up window, click **Message Query** to view the message just sent.



### Viewing producer connection

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Producer Connection** in the **Operation** column to view the list of producers connected to the topic.
<<<<<<< HEAD
    ![](https://qcloudimg.tencent-cloud.cn/raw/5964448721f3c3a94d4deced5ec2ba88.png)
=======
>>>>>>> 4c0ee768bf0276e04d7ad55207e181473466eaf0



### Deleting topic

> !
>
>- Deleting a topic will delete the messages stored in the topic too. Proceed with caution.
>- Topic deletion is an async operation. After you finish the steps required to delete a topic, it takes 1 minute for the configuration to take effect with ZooKeeper. During this period, if you try to create a topic with the same name as the deleted one, the system will return the error code `[4000]10011`. Wait and try again later.

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management** and click **Delete** in the **Operation** column.
3. In the window that pops up, click **OK** to delete the topic.



### Configuring advanced topic parameters

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management**.
3. In the **Operation** column, click **Edit** > **Show advanced configuration** and set the following parameters:
    ![](https://main.qcloudimg.com/raw/52c8c0c4e99edd52247c1152129e5ddd.png)

The parameters are described as follows:

<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Default Value</th>
        <th style='text-align:left;'>Valid Values</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>cleanup.policy</td>
        <td style='text-align:left;'>delete</td>
        <td style='text-align:left;'>delete/compact</td>
        <td style='text-align:left;'>Log can be deleted by retention time, or can be compacted by key (the compact mode is required for kafka connect).</td>
    </tr>
    <tr>
        <td style='text-align:left;'>min.insync.replicas</td>
        <td style='text-align:left;'>1</td>
        <td style='text-align:left;'>-</td>
        <td style='text-align:left;'>When "producer" sets "request.required.acks" to 1, "min.insync.replicas" will specify the minimum number of replicas.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>unclean.leader.election.enable</td>
        <td style='text-align:left;'>true</td>
        <td style='text-align:left;'>true/false</td>
        <td style='text-align:left;'>This parameter specifies whether a replica not in ISR can be set as a leader.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>segment.ms</td>
        <td style='text-align:left;'>-</td>
        <td style='text-align:left;'>1–90 days</td>
        <td style='text-align:left;'>Segment shard rolling duration in ms. Minimum value: 86,400,000 ms.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>retention.ms</td>
        <td style='text-align:left;'>Message retention period of the instance</td>
        <td style='text-align:left;'>60000 ms–90 days</td>
        <td style='text-align:left;'>Message retention period at the topic level.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>retention.bytes</td>
        <td style='text-align:left;'>Message retention size of the instance</td>
        <td style='text-align:left;'>1–1024 GB</td>
        <td style='text-align:left;'>Message retention size at the topic level. If both the message retention period and size are set for a topic, the threshold first reached by actually retained messages will prevail.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>max.message.bytes</td>
        <td style='text-align:left;'>-</td>
        <td style='text-align:left;'>1 KB–12 MB</td>
        <td style='text-align:left;'>Maximum message size at the topic level. If this parameter is left empty, it will be 1 MB by default.</td>
    </tr>
    </tbody>
</table>




### Setting topic traffic throttling rule

You can throttle the topic traffic to prevent the excessive traffic of one topic from affecting other topics.

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management**.
3. In the **Operation** column, click **Edit** > **Traffic Throttling** and set the threshold.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3963798dd53c757c0a4f72f24e66d34b.png)
   - Maximum Topic Production Traffic: This value excludes replica traffic and ranges from 1 MB/s to the maximum bandwidth purchased for the instance / number of replicas of the topic.
   - Maximum Topic Consumption Traffic: This value ranges from 1 MB/s to the maximum bandwidth purchased for the instance.
> ?
>
> - The underlying layer throttles the traffic for brokers, and the actual traffic throttling value (equal to an integer multiple of the number of brokers) may be slightly different from the set value.
> - For more information on the soft traffic throttling mechanism, see [Traffic Throttling](https://intl.cloud.tencent.com/document/product/597/39874).

