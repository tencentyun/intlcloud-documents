Tencent Cloud Advisor is a ready-to-use product that assesses the risk of cloud resources. Based on the [CAM Service Role Authorization](https://intl.cloud.tencent.com/document/product/598/19421) mechanism, Advisor allows you to analyze potential risks of your cloud resources with one click. It also provides resource optimization advice online according to your business needs so that you can improve your system security and service reliability. 

## Feature Overview

Advisor improves business continuity by providing various assessment items, flexible assessment configurations, and systematic optimization advice.

#### Various assessment items

Advisor supports multiple Tencent Cloud services from various dimensions (such as security, reliability, and service restriction), covering dozens of assessment items. Advisor is constantly upgrading to support more services. Currently, the following Tencent Cloud services and assessment items are supported.

<table>
<thead>
<tr>
<th>Type</th>
<th>Service</th>
<th>Assessment Item</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=11>Security
</td>
<td  rowspan=2>COS</td>
<td>COS sub-account access permission not set</td>
</tr>
<tr>
<td>COS sub-account access permission not restricted</td>
</tr>
<tr>
<td rowspan=3>CVM</td>
<td>CVM public access not restricted</td>
</tr>
<tr>
<td>CVM public network ports with high risks enabled</td>
</tr>
<tr>
<td>CVM public login not restricted</td>
</tr>
<tr>
<td  rowspan=2>Elasticsearch Service</td>
<td>Elasticsearch public access not restricted</td>
</tr>
<tr>
<td>Kibana public access not restricted</td>
</tr>
<td  rowspan=2>TencentDB for MySQL</td>
<td>Root account security of TencentDB for MySQL</td>
</tr>
<tr>
<td>High-risk operations of TencentDB for MySQL not restricted</td>
</tr>
<td  rowspan=2>TencentDB for Redis</td>
<td>Default account security of TencentDB for Redis</td>
</tr>
<tr>
<td>High-risk commands of TencentDB for Redis not disabled</td>
</tr>
<td rowspan=6>Reliability
</td>
<td>COS</td>
<td>COS bucket versioning</td>
<tr>
<td>CVM</td>
<td>System disk snapshot of CVM</td>
</tr>
<td>Elasticseach Service</td>
<td>Automatic snapshot backup of ES cluster</td>
</tr>
<td  rowspan=2>TencentDB for MySQL</td>
<td>Automatic backup of TencentDB for MySQL</td>
</tr>
<tr>
<td>Cross-region disaster recovery of TencentDB for MySQL</td>
</tr>
<td rowspan=1>TencentDB for Redis</td>
<td>Automatic backup of TencentDB for Redis</td>
</tr>
<tbody><tr>
<td rowspan=8>Service Restriction
</td>
<td>CBS</td>
<td>CBS storage capacity</td>
<tr>
<td>CVM</td>
<td>CVM instance expired</td>
</tr>
<td  rowspan=2>TencentDB for MongoDB</td>
<td>TencentDB for MongoDB instance expired</td>
</tr>
<tr>
<td>Storage capacity of TencentDB for MongoDB</td>
</tr>
<td  rowspan=2>TencentDB for MySQL</td>
<td>TencentDB for MySQL instance expired</td>
</tr>
<tr>
<td>Disk capacity of TencentDB for MySQL</td>
</tr>
<td  rowspan=2>TencentDB for Redis</td>
<td>TencentDB for Redis instance expired</td>
</tr>
<tr>
<td>Memory capacity of TencentDB for Redis</td>
</tr>
</tr>
</tbody></table>



#### Flexible assessment configurations

- Assessment items can be added, deleted, or ignored as needed. Concise assessment reports allow you to focus on the key metrics.
- You can ignore specific cloud resources to focus on assessing the execution status of key resources.

#### Systematic optimization advice

With the assessment results as well as Tencent Cloud’s years of best practices in customer services, Advisor offers systematic, targeted, and operable optimization advice to help you take preventive measures and improve business continuity.

