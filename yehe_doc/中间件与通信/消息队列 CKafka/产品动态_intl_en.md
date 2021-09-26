## September 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka supports higher public network bandwidth</td>
<td>CKafka provides 3 Mbps public network bandwidth for free by default. Pro Edition instances can upgrade public network bandwidth to 198 Mbps additionally.</td>
<td>2021-09-09</td>
<td>Public Network Bandwidth Management</td>
</tr><tr>
<td>Standard Edition instances with high specifications are no longer available</td>
<td>CKafka Standard Edition instances with over 150 MB/s bandwidth (instance types: large and xlarge) are no longer available since September 9, 2021. Such types of instances purchased before that day can still be used, and their specifications can still be upgraded according to the previous specification system.</td>
<td>2021-09-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></td>
</td>
</tr></table>



## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka supports SASL_SSL access</td>
<td>CKafka supports SASL_SSL access, meeting the security and compliance requirements of more users.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr><tr>
<td>The message query feature supports the query of messages in all partitions</td>
<td>You can view the message details of all partitions in the console, without the need to view them one by one.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39719">Querying Message</a></td>
</tr><tr>
<td>Supports batch adding IPs when configuring an ACL policy</td>
<td>You can batch add IPs or IP ranges (which are separated with semicolon) when configuring an ACL policy in the console to save operation costs.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</td>
</tr></table>






## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The disk capacity limit of high-spec Pro Edition instances is adjusted</td>
<td>For Pro Edition instances with 1600 MB/s or higher bandwidth, the disk capacity limit of them has increased to 200,000 GB.</td>
<td>2021-08-03</td>
<td>-</td>
</tr><tr>
<td>Supports viewing the details of topics and unsynced replicas</td>
<td>CKafka supports viewing the details of topics and unsynced replicas in the console.</td>
<td>2021-08-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32554">Topic Management</a></td>
</tr><tr>
<td>Regex is supported for instance naming</td>
<td>When purchasing multiple instances, you can batch create instances by its numeric suffix (which is numbered in an ascending order) or its designated pattern string.</td>
<td>2021-08-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41581">Naming with Consecutive Numeric Suffixes or Designated Pattern String</a></td>
</tr><tr>
<td>CKafka is compatible with open-source Kafka 2.8</td>
<td>CKafka Pro Edition is compatible with open-source Kafka 2.8.</td>
<td>2021-08-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40964">Suggestions for CKafka Version Selection</a></td>
</tr></table>







## July 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Pro Edition supports the advanced monitoring feature</td>
<td>You can view the production and consumption traffic rankings of topics and the consumption speed rankings of consumer groups in the console, making it easier for OPS personnel to troubleshoot issues.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41378">Viewing Advanced OPS Features (Pro Edition)</a></td>
</tr><tr>
<td>Supports partition-level monitoring</td>
<td>CKafka supports displaying the monitoring data (such as the number of produced and consumed messages and consumption speed) of a single partition of a topic.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/12167">Viewing Monitoring Data</a></td>
</tr><tr>
<td>The feature of migrating self-built Kafka clusters to cloud is perfected</td>
<td>With the specification calculator and migration tools provided by CKafka, a self-built Kafka cluster can be migrated to the cloud.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41379">Migration</a></td>
</tr><tr>
<td>CKafka 2.4.2 is replaced by CKafka 2.4.1</td>
<td>-</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40964">Suggestions for CKafka Version Selection</a></td>
</tr></table>





## May 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The available bandwidth increases</td>
<td>The limit of available bandwidth increases from 3,200 MB/s to 10,000 MB/s.</td>
<td>2021-05-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></td>
</tr></table>






## April 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports fuzzy match when configuring ACL policies</td>
<td>CKafka supports configuring an ACL policy for multiple topics. Fuzzy match by topic name prefix is supported for CKafka 2.4.2 instances.</td>
<td>2021-04-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</tr><tr>
<td>The high-speed and stable modes are supported for instance upgrade</td>
<td>You can select either high-speed or stable mode when upgrading an instance according to your business requirements. The time consumed in the high-speed mode is about one-tenth that consumed in the stable mode.</td>
<td>2021-04-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr><tr>
<td>Pro Edition supports advanced monitoring</td>
<td>CKafka Pro Edition supports advanced monitoring. You can view metrics such as core services, production, consumption, and broker GC in the console, making it easier for OPS personnel to troubleshoot issues.</td>
<td>2021-04-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40038">Querying Advanced Monitoring (Pro Edition)</a></td>
</tr><tr>
<td>Pro Edition supports Premium Cloud Storage</td>
<td>-</td>
<td>2021-04-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></td>
</tr></table>









## March 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports upgrade at specified time</td>
<td>CKafka Supports upgrading instances at specified time to avoid affecting your business.</td>
<td>2021-03-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr><tr>
<td>Supports dynamic message retention policies</td>
<td>With the dynamic data retention policy configured, when the disk utilization reaches a certain percentage, a certain proportion of data will automatically expire.</td>
<td>2021-03-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40211">Adding Dynamic Message Retention Policy</a></td>
</tr><tr>
<td>Consumer groups can be deleted</td>
<td>Consumer groups can be deleted in the CKafka console.</td>
<td>2021-03-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40037">Deleting Consumer Group</a></td>
</tr></table>






## February 2021


<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Multi-AZ deployment is supported</td>
<td>CKafka Pro Edition supports multi-AZ deployment. When you purchase a CKafka instance in a region with three or more AZs, you can select any two of them for multi-AZ deployment.</td>
<td>2021-02-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40243">Multi-AZ Deployment</a></td>
</tr><tr>
<td>Supports viewing instance upgrade progress</td>
<td>CKafka Pro Edition supports displaying the instance upgrade progress.</td>
<td>2021-02-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr></table>






## December 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka supports the SASL access mode for the route type “public domain name access”</td>
<td>You can select public domain name SASL access as the access mode on the instance details page, but such access mode can be selected for only one route for an instance.</td>
<td>2020-12-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr></table>








## October 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka supports querying messages in the console</td>
<td>In case of message consumption exceptions, you can query the exceptional message in the CKafka console for troubleshooting.</td>
<td>2020-10-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39719">Querying Message</a></td>
</tr></table>






## August 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka Pro Edition is officially launched</td>
<td>Pro Edition (formerly Dedicated Edition) instances are available for purchase in multiple regions. Each instance is a dedicated cluster, for which parameters can be flexibly configured. Pro Edition is compatible with open-source Kafka 2.4. We offer limited-time discounts for a limited number of instances and look forward to your purchase.</td>
<td>2020-08-31</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Product Specifications</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></li></td>
</tr></table>







## July 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka Dedicated Edition instances are available for purchase during open beta</td>
<td>Dedicated Edition instances are now available for purchase in multiple regions. You can purchase them on the purchase page at the same price of Standard Edition instances instead of submitting a ticket.</td>
<td>2020-07-20</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Product Specifications</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></li></td>
</tr></table>







## March 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka Dedicated Edition instances are in open beta</td>
<td><li>During the open beta, Dedicated Edition instances (small type) are available in Chengdu region.</li><li>Dedicated instances have dedicated virtual host nodes, and the specifications of them can be customized according to business scenarios.</li></td>
<td>2020-03-24</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Product Specifications</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></li></td>
</tr></table>







## January 2020

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The instance details feature is optimized</td>
<td>CKafka supports viewing the details of open-source Kafka instances.</td>
<td>2020-01-15</td>
<td>-</td>
</tr><tr>
<td>The instance query method is optimized</td>
<td>On the instance list page, fuzzy query by IP/VIP port is supported for querying instances.</td>
<td>2020-01-14</td>
<td>-</td>
</tr><tr>
<td>The instance purchase page is optimized</td>
<td><li>The purchase page supports VPC search.</li><li>The purchase page supports preset tags.</li><li>The purchase page supports displaying high-availability cross-AZ clusters.</li></td>
<td>2020-01-13</td>
<td>-</td>
</tr><tr>
<td>Ckafka APIs are upgraded to v3.0</td>
<td><li>The new API documentation is more standardized and comprehensive, and thus, more user-friendly.</li><li>The support for nearby access in all regions allows faster connection to Tencent Cloud services.</li></td>
<td>2020-01-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/38270">API Documentation</a></td>
</tr></table>







## December 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The consumer group feature is optimized</td>
<td>CKafka supports viewing the monitoring view of all partitions.</td>
<td>2019-12-25</td>
<td>-</td>
</tr></table>








## October 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>CKafka supports the data sync feature<br>(in beta test)</td>
<td>CKafka provides efficient data transfer services based on open-source Kafka Connector.<br><li>You can transfer data between any topics of different CKafka instances in the same region in CKafka Console.</li><li>You can transfer data between any topics of different CKafka instances in the same region or different regions through CKafka APIs.</li></td>
<td>2019-10-30</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/32556">Data Sync</a></li><li>Creating Data Sync Task</li></td>
</tr><tr>
<td>The monitoring and alarming feature is optimized</td>
<td>This feature supports the monitoring of and the alarming for the number of instance connections and consumption speed.</td>
<td>2019-10-30</td>
<td>-</td>
</tr></table>







## September 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The alarm configuration feature is optimized</td>
<td>Alarm parameters can be directly configured on the instance list page.</td>
<td>2019-09-08</td>
<td>-</td>
</tr></table>








## August 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Data reliability is improved</td>
<td>Existing technologies cannot guarantee that data will never be lost, but you can maximize the data reliability as possible as you can by using certain configuration parameters.</td>
<td>2019-08-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/31586">CKafka Data Reliability Description</a></td>
</tr></table>







## July 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The terms of service are completed</td>
<td>The new version of Service Level Agreement features clearer content and structure.</td>
<td>2019-07-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/31779">Service Level Agreement (New Version)</a></td>
</tr><tr>
<td>Topics can be automatically created</td>
<td>If “auto-create topic” is enabled in the console, when you use or access the metadata of a topic that does not exist, the topic will be automatically created with the configured number of replicas and partitions.</td>
<td>2019-05-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40039">Creating Topic</a></td>
</tr></table>







## April 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports default alarms</td>
<td>When over 90% of the disk space is occupied, notifications will be sent to you through SMS, email, and Message Center by default, avoiding service unavailability caused by your forgetting to configure alarm policies.</td>
<td>2019-04-18</td>
<td>-</td>
</tr></table>







## March 2019

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>The message retention time is extended</td>
<td>CKafka extends the max message retention time from one month to three months.</td>
<td>2019-03-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40039">Creating Instance</a></td>
</tr><tr>
<td>Adds regions outside Chinese mainland</td>
<td>CKafka adds two regions and one zone outside Chinese mainland: Toronto, Virginia, and Silicon Valley Zone 1.</td>
<td>2020-03-02</td>
<td>-</td>
</tr></table>








## December 2018

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports configuring advanced parameters for topics</td>
<td>You can configure fine-grained parameters for instance topics in the CKafka console.</td>
<td>2018-12-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32554">Topic Management</a></td>
</tr></table>







## October 2018

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports cross-AZ disaster recovery clusters that feature high availability</td>
<td>CKafka Supports cross-AZ disaster recovery clusters that feature high availability and stability.</td>
<td>2018-10-28</td>
<td>-</td>
</tr></table>







## August 2018

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Route access rules can be configured<br>(in beta test)</td>
<td>You can add routing policies in the CKafka console to enhance the user network access control during public/private network transfer.</td>
<td>2018-08-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr></table>
