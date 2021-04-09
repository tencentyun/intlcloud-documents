Tencent Cloud’s Cloud Monitor (CM) is a service that can monitor Tencent Cloud service resources in real time and generate alarms.

CM provides users with a platform for the centralized monitoring of [CVMs](https://intl.cloud.tencent.com/product/cvm), cloud databases, and other Tencent Cloud services. CM displays comprehensive information such as the cloud service resource usage, application performance, and cloud service operation status. It also supports features such as multi-metric monitoring, custom alarms, cross-region and cross-project instance grouping, and custom dashboards for visual monitoring. With these features, CM can help you detect emergencies in running Tencent Cloud services in a timely manner, enhancing system stability, improving OPS efficiency, and reducing OPS costs.

CM collects and obtains monitoring metric data from all dimensions and displays the data in visual charts to help you better understand the health and performance of Tencent Cloud services. Moreover, after you configure alarm rules, CM can instantly notify you of business exceptions through message push, so that you can fully control the usage and health of Tencent Cloud service resources without secondary development. To learn more about CM and obtain relevant monitoring data, go to the [CM console](https://console.cloud.tencent.com/monitor/overview), [API Category](https://intl.cloud.tencent.com/document/product/248/33873), or [Tencent Cloud CLI](https://intl.cloud.tencent.com/document/product/1013).

## Basic Features

You can access the following features in the Cloud Monitor console:



<table>
<thead>
<tr>
<th>Component</th>
<th>Capability</th>
<th>Main Feature</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">Monitoring overview</td>
<td>Displays the overall monitoring information for Tencent Cloud services</td>
<td>Displays the overall information and alarms for Tencent Cloud services at a glance</td>
</tr>
<tr>
<td nowrap="nowrap">Dashboard</td>
<td nowrap="nowrap"><li>Preset monitoring dashboard<br></li><li>Custom monitoring dashboard</li></td>
<td>Provides flexible custom view features applicable to multiple monitoring scenarios, such as cross-instance data aggregation, real-time/historical data display, similar metric comparison, and linked charts</td>
</tr>
<tr>
<td>Alarm management</td>
<td>Centralized alarm management</td>
<td>Allows you to configure alarm rules for monitoring metrics, view historical alarms, and receive alarm notifications</td>
</tr>
<tr>
<td>Tencent Cloud service monitoring</td>
<td>Displays the specific monitoring information of Tencent Cloud services</td>
<td>Allows users to view the monitoring details and alarm details of cloud resources under the user’s account</td>
</tr>
<tr>
<td>Custom monitoring</td>
<td>Displays the monitoring metric data customized by the user</td>
<td>Provides entries to more data for self-service data reporting in addition to regular monitoring metrics</td>
</tr>
<tr>
<td>Event monitoring</td>
<td>Displays the important event information of Tencent Cloud services and platforms</td>
<td>Provides the reporting, query, and alarm features for event-type data</td>
</tr>
<tr>
<td>Traffic monitoring</td>
<td>Displays the traffic information</td>
<td>Displays the traffic usage of the public network outbound bandwidth</td>
</tr>
</tbody></table>



## Architecture

CM provides basic metrics monitoring and data storage services for users. It is a space for storing the data of all cloud resources. CM collects and obtains the monitoring metric data for Tencent Cloud services through various channels. After processing the data, it stores the data in a repository. You can go to the [CM console](https://console.cloud.tencent.com/monitor/overview) to view the monitoring data in charts or pull metric data through APIs. You can also [create alarm policies](https://intl.cloud.tencent.com/document/product/248/38908) to define how to handle the monitoring data via the alarm processing system and enable the system to send alarm notifications when the monitoring data triggers the alarm conditions.

**Architecture Diagram:**
![](https://main.qcloudimg.com/raw/d6dadcb6df11651053ce31ff9f037895.jpg)



## Supported Services

Currently, CM can automatically monitor the following services. Once you start a service, its metric data will automatically be sent to CM.

>? Currently, monitoring statistics are collected at granularities of one minute, five minutes, one hour, and one day. Most services, such as Cloud Virtual Machine (CVM) and cloud databases, support the monitoring granularity of one minute, which means that monitoring statistics are collected every minute. Some other products only support a granularity of five minutes, which means that monitoring statistics are collected every five minutes.
> Monitoring in seconds will be available to certain services. TencentDB for MySQL instances now support free monitoring at the granularity of five seconds. One month before the official billing starts, we will inform you via SMS, the Tencent Cloud Message Center, and email.

- [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213)
- [Cloud Block Storage](https://intl.cloud.tencent.com/document/product/362)(only when mounted on a running CVM)
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214)
- Cloud databases
	- [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)
	- [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/240)
	- [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239)
	- [Game Database TcaplusDB](https://intl.cloud.tencent.com/document/product/1016)
	- [Data Subscription](https://intl.cloud.tencent.com/document/product/571/8774)
- [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845)
- [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/215)
	- [NAT Gateway](https://intl.cloud.tencent.com/document/product/1015)
	- [Peering Connection](https://intl.cloud.tencent.com/document/product/553)
	- Cross-region connection over the classic network
	- [VPN Gateway](https://intl.cloud.tencent.com/document/product/1037)
	- [VPN Connections](https://intl.cloud.tencent.com/document/product/1037)
	- [Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216)
	- [Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586)
	- Anycast EIPs
- [Direct Connect](https://intl.cloud.tencent.com/document/product/216)
	- Connections
	- Dedicated tunnels
- Messaging service
	- Topic subscription
	- Queues
- [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436)
- [Cloud File Storage](https://intl.cloud.tencent.com/document/product/582)
- [Web Application Firewall](https://intl.cloud.tencent.com/document/product/627)
