## Overview

Cloud Monitoring (CM) provides various methods to help you identify resource exceptions and multiple channels to notify you promptly.

![](https://main.qcloudimg.com/raw/f1627024b2d2bb0f5e35321bf8e3809b.jpg)

## Locating Exceptions

### Detecting exceptions through alarms

Tencent Cloud uses monitoring and alarms to promptly detect an exception and notify you automatically. This helps keep you informed on exceptions in real time across all scenarios. You can log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/overview) and configure alarm policies for resources. For more information, see [Creating Alarm Policies](https://intl.cloud.tencent.com/document/product/248/6215).

If you have configured key performance metrics and events as alarm rules, you will be notified promptly in multiple ways via the alarm channel if an exception occurs.

Alarm policies configured with an alarm recipient group will be sent to you via SMS messages, emails, etc. Features such as repeated alarms and alarm aggregation are also supported to keep you informed while avoiding unnecessary notifications.

You can also configure the callback API feature in alarm channel to receive alarms promptly and process the alarm information.

### Detecting exceptions through monitoring charts

You need to actively analyze the historical data and average trends of performance metrics to locate exceptions through monitoring charts. If an exception is difficult to locate using alarm rules or has not been configured with alarms, you can use monitoring charts to locate it during daily health check. Compared to alarms, monitoring charts allow you to query the global influence of resource exceptions. You can subscribe key resources to the Dashboard and configure monitoring charts to highlight exceptions in different scenarios.

For some instances, you can subscribe to details views to compare the trends of instance performance data on the Dashboard.

For resource clusters, you can subscribe to the aggregated data of a cluster to view the monitoring chart of the cluster on the Dashboard, and compare it with that of a single instance in this cluster. For more information, see [Mass monitoring scenarios](https://intl.cloud.tencent.com/document/product/248/32833).

For exceptions detected through monitoring charts, you can use the sorting feature to locate specific resources related to an exception for further troubleshooting.

## Troubleshooting

### Locating exception objects on the monitoring overview page

If you receive an alarm during daily health check, you can go to [Monitoring Overview](https://console.cloud.tencent.com/monitor/overview) on the Cloud Monitoring Console.
1. Go to the overview page -> service health status module to view exceptions in each region and project.
   You can browse recent exceptions by clicking on the status of each service.
![](https://main.qcloudimg.com/raw/bef2d6f00c46f99fc18c14f8026ced30.png)
2. Click on the number of affected objects to go to the cloud product monitoring page.
![](https://main.qcloudimg.com/raw/8485dd568f76e906d768361dd438eeb0.png)
Affected resource objects are automatically filtered out on the cloud product monitoring page.
3. Click on the ID of a specific object to go to the monitoring details page, where detailed information about its historical exceptions is provided.
   - The exception timeline allows you to view the current and historical information of the affected object. This helps you troubleshoot current exceptions based on historical alarms and status changes.
   - The monitoring data for resource performance allows you to compare the current and historical data of the same metric year over year and month over month, or compare data changes of different metrics within the same period for troubleshooting.
![](https://main.qcloudimg.com/raw/2af63a2c548ae9eec8608f83145bfe0f.png)
