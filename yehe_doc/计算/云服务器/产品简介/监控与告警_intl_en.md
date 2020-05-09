**Monitoring and Alarms** help ensure high reliability, high availability, and high performance of CVMs. This document describes the monitoring and alarm features provided by CVM. For more details, please see [Cloud Monitor](https://cloud.tencent.com/document/product/248) product documentation.

## Overview
CVM monitoring and alarms are management tools used to monitor CVM in real time. The monitoring and alarm features can display the most complete and detailed monitoring data, extract key metrics from the CVM in real time, and display them in monitoring charts. The features help you gain a comprehensive understanding of the resource usage, performance, and operating status of the CVM. You can also configure custom alarm thresholds and send notifications based on your custom rules.

## Basic Features
On the console, you can access the following features of CVM monitoring and alarms:

| Module | Capability | Main Features |
| ----- | -------------- | --------------------------------------- |
| Monitor Overview | Cloud Monitor overview | General overview, alarm overview, and monitoring information overview |
| My Alarms | Supports custom alarm threshold | Supports alarm configuration for CVM |
| Cloud Product Monitoring | Visualizes cloud product monitoring | Views CVM monitoring |
| Custom Monitoring | Views custom monitoring metrics | Views custom monitoring metrics and reported data |
| Data Usage Monitoring | Data usage monitoring | View the user's overall bandwidth information |

For more information, please see Cloud Monitor [Overview](https://intl.cloud.tencent.com/document/product/248/32799).

## Application Scenarios
- **Daily management:** Log in to the Cloud Monitoring Console to view the monitoring information of all your cloud products.
- **Timely handling of exceptions:** Cloud Monitor will send you alarm notifications promptly when the monitoring data reaches the alarm threshold so that you can troubleshoot the causes.
- **Timely expansion:** You can configure alarm policies for bandwidth, the number of connections, disk utilization and other monitoring items to check the overall status of your Tencent Cloud services. You will receive alarm notifications when business surges and can expand your CVMs accordingly.
 
## Monitoring Items
To benchmark instance performance, you should at least monitor the following items:

| Monitoring Item | Monitoring Metric | 
|---------|---------|
| CPU utilization | cpu_usage | 
| Memory utilization | mem_usage |
| Outbound bandwidth of private network | lan_outtraffic |
| Inbound bandwidth of private network | lan_intraffic |
| Outbound bandwidth of public network | wan_outtraffic |
| Inbound bandwidth of public network | wan_intraffic |
| Disk utilization | disk_usage |
| Disk I/O waiting time | disk_io_await |

## Monitoring Data
- **Monitoring interval:** Cloud Monitor provides monitoring data at different statistical granularities, including 1 minute, 5 minutes, 1 hour, and 1 day. CVM supports the monitoring granularity of 1 minute, meaning data is collected every 1 minute. The default interval is 5 minutes.
- **Data storage**: monitoring data at a 1-minute, 5-minute, and 1-hour granularity will be retained for 31 days; monitoring data at a 1-day granularity will be retained for half a year.
- **Alarm display:** data is displayed in easy-to-read charts. Cloud Monitoring Console includes the monitoring data of all products to give you a comprehensive overview of their running status.
- **Alarm setting:** you can set limits for monitoring metrics. When the condition is met, alarm notification will be sent to the recipient group promptly. For more information, please see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).
