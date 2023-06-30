**Monitoring and Alarming** help ensure high reliability, availability and performance of CVMs. When you create a CVM, Cloud Monitor will be activated for free by default, through which you can analyze and implement alarms and get CVM monitoring metrics.
This document describes the CVM monitoring and alarm features. For more information, see the [Cloud Monitor documentation](https://intl.cloud.tencent.com/document/product/248?) .

## Overview
CVM Monitoring and Alarming displays complete monitoring data of different CVM key metrics in real time. With this feature, you can have a comprehensive understanding of the resource usage, performance, and running status of the CVM instance. You can also configure custom alarm thresholds and notification rules.

## Basic Features
You can access the following CVM monitoring and alarms features in the Cloud Monitor console:

| Component | Capability | Main Features |
| ----- | -------------- | --------------------------------------- |
| [Monitor Overview](https://console.cloud.tencent.com/monitor/overview)  | Displays the overall monitoring information for Tencent Cloud services          | Provides the overall information and alarms for Tencent Cloud services                     |
| [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist)  | Displays the custom alarm policy list   | Supports alarm configuration for CVM         |
| [Cloud Virtual Machine](https://console.cloud.tencent.com/monitor/product/cvm) | Displays the specific CVM monitoring information      | Allows you to view the CVM monitoring data |
| [Dashboard](https://console.cloud.tencent.com/monitor/dashboard2/default?channel=8) | Displays the custom monitoring dashboard | Graphically displays monitoring data to facilitate the dynamic metric analysis |
| [Custom Monitoring](https://console.cloud.tencent.com/monitor/indicator-manage) | Displays the custom monitoring metrics | Allows you to view the predefined custom monitoring metrics and reported data            |
| [Traffic Monitoring](https://console.cloud.tencent.com/monitor/flow)  | Displays the traffic monitoring           | Allows you to view your overall bandwidth usage                              |

For more information about Cloud Monitor, see [Product Overview](https://intl.cloud.tencent.com/document/product/248/32799).

## Overview
- **Daily management:** log in to the Cloud Monitor console and view the running status of each monitored product.
- **Troubleshooting exceptions:** Cloud Monitor will send you alarm notifications promptly when the monitoring data reaches the alarm threshold so that you can troubleshoot the issue.
- **Timely expansion:** you can configure alarm policies for bandwidth, number of connections, disk utilization and other monitoring items to check the overall status of your Tencent Cloud services. You will receive alarm notifications when business surges and can expand your CVMs accordingly.

## Monitoring Items
To monitor instance performance benchmarks, you should monitor at least the following items. You can go to the [CVM console](https://console.cloud.tencent.com/cvm/instance) to obtain related monitoring information on the instance details page.

<table>
<thead>
<tr>
<th width="20%">Monitoring Item</th>
<th>Monitoring Metric</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>CPU usage</td>
<td>cpu_usage</td>
<td>CPU usage ratio. The data is collected and reported by the internal monitoring component of the server, making the data more accurate.</td>
</tr>
<tr>
<td>Memory utilization</td>
<td>mem_usage</td>
<td>The ratio of the actual amount of memory used by the user to the total amount of memory, excluding the memory occupied by buffer and system cache.</td>
</tr>
<tr>
<td>Private network outbound bandwidth</td>
<td>lan_outtraffic</td>
<td>Average outbound traffic per second of private ENI.</td>
</tr>
<tr>
<td>Private network inbound bandwidth</td>
<td>lan_intraffic</td>
<td>Average inbound traffic per second of private ENI.</td>
</tr>
<tr>
<td>Public network outbound bandwidth</td>
<td>wan_outtraffic</td>
<td>Average outbound traffic per second over the public network. The minimum granularity for bandwidth statistics is 10 seconds (bandwidth calculation method: total traffic in 10 seconds divided by 10 seconds).</td>
</tr>
<tr>
<td>Public network inbound bandwidth</td>
<td>wan_intraffic</td>
<td>Average inbound traffic per second of the public network.</td>
</tr>
<tr>
<td>Disk usage</td>
<td>disk_usage</td>
<td>Disk usage.</td>
</tr>
<tr>
<td>Disk I/O wait time</td>
<td>disk_io_await</td>
<td>Average wait time per disk I/O operation.</td>
</tr>
</tbody></table>

## Monitoring Data
- **Monitoring interval:** Cloud Monitor provides monitoring data at different statistical granularities, including 1 minute, 5 minutes, 1 hour, and 1 day. CVM supports the monitoring granularity of 1 minute, meaning data is collected every 1 minute. The default interval is 5 minutes.
- **Data storage:** monitoring data at a 1-minute, 5-minute, and 1-hour granularity will be retained for 31 days; monitoring data at a 1-day granularity will be retained for half a year.
- **Alarm display:** data is displayed in easy-to-read charts. The Cloud Monitor console displays the monitoring data of all products to give you a comprehensive overview of their running status.
- **Alarm settings:** you can set limits for monitoring metrics. When the condition is met, alarm notification will be sent to the recipient group promptly. For more information, see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/248/38916).
- **Dashboard settings:** you can create a monitoring metric dashboard to dynamically analyze abnormal metrics and view the metric change in real time for prompt resource expansion. For more information, see [Creating a Dashboard](https://intl.cloud.tencent.com/document/product/248/38468).
