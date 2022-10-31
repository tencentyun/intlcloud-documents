## October 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the exclusive cluster feature commercially</td>
<td>You can purchase exclusive clusters with physical resources isolated between them.</td>
<td>2022-10-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/43067">Purchase Guide</a></td>
</tr></table>








## April 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Upgraded the monitoring feature</td>
<td>TDMQ for RabbitMQ has upgraded its monitoring panel. The new panel supports monitoring metrics of clusters, vhosts, exchanges, and queues, with dozens of new monitoring metrics added for status diagnosis and problem locating, such as P95/P99/P999 production durations.</td>
<td>2022-04-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/47691">Monitoring and Alarms</a></td>
</tr></table>






## January 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported RabbitMQ migration to the cloud</td>
<td>TDMQ for RabbitMQ supports migrating RabbitMQ clusters to the cloud for a better service experience.
</td>
<td>2022-01-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/45977">Migrating RabbitMQ to Cloud</a></td>
</tr></table>



## December 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the message query feature</td>
<td>You can check the production records of a batch of messages in the specified time period or a specific message with the specified message ID. After finding the production records, you can further view the body content and parameters of the messages.
</td>
<td>2021-12-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/45975">Message Query</a></td>
</tr><tr>
<td>Provided demos for multiple programming languages</td>
<td>-</td>
<td>2021-12-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/46552">SDK for Java</a></td>
</tr></table>







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
<td>Supported connection with RabbitMQ client in the open-source Spring framework</td>
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
<td>TDMQ for RabbitMQ is a proprietary message queue service developed by Tencent. It supports the AMQP 0-9-1 protocol and is fully compatible with all components and principles of Apache RabbitMQ. It also has the underlying benefits of computing-storage separation and flexible scaling.
</td>
<td>2021-09-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1112/43060">Overview</a></td>
</tr></table>

