## Overview

Topic is a category name where messages are stored and published. With CKafka, producers write messages to topics, and consumers read messages from topics. To enable horizontal scaling, a topic is divided into multiple [partitions](https://intl.cloud.tencent.com/document/product/597/32275). This allows you to horizontally scale your resources by adding more partitions in case of performance bottlenecks.

This document describes how to create a topic in the CKafka console.

## Prerequisites

You have created an instance as instructed in [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718).

## Directions

### Step 1. Create a topic

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
3. On the instance details page, click **Topic Management** at the top and click **Create**.
4. In the **Create Topic** window, set the **Partition Count**, **Replica Count**, and other parameters.
   ![](https://qcloudimg.tencent-cloud.cn/raw/931c72752e4835ce41c330137943b0f6.png)
   - Name: The topic name. It cannot be changed once entered and can contain only letters, digits, underscores, or symbols ("-" and ".").
   - Partition Count: It is a concept in physical partition, where one topic can contain one or more partitions. CKafka uses partition as an allocation unit.
   - Replica Count: The number of partition replicas, which ensure the high availability of partitions. For data reliability considerations, two replicas are enabled by default. Replicas are also counted into the number of partitions. For example, if you create 1 topic with 6 partitions and 2 replicas for each partition, then you have a total of 12 partitions (1 x 6 x 2).
> !Creating a single-replica topic cannot guarantee the availability; therefore, you should choose it with caution.
   - **Tag**: Set a resource tag. For more information, see [Tag Overview](https://intl.cloud.tencent.com/document/product/597/41600).
   - Preset ACL Policy: Select the preset ACL policy. For more information on ACL policy, see [Configuring ACL Policy](https://intl.cloud.tencent.com/document/product/597/39084).
5. Click **Submit**.



### Step 2. Configure advanced topic parameters

1. On the **Instance List** page, click the **ID/Name** of the target instance to enter the instance details page.
2. On the instance details page, select **Topic Management**.
3. In the **Operation** column, click **Edit** > **Show advanced configuration** and set the following parameters:
   ![](https://qcloudimg.tencent-cloud.cn/raw/ee3cb60f0c3eaf4e913594e5a620c449.png)

The parameters are as detailed below:

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
        <td style='text-align:left;'>5mins–90 days</td>
        <td style='text-align:left;'>The segment shard rolling duration in ms. Minimum value: 86,400,000 ms.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>retention.ms</td>
        <td style='text-align:left;'>The message retention period of the instance</td>
        <td style='text-align:left;'>60000 ms–90 days</td>
        <td style='text-align:left;'>The message retention period at the topic level.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>retention.bytes</td>
        <td style='text-align:left;'>The message retention size of the instance</td>
        <td style='text-align:left;'>1–1024 GB</td>
        <td style='text-align:left;'>The message retention size at the topic level. If both the message retention period and message retention size are set for a topic, the actual message retention will be determined by which threshold is reached first.</td>
    </tr>
    <tr>
        <td style='text-align:left;'>max.message.bytes</td>
        <td style='text-align:left;'>-</td>
        <td style='text-align:left;'>1 KB–12 MB</td>
        <td style='text-align:left;'>The maximum message size at the topic level. If this parameter is left empty, it will be 1 MB by default.</td>
    </tr>
    </tbody>
</table>
