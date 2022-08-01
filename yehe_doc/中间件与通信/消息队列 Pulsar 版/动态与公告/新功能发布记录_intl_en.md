## June 2022

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported creating non-persistent messages</td>
<td>You can choose to create non-persistent messages in the console and select the number of partitions for such messages.</td>
<td>2022-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42930">Topic Management</a></td>
</tr><tr>
<td>Supported setting limits on cluster quotas</td>
<td>To enhance the stability of virtual clusters, limits are imposed on some cluster quotas (existing clusters are not affected):
<li>The range of the TTL for new namespaces is changed to 60 seconds–1 day.</li>
<li>For new virtual clusters, the maximum production/consumption TPS per topic partition is reduced from 50,000 to 5,000, and the maximum production/consumption bandwidth per topic partition is reduced from 50 MB/s to 5 MB/s, so as to avoid the mutual impact between users due to excessive traffic.</li></td>
<td>2022-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42907">Use Limits</a></td>
</tr><tr>
<td>Supported filtering topics by <b>Type</b> and <b>Creator</b> in the message topic list</td>
<td>-</td>
<td>2022-06-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42930">Topic Management</a></td>
</tr></table>

## December 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported displaying the list of topic producers</td>
<td>You can view the list of topic producers, which helps you locate producer issues more easily.</td>
<td>2021-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/46520">Producer Management</a></td>
</tr><tr>
<td>Added the display of producer/consumer counts and cap alarms</td>
<td>The numbers of producers/consumers and alarms for caps are displayed to promptly notify you of any exceptions in a topic.</td>
<td>2021-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42930">Topic Management</a></td>
</tr><tr>
<td>Supported displaying the number of retries and acknowledgment status for message trace</td>
<td>Message trace allows you to view the consumer subscription types, retries, and acknowledgment status of consumers.</td>
<td>2021-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42934">Message Query and Trace</a></td>
</tr><tr>
<td>Supported the pay-as-you-go billing mode for TDMQ for Pulsar</td>
<td>TDMQ for Pulsar becomes pay-as-you-go and will be billed starting from January 2022.</td>
<td>2021-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42909">Billing Overview</a></td>
</tr></table>



## October 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported cluster-level statistics collection</td>
<td>Cluster-level statistics can be collected, making it easier for you to view the usage details of clusters as a whole. This feature is launched to support the future pay-as-you-go billing mode.</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42928">Cluster Management</a></td>
</tr><tr>
<td>Supported tag management</td>
<td>Resource tagging and tag authentication with CAM are supported. Resource management is supported for proprietary cloudified businesses.</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42939">Managing Resource with Tag</a></td>
</tr><tr>
<td>Added topic-level alarms</td>
<td>Topic-level alarms are added for production/consumption speed and traffic and online producer/consumer count.</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42937">Alarm Configuration</a></td>
</tr><tr>
<td>Supported blocking public network access to clusters</td>
<td>-</td>
<td>2021-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42928">Cluster Management</a></td>
</tr></table>






## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supported setting the message retention period policy in namespaces</td>
<td><li>Deletion after consumption: Messages will be cleared within a certain period of time after being acknowledged successfully to save the storage space.</li><li>Persistent retention: No matter whether messages are consumed or not, they will be stored persistently within the maximum retention period and maximum storage space and then deleted chronologically after the limit is reached.</li></td>
<td>2021-08-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42929">Namespace</a></td>
</tr><tr>
<td>Supported force deletion of topics and subscriptions</td>
<td><li>Force deletion of topics: A topic will be force deleted even if it has subscriptions.</li><li>Force deletion of subscriptions: A subscription will be force deleted even if it has active consumer connections.</li></td>
<td>2021-08-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42929">Namespace</a></td>
</tr></table>




## May 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched clusters on v2.7.1</td>
<td>TDMQ for Pulsar now supports clusters on v2.7.1. <li>The cluster version is updated to open-source Pulsar 2.7.1 to support more features and simplify connection.</li><li>The <code>listenerName</code> dependency is removed for the new cluster version, so you don't need to declare <code>listenerName</code> when connecting to a cluster on v2.7.1 or later from an open-source Pulsar client.</li></td>
<td>2021-05-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1110/42898">Cluster Version Updates</a></td>
</tr></table>



## January 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Launched the cluster management feature</td>
<td>You can create virtual clusters (which share the underlying resources) and exclusive clusters (which use the underlying resources exclusively) in the console.</td>
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
<td>On the <b>Message Query</b> page, you can query the details and trace of a message, including the message content, parameters, duration of each stage, execution result, producer IP, and consumer IP.</td>
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
<td><li><a href="https://intl.cloud.tencent.com/document/product/1110/42936">Role and Authentication</li><li><a href="https://cloud.tencent.com/document/product/1179/47542">JWT Authentication Configuration</li></td>
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
<td><a href="https://cloud.tencent.com/document/product/1179/44778">Overview</a></td>
</tr></table>
