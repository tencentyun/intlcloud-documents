## Message trace query result description

A message trace query result consists of three parts: message production, message storage, and message consumption.

### Message production

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| Producer Address | Address and port of the producer.                                   |
| Production Time              | The time when the TDMQ for RocketMQ server acknowledged message receipt, accurate down to the millisecond.                |
| Sending Duration              | The time it took to send the message from the producer to the TDMQ for RocketMQ server, accurate down to the microsecond. |
| Production Status              | Message production success or failure. If the status is **Failed**, it is generally because the header of the message was lost during sending, and the above fields may be empty. |

### Message storage

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| Storage Time | The time when the message was persistently stored.                                         |
| Storage Duration              | The duration between when the message was persistently stored and when the TDMQ for RocketMQ server received the acknowledgment, accurate down to the millisecond. |
| Storage Status              | Message storage success or failure. If the status is **Failed**, the message failed to be stored on the disk, which is possibly because the underlying disk was damaged or full. In this case, submit a ticket for assistance as soon as possible. |

### Message consumption

Message consumption details are displayed in a list. TDMQ for RocketMQ supports two consumption modes: cluster consumption and broadcast consumption.

The information displayed in the list is as described below:

| Parameter | Description |
| ----------------------- | ------------------------------------------------------------ |
| Consumer Group Name | Name of the consumer group.                                               |
| Consumption Mode                | The consumer group's consumption mode, which can be either cluster consumption or broadcast consumption. For more information, see [Cluster Consumption and Broadcast Consumption](https://intl.cloud.tencent.com/document/product/1113/43113). |
| Number of Pushes                | The number of times the TDMQ for RocketMQ server has delivered the message to consumers.             |
| Last Pushed            | The last time the TDMQ for RocketMQ server delivered the message to consumers.    |
| Consumption Status                | <li>Pushed yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers but has not received their acknowledgment. </li><li>Acknowledged: Consumers acknowledged the consumption and the TDMQ for RocketMQ server has received the acknowledgment. </li><li>Put to retry queue: Acknowledgment timed out. The TDMQ for RocketMQ server will deliver the message to consumers again as it did not receive their acknowledgment. </li><li>Retried yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers again but still has not received their acknowledgment. </li><li>Put to dead letter queue: The message has been put to the dead letter queue as it failed to be consumed after multiple retries. </li>Note: If the consumption mode is "broadcasting", the consumption status can only be **Pushed**. |

You can view the message push details by clicking the right triangle on the left of the subscription name.

| Parameter | Description |
| --------------------- | ------------------------------------------------------------ |
| Push Sequence | The sequence number in which the TDMQ for RocketMQ server delivers the message to consumers.             |
| Consumer Address                | Address and port of the consumer receiving the message.                                 |
| Push Time              | The time when the TDMQ for RocketMQ server delivers the message to consumers.               |
| Consumption Status                | <li>Pushed yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers but has not received their acknowledgment. </li><li>Acknowledged: Consumers acknowledged the consumption and the TDMQ for RocketMQ server has received the acknowledgment. </li><li>Put to retry queue: Acknowledgment timed out. The TDMQ for RocketMQ server will deliver the message to consumers again as it did not receive their acknowledgment. </li><li>Retried yet unacknowledged: The TDMQ for RocketMQ server has delivered the message to consumers again but still has not received their acknowledgment. </li><li>Put to dead letter queue: The message has been put to the dead letter queue as it failed to be consumed after multiple retries. </li>Note: If the consumption mode is "broadcasting", the consumption status can only be **Pushed**. |
