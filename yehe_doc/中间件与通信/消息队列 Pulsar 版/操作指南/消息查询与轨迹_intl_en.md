TDMQ for Pulsar records the complete flow in which a message is sent from the producer to the TDMQ for Pulsar server and then consumed by the consumer, and then displays the flow as a message trace in the console.
A message trace records the entire process in which the message is sent from the producer to the TDMQ for Pulsar server and eventually to the consumer, including the duration of each stage (accurate down to the microsecond), execution result, producer IP, and consumer IP.
![](https://qcloudimg.tencent-cloud.cn/raw/71edb89393e8df75760d0d5fccbf0faa.svg)

## Overview

You can use the message query feature in the TDMQ for Pulsar console to view the content, parameters, and trace of a specific message by time or by the message ID displayed in the log. With this feature, you can do the following:

- View the specific content and parameters of the message.
- View from which producer IP a message was sent, whether it was sent successfully, and the exact time when it arrived at the server.
- View whether the message was persistently stored.
- View which consumers consumed the message, whether it was consumed successfully, and the specific time when its consumption was acknowledged.
- View the MQ's message processing latency to analyze the performance of the distributed system.

## Query limits

- You can query messages in the last 3 days.
- You can query up to 65,536 messages at a time.

## Prerequisites

You have deployed the producer and consumer services as instructed in [SDK Overview](https://intl.cloud.tencent.com/document/product/1110/42945), and they produced and consumed messages in the last seven days.

## Directions

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and click **Message Query** on the left sidebar.
2. On the **Message Query** page, select the region and environment first and then the time range for query. If you know the message ID, you can also enter it for exact match query.
3. Click **Query**, and the list below will display paginated results.
![](https://qcloudimg.tencent-cloud.cn/raw/397670a03ff60299223ce9d42b4cb722.png)
4. Click **View Details** in the **Operation** column of the target message to view its basic information, content (message body), and parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/60ac620c719676b6f5d3ed82b775860f.png)
5. Click **View Message Trace** in the **Operation** column or select the **Message Trace** tab on the details page to view the trace of the message. For more information, see [Message trace query result description](#1).
![](https://qcloudimg.tencent-cloud.cn/raw/ea6820ca51d43bd00b70f19adefaec54.png)

<span id="1"></span>

## Message trace query result description

A message trace query result consists of three parts: message production, message storage, and message consumption.

<dx-tabs>
::: Message production
| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Producer Address</nobr> | Address and port of the producer.                                   |
| Production Time              | The time when the TDMQ for Pulsar server acknowledged message receipt, accurate down to the millisecond.                |
| Production Status              | Message production success or failure. If the status is **Failed**, it is generally because the header of the message was lost during sending, and the above fields may be empty. |
:::
::: Message storage
| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Storage Time</nobr> | The time when the message was persistently stored (TDMQ for Pulsar currently adopts the strong consistency mode where messages will be acknowledged only after being stored, so the storage time is the same as the production time; if in high performance mode, they are different). |
| Storage Duration              | The duration between when the message was persistently stored and when the TDMQ for Pulsar server received the acknowledgment, accurate down to the millisecond. |
| Storage Status              | Message storage success or failure. If the status is **Failed**, the message failed to be stored on the disk, which is possibly because the underlying disk was damaged or full. In this case, submit a ticket for assistance as soon as possible. |
:::
::: Message consumption
Message consumption is displayed in the form of a list. TDMQ for Pulsar supports multi-subscription mode, where a message may be consumed by multiple consumers in multiple subscriptions.

The information displayed in the list is as described below:

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Subscription Name</nobr> | Subscriber name.                                               |
| Subscription Mode | There are four subscription modes: shared, key-shared, exclusive, and failover. For more information, see [Subscription Mode](https://intl.cloud.tencent.com/document/product/1110/42923). |
| Number of Pushes                | The number of times the TDMQ for Pulsar server has delivered the message to consumers.             |
| Last Pushed            | The last time the TDMQ for Pulsar server delivered the message to consumers.    |
| Consumption Status              | <li>Not pushed: The TDMQ for Pulsar server has not delivered the message to the consumer. </li><li>Pushed: The TDMQ for Pulsar server has delivered the message to the consumer but has not received an acknowledgment from the consumer. </li><li>Acknowledged: The consumer has sent an acknowledgment to the TDMQ for Pulsar server, which has been received. </li> |

You can view the message push details by clicking the right triangle on the left of the subscription name.

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| <nobr>Push Sequence</nobr> | Which time the TDMQ for Pulsar server delivers the message to consumers.            |
| Consumer Name | Subscription name. |
| Consumer Address                | Address and port of the consumer receiving the message.                                 |
| Push Time              | The time when the TDMQ for Pulsar server delivers the message to consumers.               |
| Push Result              | <li>Pushed: The TDMQ for Pulsar server has delivered the message to the consumer but has not received an acknowledgment from the consumer. </li><li>Acknowledged: The consumer has sent an acknowledgment to the TDMQ for Pulsar server, which has been received. </li><li>Timed-out: The TDMQ for Pulsar server did not receive an acknowledgment after the timeout period elapsed and will deliver the message again. </li> |

:::
</dx-tabs>



