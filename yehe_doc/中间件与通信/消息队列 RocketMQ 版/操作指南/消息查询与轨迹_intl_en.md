TDMQ for RocketMQ records the complete flow of a message being sent from the producer to the TDMQ for RocketMQ server for consumption by the consumer, which is displayed as a message trace in the console.
A message trace records the entire process of how a message flows, including the duration of each stage (accurate down to the microsecond), execution result, producer IP, and consumer IP.
![](https://qcloudimg.tencent-cloud.cn/raw/a8835b388055fc402a545d445c21e4d7.jpg)

## Overview

You can use the message query feature in the TDMQ for RocketMQ console to view the content, parameters, and trace of a specific message by time or by the message ID/message key displayed in the log. With this feature, you can do the following:

- View the specific content and parameters of the message.
- View from which producer IP a message was sent, whether it was sent successfully, and the exact time when it arrived at the server.
- View whether the message was persistently stored.
- View which consumers consumed the message, whether it was consumed successfully, and the specific time when its consumption was acknowledged.
- View the MQ's message processing latency to analyze the performance of the distributed system.

## Query limits

- You can query messages in the last 3 days.
- You can query up to 65,536 messages at a time.

## Prerequisite

You have deployed the producer and consumer services as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/1113/45956), and they produced and consumed messages in the last 3 days.

## Directions

1. Log in to the [TDMQ for RocketMQ console](https://console.cloud.tencent.com/tdmq/rocket-cluster) and click **Message Query** on the left sidebar.
2. On the **Message Query** page, select a region and enter the query conditions as prompted.
   - Time Range: Select the time range for query. You can select the last 6 hours, last 24 hours, or last 3 days, or set a custom time range.
   - Current Cluster: Select the cluster where the topic you want to query is located.
   - Namespace: Select the namespace where the topic you want to query is located.
   - Topic: Select the topic you want to query.
   - Query Method: Below are two supported query methods.
     - **By message ID:** A fast exact query method.
     - **By message key:** A fuzzy query method that is used when you have only set the message key.
3. Click **Query**, and the list below will display paginated results.
![](https://qcloudimg.tencent-cloud.cn/raw/e64e03f1f7aff564e6234e4100ed6660.png)
4. Click **View Details** in the **Operation** column of the target message to view its basic information, content (message body), and parameters.
5. Click **View Message Trace** in the **Operation** column or select the **Message Trace** tab on the details page to view the trace of the message. For more information, see [Message trace query result description](#1).
![](https://qcloudimg.tencent-cloud.cn/raw/26e01a17a960deb774f23a832d22003c.png)

<span id="1"></span>

## Message trace query result description

A message trace query result consists of three parts: message production, message storage, and message consumption.

#### Message production

| Parameter                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Producer Address</nobr> | Address and port of the producer.                                   |
| Production Time              | The time when the TDMQ for RocketMQ server acknowledged message receipt, accurate down to the millisecond.                |
| Sending Duration              | The time it took to send the message from the producer to the TDMQ for RocketMQ server, accurate down to the microsecond. |
| Production Status              | Message production success or failure. If the status is **Failed**, it is generally because the header of the message was lost during sending, and the above fields may be empty. |

#### Message storage

| Parameter                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Storage Time</nobr> | The time when the message was persistently stored.                                         |
| Storage Duration              | The duration between when the message was persistently stored and when the TDMQ for RocketMQ server received the acknowledgement, accurate down to the millisecond. |
| Storage Status              | Message storage success or failure. If the status is **Failed**, the message failed to be stored on the disk, which is possibly because the underlying disk was damaged or full. In this case, submit a ticket for assistance as soon as possible. |

#### Message consumption

Message consumption details are displayed in a list. TDMQ for RocketMQ supports two consumption modes: cluster consumption and broadcast consumption.

The information displayed in the list is as described below:

| Parameter                    | Description                                                         |
| ----------------------- | ------------------------------------------------------------ |
| <nobr>Consumer Group Name</nobr> | Name of the consumer group.                                               |
| Consumption Mode                | The consumer group’s consumption mode, which can be either cluster consumption or broadcast consumption. For more information, see [Cluster Consumption and Broadcast Consumption](https://intl.cloud.tencent.com/document/product/1113/43113). |
| Number of Pushes                | The number of times the TDMQ for RocketMQ server has delivered the message to consumers.             |
| Last Pushed            | The last time the TDMQ for RocketMQ server delivered the message to consumers.    |
| Consumption Status                | <li>Pushed yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers but has not received their acknowledgement. </li><li>Acknowledged: Consumers acknowledged the consumption and the TDMQ for RocketMQ server has received the acknowledgement. </li><li>Put to retry queue: Acknowledgement timed out. The TDMQ for RocketMQ server will deliver the message to consumers again as it did not receive their acknowledgment. </li><li>Retried yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers again but still has not received their acknowledgement. </li><li>Put to dead letter queue: The message has been put to the dead letter queue as it failed to be consumed after multiple retries. </li>Note: If the consumption mode is “broadcast consumption”, the consumption status can only be **Pushed**. |

You can view the message push details by clicking the right triangle on the left of the subscription name.

| Parameter                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Push Sequence</nobr> | Which time the TDMQ for RocketMQ server delivers the message to consumers.            |
| Consumer Address                | Address and port of the consumer receiving the message.                                 |
| Push Time              | The time when the TDMQ for RocketMQ server delivers the message to consumers.               |
| Consumption Status                | <li>Pushed yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers but has not received their acknowledgement. </li><li>Acknowledged: Consumers acknowledged the consumption and the TDMQ for RocketMQ server has received the acknowledgement. </li><li>Put to retry queue: Acknowledgement timed out. The TDMQ for RocketMQ server will deliver the message to consumers again as it did not receive their acknowledgment. </li><li>Retried yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers again but still has not received their acknowledgement. </li><li>Put to dead letter queue: The message has been put to the dead letter queue as it failed to be consumed after multiple retries. </li>Note: If the consumption mode is “broadcast consumption”, the consumption status can only be **Pushed**. |

