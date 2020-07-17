## Overview

Cloud Monitoring (CM) provides various methods to help you identify resource exceptions and delivers exception information to you in real time through multiple channels.

![](https://main.qcloudimg.com/raw/f1627024b2d2bb0f5e35321bf8e3809b.jpg)

## Locating Exceptions

### Detecting exceptions through monitoring alarms

Through monitoring alarms, Tencent Cloud can promptly detect an exception and automatically inform you of it. This ensures that you can detect exception information in real time across all scenarios. You can log in to the [Cloud Monitor Console](https://console.cloud.tencent.com/monitor/overview) and configure corresponding alarm policies for important resources. For more information, see [Create an alarm policy](https://intl.cloud.tencent.com/document/product/248/6215).

If you have configured important performance metrics and events as alarm rules, when an exception occurs, you and your system are immediately informed of this exception in multiple ways via the alarm channel.

Alarm policies configured with an alarm recipient group will reach you via SMS messages or emails. Features such as repeated alarms and alarm convergence are also supported, keeping you informed of important alarms while avoiding unnecessary alarm notifications.

You can also allow exception alarm information to be sent to your system by configuring the callback API feature in the alarm channel, which will allow you to further aggregate and process the exception alarm information.

### Detecting exceptions through monitoring charts

When locating exceptions through monitoring charts, you need to actively consult the average trends and historical data of performance metrics to locate exceptions. Exceptions for which alarms are not configured or are difficult to locate using alarm rules can be discovered through monitoring charts during daily inspections. In contrast to alarms, monitoring charts can help you determine the global influence of resource exceptions. You can highlight resource exception information for various scenarios by subscribing to important resources, properly configuring their monitoring charts, and displaying these charts on the dashboard.

For some instances, you can subscribe to instance details views to compare the trends of instance performance data on the dashboard.

For resource clusters, you can subscribe to the aggregated data of a cluster to show the overall monitoring chart of the cluster on the dashboard. Then, you can compare it with that of a single instance in this cluster. For more information, see [Best practices for large-scale monitoring scenarios](https://intl.cloud.tencent.com/document/product/248/32833).

By using the chart sorting feature, you can locate the specific resources related to any exception detected through a chart and determine the impact of the exception for further troubleshooting.

## Troubleshooting

### Locating exception objects on the monitoring overview page

When conducting routine inspections or when you receive alarm messages, you can log in to the cloud monitoring console and go to the [Monitoring Overview](https://console.cloud.tencent.com/monitor/overview) page.
1. Go to the overview page -> cloud service health status module to see the resource exceptions in each region and project.
   You can browse recent exceptions by using the exception information overview feature.
![](https://main.qcloudimg.com/raw/bef2d6f00c46f99fc18c14f8026ced30.png)
2. Click the number of exception objects to access the cloud product monitoring page.
![](https://main.qcloudimg.com/raw/8485dd568f76e906d768361dd438eeb0.png)
Abnormal resource objects are automatically filtered out for display on the cloud product monitoring page.
3. Click the ID of a specific object to access the monitoring details page of the object, where details are provided to trace the exception history and help locate exceptions.
   - The exception timeline allows you to view the current and historical information of the abnormal object. This helps you troubleshoot current exceptions based on historical alarms and status change information.
   - Resource performance monitoring data provides you with the most comprehensive resource performance data. You can perform a year-over-year or month-over-month comparison between the current data and historical data of the same metric, or compare data changes of different metrics within the same period for troubleshooting.
![](https://main.qcloudimg.com/raw/2af63a2c548ae9eec8608f83145bfe0f.png)
