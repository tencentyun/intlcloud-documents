**Monitoring and Alarming** help ensure high reliability, availability and performance of CVMs. This document describes the CVM monitoring and alarm features. For more information, please see the [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248?) documentation.

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

For more information about Cloud Monitor, please see [Product Overview](https://intl.cloud.tencent.com/document/product/248/32799)

## Use Cases
- **Daily management:** log in to the Cloud Monitor console and view the running status of each monitored product.
- **Troubleshooting exceptions:** Cloud Monitor will send you alarm notifications promptly when the monitoring data reaches the alarm threshold so that you can troubleshoot the issue.
- **Timely expansion:** you can configure alarm policies for bandwidth, number of connections, disk utilization and other monitoring items to check the overall status of your Tencent Cloud services. You will receive alarm notifications when business surges and can expand your CVMs accordingly.

## Monitoring Items
To benchmark instance performance, you should at least monitor the following items:

| Monitoring Item | Monitoring Metric |
|---------|---------|
| CPU utilization | cpu_usage |
| Memory utilization | mem_usage |
| Private network outbound bandwidth | lan_outtraffic |
| Private network inbound bandwidth| lan_intraffic |
| Public network outbound bandwidth | wan_outtraffic |
| Public network inbound bandwidth | wan_intraffic |
| Disk utilization | disk_usage |
| Disk I/O waiting time | disk_io_await |

## Monitoring Data
- **Monitoring interval:** Cloud Monitor provides monitoring data at different statistical granularities, including 1 minute, 5 minutes, 1 hour, and 1 day. CVM supports the monitoring granularity of 1 minute, meaning data is collected every 1 minute. The default interval is 5 minutes.
- **Data storage:** monitoring data at a 1-minute, 5-minute, and 1-hour granularity will be retained for 31 days; monitoring data at a 1-day granularity will be retained for half a year.
- **Alarm display:** data is displayed in easy-to-read charts. The Cloud Monitor console displays the monitoring data of all products to give you a comprehensive overview of their running status.
- **Alarm settings:** you can set limits for monitoring metrics. When the condition is met, alarm notification will be sent to the recipient group promptly. For more information, please see [Configuring Alarm Policies](https://intl.cloud.tencent.com/document/product/248/38908).
-  **Dashboard settings:** you can create a monitoring metric dashboard to dynamically analyze abnormal metrics and view the metric change in real time for prompt resource expansion. For more information, see [Creating a Dashboard](https://intl.cloud.tencent.com/document/product/248/38468).
