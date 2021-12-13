## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported setting the message retention period policy in namespaces</td>
<td><li>Deletion after consumption: messages will be cleared within a certain period of time after being acknowledged successfully to save the storage space.</li><li>Persistent retention: no matter whether messages are consumed or not, they will be stored persistently within the maximum retention period and maximum storage space and then deleted chronologically after the limit is reached.</li></td>
<td>2021-08-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42929">Namespace</a></td>
</tr><tr>
<td>Supported force deletion of topics and subscriptions</td>
<td><li>Force deletion of topics: a topic will be force deleted even if it has subscriptions.</li><li>Force deletion of subscriptions: a subscription will be force deleted even if it has active consumer connections.</li></td>
<td>2021-08-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42930">Topic Management</a></td>
</tr></table>


## May 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched clusters on v2.7.1</td>
<td>TDMQ for Pulsar now supports clusters on v2.7.1. <li>The cluster version is updated to open-source Pulsar 2.7.1 to support more features and simplify connection.</li><li>The `listenerName` dependency is removed for the new cluster version, so you don't need to declare `listenerName` when connecting to a cluster on v2.7.1 or above from an open-source Pulsar client.</li></td>
<td>2021-05-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42898">Cluster Version Release Notes</a></td>
</tr></table>

## January 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the cluster management feature</td>
<td>You can create virtual clusters (which share the underlying resources) and dedicated clusters (which use the underlying resources exclusively) in the console.</td>
<td>2021-01-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42928">Cluster Management</a></td>
</tr></table>


## October 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the message query and message trace features</td>
<td>On the **Message Query** page, you can query the details and trace of a message, including the message content, parameters, duration of each stage, execution result, producer IP, and consumer IP.</td>
<td>2020-10-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42934">Message Query and Trace</a></td>
</tr><tr>
<td>Started the open beta test for TDMQ for Pulsar</td>
<td>The open beta test for TDMQ for Pulsar is officially started, and TDMQ for Pulsar can be activated for trial without application. The open beta test has certain limits on the maximum QPS, maximum number of topics, and delayed message concurrency.</td>
<td>2020-10-12</td>
<td>-</td>
</tr></table>



## September 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported connection to TDMQ for Pulsar from native Pulsar clients</td>
<td>You can connect to TDMQ for Pulsar from native Pulsar clients. For security reasons, you need to configure the appropriate role permissions in the console and configure the token on the client (which works in the same way as JWT token authentication used in the community).</td>
<td>2020-09-17</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/1110/42936">Role and Authentication</li><li><a href="https://intl.cloud.tencent.com/document/product/1110/42933">JWT Authentication Configuration</li></td>
</tr><tr>
<td>Upgraded TDMQ for Pulsar in closed beta test to support the native SDK</td>
<td>TDMQ for Pulsar will be suspended and upgraded between 09:00 AM and 12:00 PM on September 17, 2020 to support connection from native Pulsar clients.</td>
<td>2020-09-11</td>
<td>-</td>
</tr></table>


## August 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched TDMQ for Pulsar in multiple regions</td>
<td>TDMQ for Pulsar will be available in the Shanghai region starting from August 9, 2020 and in the Beijing and Chengdu regions starting from August 18, 2020.</td>
<td>2020-08-18</td>
<td>-</td>
</tr></table>



## June 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched TDMQ for Pulsar</td>
<td>TDMQ for Pulsar is a proprietary finance-grade distributed message middleware developed based on Pulsar, a top open-source project of Apache. It features high consistency, reliability, and concurrency. Currently, it is widely used in Tencent's billing scenarios, including core transaction as well as real-time reconciliation, monitoring, and big data analysis.</td>
<td>2020-06-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42904">Overview</a></td>
</tr></table>
