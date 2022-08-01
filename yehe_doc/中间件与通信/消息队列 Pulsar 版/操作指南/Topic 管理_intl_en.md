## Overview

Topic is a core concept in TDMQ for Pulsar. It is usually used to categorize and manage various messages produced by the system in a centralized manner; for example, messages related to transactions can be placed in a topic named "trade" for other consumers to subscribe to.
In actual application scenarios, a topic often represents a business category. You can decide how to design different topics based on your system and data architectures.

This document describes how to use topics to categorize and manage messages in TDMQ for Pulsar.

## Prerequisites

You have created a namespace.

## Directions

### Creating a topic

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and click **Topic Management** on the left sidebar.
2. On the **Topic Management** page, click **Create** to pop up the **Create Topic** window.
3. In the **Create Topic** window, enter the following information:
   ![](https://qcloudimg.tencent-cloud.cn/raw/d0d5b0e74d259fe81a2ea1f588318394.png)
    - Topic Name: It cannot be empty and can contain up to 128 digits, letters, and special symbols (-\_=:.).
    - Topic Type: **Persistent** or **Non-persistent**.
      - Persistent: Persistently stored messages are stored in the disk with multiple replicas to avoid message loss. Such messages are suitable for scenarios that require high data reliability such as financial or business transactions.
      - Non-persistent: Non-persistently stored messages are stored in the broker. Such messages are suitable for stream processing or other scenarios that do not require high data reliability. Such messages cannot be queried and traced.
    - Partition:
      - Pulsar guarantees that messages in a single partition are sequential - that is, if there is only one partition in a topic, messages there are globally sequential.
      - Multi-partition topics have better performance than single-partition topics. To balance performance and sequence, you can use the Key-Shared subscription mode as instructed in [Subscription Mode](https://intl.cloud.tencent.com/document/product/1110/42923) to make messages partitionally sequential. You only need to mark messages that need to be sequential with the same key and deliver them to the same partition.
    - Description: Enter the topic remarks of up to 128 characters.
4. Click **Save**, and you can see the created topic in the topic list.
![](https://qcloudimg.tencent-cloud.cn/raw/897456deed29b847d8876154740027a4.png)
<table>
<tr>
<th>Parameter	</th>
<th>Description</th>
</tr>
<tr>
<td>Topic Name</td>
<td>The topic name in the format of <code>pulsar-****/namespace/topicName</code>.</td>
</tr>
<tr>
<td>Monitoring</td>
<td>Click <img src = "https://qcloudimg.tencent-cloud.cn/raw/ac572a960433508f64f226e6ea218c10.png"> to view the topic monitoring details. For more information on monitoring metrics, see <a href = "https://cloud.tencent.com/document/product/1179/66709">Viewing Monitoring Data</a>.</td>
</tr>
<tr>
<td>Type</td>
<td>The message type, including general, globally sequential, and partitionally sequential. For more information, see <a href = "https://cloud.tencent.com/document/product/1179/44833"><b>Message Type</b></a>.</td>
</tr>
<tr>
<td>Creator</td>
<td><b>User</b> or <b>System</b>.</td>
</tr>
<tr>
<td>Partition</td>
<td>The number of topic partitions.</td>
</tr>
<tr>
<td>Client</td>
<td><ul><li>Producer: It displays the number of producers/the maximum number of producers. Click it to enter the producer details page. For more information, see <a href = "https://cloud.tencent.com/document/product/1179/66708"><b>Producer Management</b></a>.</li>
<li>Consumer: It displays the number of consumers/the maximum number of consumers. Click it to enter the consumer details page. For more information, see <a href = "https://cloud.tencent.com/document/product/1179/44821#.E6.9F.A5.E7.9C.8B.E8.AE.A2.E9.98.85.E8.AF.A6.E6.83.85"><b>Viewing subscription details</b></a>.</li></ul>
<b>Note: </b>When the value is displayed in orange (warning), the fraction has reached 80%. When it is displayed in red (error), the fraction has reached 90%, in which case you need to close unnecessary client connections.
</td>
</tr>
<tr>
<td>Creation Time</td>
<td>The creation time of the topic.</td>
</tr>
<tr>
<td>Description</td>
<td>The remarks of the topic.</td>
</tr>
</table>



### Querying a topic

You can search for topics by topic name in the search box in the top-right corner of the [Topic Management](https://console.cloud.tencent.com/tdmq/topic) page. TDMQ for Pulsar will perform a fuzzy match and display the search results.

You can also filter topics by **Type** and **Creator** in the topic list.

### Editing a topic

1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Edit** in the **Operation** column of the target topic.
2. In the pop-up window, you can edit the number of topic partitions (which is 1 for globally sequential messages and cannot be edited) as well as the description.
3. Click **Submit**.

### Sending a message

You can manually send a message to the specified topic in the TDMQ for Pulsar console.

1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Send Message** in the **Operation** column of the target topic.
2. Enter the message content of up to 64 KB in the pop-up window.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c7519c1bfe6c6d2b37810136ec9c8acb.png)
3. Click **Submit** to send the message. After the message is sent, it can be consumed by any subscribers to the topic.





### Adding a subscription

You can manually create a subscription in the TDMQ for Pulsar console.

1. In [Topic Management](https://console.cloud.tencent.com/tdmq/topic), click **Create Subscription** in the **Operation** column of the target topic.
2. Enter the subscription name and description in the pop-up window.
 - Subscription Name: It can contain up to 64 characters.
 - Auto-Create Retry & Dead Letter Queue: You can choose whether to automatically create a retry letter topic and a dead letter topic.
 - Description: Enter remarks of up to 200 characters.
![](https://qcloudimg.tencent-cloud.cn/raw/396cf90b66dbe4e456d9f033cae2a399.png)
3. Click **Submit**.
   You can click **View Subscription** in the **Operation** column of a topic to view its subscriptions, and the subscription just created will be displayed in the list.

>?
>
>- If you select **Auto-Create Retry & Dead Letter Queue**, TDMQ for Pulsar will automatically create a retry topic and a dead letter topic, which will be displayed in the topic list as two new topics named "subscription name + RETRY" and "subscription name + DLQ" respectively.
>- For the concepts and usage of retry letter and dead letter topics, see [Retry Letter Topic and Dead Letter Topic](https://intl.cloud.tencent.com/document/product/1110/42958).

### Deleting a topic

>!After a topic is deleted, all unconsumed messages retained in it will be cleared; therefore, proceed with caution.

1. In **Topic Management**, click **More** > **Delete** in the **Operation** column of the target topic. You can also select multiple topics and click **Delete** at the top of the topic list.
2. In the pop-up window, click **Submit**.
   Force Deletion: After this option is enabled, a topic will be forcibly deleted even if it has subscriptions.
   <img src="https://qcloudimg.tencent-cloud.cn/raw/c3eb46625efc49c0d5b4783569a2ffdb.png" width="600">
