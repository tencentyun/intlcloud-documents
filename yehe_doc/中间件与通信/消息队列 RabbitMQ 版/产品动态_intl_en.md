## October 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported the alternate exchange capability of open-source RabbitMQ</td>
<td>If the primary exchange cannot route a message, the message will be routed to the alternate exchange for message delivery. This feature can be used for message delivery monitoring.</td>
<td>2021-10-27</td>
<td>-</td>
</tr><tr>
<td>Supported declarations on the client</td>
<td>You can declare exchanges, queues, and bindings through code on the client, which greatly reduces the manual workload during migration. </td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/43083">RabbitMQ Client API Description</a></td>
</tr><tr>
<td>Supported connection with Rabbitmq client in the open-source Spring framework</td>
<td>Thanks to the support for declarations on the client, you can seamlessly migrate to TDMQ for RabbitMQ if you originally use the message queue through Spring's built-in client.</td>
<td>2021-10-27</td>
<td>-</td>
</tr><tr>
<td>Supported exclusive consumption</td>
<td>You can declare the `exclusive` field in the consumption code, indicating that the queue can be consumed by only one consumer, and an error will be reported when a second consumer tries to connect to it. </td>
<td>2021-10-27</td>
<td>-</td>
</tr></table>



## September 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched TDMQ for RabbitMQ</td>
<td>TDMQ for RabbitMQ is Tencent's proprietary message queue service. It supports the AMQP 0-9-1 protocol and is fully compatible with all components and principles of Apache RabbitMQ. It also has the underlying benefits of computing-storage separation and flexible scaling.
</td>
<td>2021-09-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/43060">Overview</a></td>
</tr></table>
