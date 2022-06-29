## May 2022

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Pro Edition supports more instance connections and consumer groups</td>
<td>Pro Edition supports up to 10,000 instance connections and up to 200 instance-level consumer groups.</td>
<td>2022-05-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39601">Use Limits</a></td>
</tr><tr>
<td>A topic now supports up to 3,000 partitions</td>
<td>-</td>
<td>2022-05-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39601">Use Limits</a></td>
</tr>
</table>










## April 2022

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>The production/consumption bandwidth percentage can be viewed</td>
<td>You can view the production/consumption bandwidth percentage</td>
<td>2022-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/12167">Viewing Monitoring Data</a></td>
</tr><tr>
<td>The automatic disk capacity expansion records can be viewed</td>
<td>You can view the automatic disk capacity expansion records.</td>
<td>2022-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40211">Automatic Disk Capacity Expansion</a></td>
</tr><tr>
</tr>
</table>









## March 2022

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>The production/consumption bandwidth percentage can be viewed</td>
<td>You can view the production/consumption bandwidth percentage</td>
<td>2022-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/12167">Viewing Monitoring Data</a></td>
</tr><tr>
<td>The automatic disk capacity expansion records can be viewed</td>
<td>You can view the automatic disk capacity expansion records.</td>
<td>2022-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40211">Automatic Disk Capacity Expansion</a></td>
</tr><tr>
<td>Topic-level throttling is supported</td>
<td>You can throttle the topic traffic to prevent the excessive traffic of one topic from affecting other topics.</td>
<td>2022-03-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></td>
</tr>
</table>









## February 2022

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Automatic consumer group creation can be disabled</td>
<td>CKafka allows you to disable automatic consumer group creation in the console. After it is disabled, only existing consumer groups in the console can be used for consumption.</td>
<td>2022-02-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/44994">Creating Consumer Group</a></td>
</tr><tr>
<td>Pro Edition supports multi-AZ deployment</td>
<td>You can change the deployment AZ of Pro Edition instances directly in the console to simplify business migration.</td>
<td>2022-02-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46672">AZ Migration</a></td>
</tr><tr>
<td>Pro Edition supports VPC access through SASL_SCRAM</td>
<td>Pro Edition supports authentication through SASL_SCRAM when you access CKafka in a VPC.</td>
<td>2022-02-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr><tr>
<td>You can specify the IP when creating a VPC route</td>
<td>If you select VPC access, you can specify the IP to keep it unchanged when changing the access mode.</td>
<td>2022-02-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr><tr>
<td>You can set the maintenance time</td>
<td>The backend system performs maintenance operations on your CKafka instance from time to time to ensure its stability. To minimize the potential impact on your business, we recommend you set an acceptable maintenance period for your business instance, usually during off-peak hours.</td>
<td>2022-02-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/46673">Setting System Maintenance Time</a></td>
</tr>
</table>









## January 2022

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Topic display fields are added</td>
<td>You can set tags when creating a topic and view producer connections.</td>
<td>2022-01-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></td>
</tr><tr>
<td>You can create consumer groups and send messages directly in the console</td>
<td>You can create consumer groups and send messages directly in the CKafka console, without the need to perform operations on the local client.</td>
<td>2022-01-07</td>
  <td><li><a href="https://intl.cloud.tencent.com/document/product/597/44994">Creating Consumer Group</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></li></td>
</tr><tr>
<td>Pro Edition supports displaying instance connection information</td>
<td>CKafka Pro Edition supports displaying the number of connections in the dashboard. This allows you to view the connections to each server more easily when the number of instance connections is about to be used up.</td>
<td>2022-01-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41378">Viewing Advanced Ops Features (Pro Edition)</a></td>
</tr><tr>
<td>Pro Edition supports automatic disk capacity expansion</td>
<td>CKafka supports automatic adjustment of the disk utilization. After the disk utilization reaches the threshold, you can set the dynamic message retention policy to reduce the message retention time or set the automatic disk capacity expansion policy to adjust the disk space.</td>
<td>2022-01-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40211">Automatic Disk Capacity Expansion</a></td>
</tr><tr>
<td>Public network bandwidth is optimized</td>
<td>You can view the monitoring data of the public network bandwidth. In addition, if you use Pro Edition, you can now purchase the public network bandwidth using the monthly subscription billing mode when purchasing an instance on the purchase page. Existing instances continue to use the bill-by-hour bandwidth rules and can be upgraded.</td>
<td>2022-01-07</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/42386">Public Network Bandwidth Management</a></td>
</tr>
</table>












## November 2021

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>Pro Edition supports transfer over the public network with SASL_SSL</td>
<td>CKafka Pro Edition supports the SASL_SSL access mode.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr>
<tr>
<td>Pro Edition supports displaying the monitoring information scraped by Prometheus</td>
<td>CKafka Pro Edition can display broker nodes’ metric information scraped by Prometheus, including basic monitoring metrics such as CPU, memory usage, and system load, as well as the metrics exposed by the broker's JMX.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/43840">Connection to Prometheus</a></td>
</tr>
<tr>
<td>Pro Edition supports data sync</td>
<td>CKafka Pro Edition supports the data sync feature, which satisfies the needs for topic-level data sync and supports data transfer and automatic sync between any topics in different CKafka instances.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32556">Data Sync</a></td>
</tr><tr>
<td>Pro Edition supports quick diagnosis</td>
<td>CKafka Pro Edition offers the quick diagnosis feature, which can proactively troubleshoot cluster problems and risks, provide solutions based on Tencent Cloud experts' experience, and automatically generate reports from the health check results.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/43841">Quick Diagnosis (Pro Edition)</a></td>
</tr><tr>
<td>You can view the topic rankings in terms of disk usage</td>
<td>You can view the topic rankings in terms of disk usage in the CKafka console, which makes cost accounting easier.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41378">Viewing Advanced Ops Features (Pro Edition)</a></td>
</tr><tr>
<td>Topics support the advanced setting of `retention.bytes`</td>
<td>You can set `retention.bytes` in the advanced topic settings for use together with `retention.ms`. </td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></td>
</tr><tr>
<td>The cap of purchasable bandwidth is increased to 20,000 MB/sec</td>
<td>The cap of purchasable bandwidth is increased to 20,000 MB/sec, which can meet the user needs for configuration upgrade during traffic peaks in sales campaigns.</td>
<td>2021-11-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></td>
</tr>
</table>














## October 2021

<table>
<tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr>
<tr>
<td>The ACL policy is optimized</td>
<td>You can preset ACL rules, which will be automatically applied when you create topics later.</td>
<td>2021-10-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</tr>
<tr>
<td>The maximum number of consumer groups is increased, and alarm configuration is added</td>
<td>The maximum number of consumer groups is increased from 50 to 200, and a metric for reaching the maximum number of consumer groups is added.</td>
<td>2021-10-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39601">Use Limits</a></td>
</tr>
<tr>
<td>A tool for smooth upgrade from Standard Edition to Pro Edition is provided</td>
<td>Due to architecture optimizations, the advanced specification of Standard Edition was deactivated on September 9, 2021. You can smoothly upgrade Standard Edition instances purchased afterwards to Pro Edition in the console.</td>
<td>2021-10-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr><tr>
<td>Pro Edition supports viewing log details in the CKafka console</td>
<td>Pro Edition supports viewing log details in the CKafka console, including consumer group broker logs and controller logs.</td>
<td>2021-10-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/43842">Viewing Log</a></td>
</tr>
</table>










## September 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Pro Edition supports higher public network bandwidth</td>
<td>CKafka provides 3 Mbps public network bandwidth for free by default. Pro Edition instances can upgrade public network bandwidth to 198 Mbps additionally.</td>
<td>2021-09-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/42386">Public Network Bandwidth Management</a></td>
</tr><tr>
<td>Standard Edition instances with high specifications are no longer available</td>
<td>Due to architecture optimizations, CKafka Standard Edition instances with over 150 MB/sec bandwidth (instance types: large and xlarge) have no longer been available since September 9, 2021. Such types of instances purchased before that day can still be used, and their specifications can still be upgraded based on the previous specification system.</td>
<td>2021-09-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/11745">Billing Overview</a></td>
</tr></table>











## August 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Pro Edition supports SASL_SSL access</td>
<td>CKafka Pro Edition supports SASL_SSL access, which can meet the security and compliance requirements of more users.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/32555">Adding Routing Policy</a></td>
</tr><tr>
<td>The message query feature supports the query of messages in all partitions</td>
<td>You can view the message details of all partitions in the console, without the need to view them one by one.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39719">Querying Message</a></td>
</tr><tr>
<td>You can add IPs in batches when configuring an ACL policy</td>
<td>You can add IPs or IP ranges (which are separated by semicolon) in batches when configuring an ACL policy in the console to save operation costs.</td>
<td>2021-08-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</tr><tr>
<td>The disk capacity limit of high-specification Pro Edition instances is adjusted</td>
<td>The disk capacity of Pro Edition instances with 1,600 MB/sec or higher bandwidth is increased to 200,000 GB.</td>
<td>2021-08-03</td>
<td>-</td>
</tr><tr>
<td>You can view the details of topics and unsynced replicas</td>
<td>CKafka supports viewing the details of topics and unsynced replicas in the console.</td>
<td>2021-08-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></td>
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












## June 2021

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Pro Edition supports the advanced monitoring feature</td>
<td>You can view the production and consumption traffic rankings of topics and the consumption speed rankings of consumer groups in the console, making it easier for Ops personnel to troubleshoot issues.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41378">Viewing Advanced Ops Features (Pro Edition)</a></td>
</tr><tr>
<td>Supports partition-level monitoring</td>
<td>CKafka supports displaying the monitoring data (such as the number of produced and consumed messages and consumption speed) of a single partition of a topic.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/12167">Viewing Monitoring Data</a></td>
</tr><tr>
<td>The feature of migrating self-built Kafka clusters to cloud is perfected</td>
<td>CKafka provides the specification calculator and migration tools to help you migrate a self-built Kafka cluster to the cloud.</td>
<td>2021-07-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/41379">Migration</a></td>
</tr><tr>
<td>CKafka 2.4.2 is modified</td>
<td>CKafka 2.4.2 is replaced by CKafka 2.4.1.</td>
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
<td>The purchasable bandwidth is increased</td>
<td>The limit of purchasable bandwidth is increased from 3,200 MB/sec to 10,000 MB/sec.</td>
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
<td>Fuzzy match is supported for configuring ACL policies</td>
<td>CKafka supports configuring an ACL policy for multiple topics. Fuzzy match by topic name prefix is supported for CKafka 2.4.2 instances.</td>
<td>2021-04-14</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/39084">Configuring ACL Policy</a></td>
</tr><tr>
<td>The high-speed and stable modes are supported for instance upgrade</td>
<td>You can select either the high-speed or stable mode when upgrading an instance based on your business requirements. The time consumed in the high-speed mode is about one-tenth that consumed in the stable mode.</td>
<td>2021-04-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr><tr>
<td>Pro Edition supports advanced monitoring</td>
<td>CKafka Pro Edition supports advanced monitoring. You can view the monitoring data of metrics such as core services, production, consumption, and broker GC in the console, making it easier for Ops personnel to troubleshoot issues.</td>
<td>2021-04-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40038">Querying Advanced Monitoring (Pro Edition)</a></td>
</tr><tr>
<td>Pro Edition supports Premium Cloud Storage</td>
<td>Pro Edition supports Premium Cloud Storage.</td>
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
<td>CKafka supports upgrade at specified time</td>
<td>CKafka supports upgrading instances at specified time to avoid affecting your business.</td>
<td>2021-03-18</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40650">Upgrading Instance</a></td>
</tr><tr>
<td>CKafka supports dynamic message retention policies</td>
<td>After you configure the dynamic data retention, a certain proportion of data will automatically expire when the disk utilization reaches the specified percentage.</td>
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
<td>Pro Edition supports multi-AZ deployment</td>
<td>CKafka Pro Edition supports multi-AZ deployment. When you purchase a CKafka instance in a region with three or more AZs, you can select any two of them for multi-AZ deployment.</td>
<td>2021-02-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40243">Multi-AZ Deployment</a></td>
</tr><tr>
<td>Pro Edition supports displaying the instance upgrade progress</td>
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
<td>In case of message consumption exceptions, you can query the exception message in the CKafka console for troubleshooting.</td>
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
<td>Pro Edition (formerly Dedicated Edition) instances are available for purchase in multiple regions. Each instance is a dedicated cluster, for which parameters can be flexibly configured. Pro Edition is compatible with open-source Kafka 2.4. We offer limited-time discounts for a limited number of instances.</td>
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
<td>CKafka Dedicated Edition instances are available for purchase during open beta test</td>
<td>Dedicated Edition instances are now available for purchase in multiple regions. You can purchase them on the purchase page at the same price of Standard Edition instances without submitting a ticket.</td>
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
<td>CKafka Dedicated Edition instances are in open beta test</td>
<td><li>During the open beta test, Dedicated Edition instances (small type) are available in Chengdu region.</li><li>Dedicated instances have dedicated virtual host nodes, and the specifications of them can be customized based on business scenarios.</li></td>
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
<td>January 14, 2020</td>
<td>-</td>
</tr><tr>
<td>The instance purchase page is optimized</td>
<td><li>The purchase page supports VPC search.</li><li>The purchase page supports preset tags.</li><li>The purchase page supports displaying high-availability multi-AZ clusters.</li></td>
<td>January 13, 2020</td>
<td>-</td>
</tr><tr>
<td>Ckafka APIs are upgraded to v3.0</td>
<td><li>The new API documentation is more standardized and comprehensive.</li><li>The support for nearby access in all regions allows faster connection to Tencent Cloud services.</li></td>
<td>January 06, 2020</td>
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
<td>CKafka supports viewing the monitoring views of all partitions.</td>
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
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/32556">Data Sync</a></li></td>
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
<td>Existing technologies cannot guarantee that data will never be lost, but you can maximize the data reliability as possible as you can by using particular configuration parameters.</td>
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
<td>The terms of service are perfected</td>
<td>The new version of Service Level Agreement features clearer content and structure.</td>
<td>2019-07-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/31779">Service Level Agreement (New Version)</a></td>
</tr><tr>
<td>Topics can be automatically created</td>
<td>If “Auto-Create Topic” is enabled in the console, when you use or access the metadata of a topic that does not exist, the topic will be automatically created with the configured number of replicas and partitions.</td>
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
<td>Default alarms are supported</td>
<td>When the disk usage exceeds 90%, notifications will be sent to you through SMS, email, and Message Center by default, avoiding service unavailability if alarm policies are not configured.</td>
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
<td>The message retention period is extended</td>
<td>CKafka extends the max message retention period from one month to three months.</td>
<td>2019-03-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/40039">Creating Instance</a></td>
</tr><tr>
<td>Adds regions outside the Chinese mainland</td>
<td>CKafka adds two regions and one zone outside the Chinese mainland: Toronto, Virginia, and Silicon Valley Zone 1.</td>
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
<td>CKafka supports configuring advanced parameters for topics</td>
<td>You can configure fine-grained parameters for instance topics in the CKafka console.</td>
<td>2018-12-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/597/47583">Topic Management</a></td>
</tr></table>













## October 2018

<table><tr>
<th width="20%">Update</th>
<th width="45%">Description</th>
<th width="15%">Release Date</th>
<th width="20%">Documentation</th>
</tr><tr>
<td>Supports cross-AZ disaster recovery clusters that feature high availability</td>
<td>CKafka supports cross-AZ disaster recovery clusters that feature high availability and stability.</td>
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
