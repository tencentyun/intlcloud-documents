## Overview

Cloud Monitoring (CM) provides various methods to help you identify resource exceptions, and delivers exception information to you in real time through multiple channels.

![](http://mc.qcloudimg.com/static/img/3486dc34300abd096c209c69ab4a73b1/image.png)

## Locating Exceptions

### Detecting exceptions through monitoring alarms

Through monitoring alarms, Tencent Cloud can promptly detect an exception and automatically inform you of it. This ensures that you can detect exception information in real time across all scenarios. You can log in to [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/overview) and configure corresponding alarm policies for important resources. For more information, see [Create an alarm](https://intl.cloud.tencent.com/document/product/248/6215).

If you have configured important performance metrics and events as alarm rules, when an exception occurs, you and your system are immediately informed of this exception in multiple ways via the alarm channel.

Alarm policies configured with an alarm recipient group will reach you via SMS messages or emails. Features such as repeated alarms and alarm convergence are also supported, keeping you informed of important alarms while avoiding sending unnecessary alarm notifications.

You can also allow exception alarm information to be sent to your system by configuring the callback API feature in the alarm channel, which will allow you to further aggregate and process the exception alarm information.

### Detecting exceptions through monitoring views

Through monitoring views, you can actively detect and locate exceptions based on average trends and historical data of performance metrics. By routinely inspecting monitoring views, you can discover exceptions with no configured alarms or exceptions that are hard to locate based on alarm rules. Compared to monitoring alarms, monitoring views can help you learn about the impact of exceptions on resources on a global scale. You can highlight resource exception information in various scenarios by subscribing important resources to the dashboard and properly configuring charts.  <!--For more information, see [Configure Dashboards]().-->

For some instances, you can subscribe to instance details views to compare the trends of instance performance data on a dashboard.

For resource clusters, you can subscribe to the aggregated data of a cluster to see the overall monitoring view of the cluster on the dashboard, and compare it with that of a single instance in this cluster. For more information, see [Best practices for large-scale monitoring scenarios](https://intl.cloud.tencent.com/document/product/248/32833).

By using the list sorting feature, you can locate the specific resources of any exception detected through a view and determine the impact of the exception for further troubleshooting.

## Troubleshooting

### Locating exception objects on the monitoring overview page

When conducting routine inspection or when receiving an alarm message, you can log into the loud monitoring console and go to the [Monitoring Overview](https://console.cloud.tencent.com/monitor/overview) page.
1. On the **Monitoring Overview** page, locate **Service Health Status in Last 24 Hours** to view the resource exceptions of each region and project.
   You can browse recent exceptions by using the exception information overview feature.
![](https://main.qcloudimg.com/raw/6c2b2796c4523c28f2e481923762b9a0.png)
2. Click the number of exception objects to access the cloud product monitoring page.
![](https://main.qcloudimg.com/raw/8485dd568f76e906d768361dd438eeb0.png)
Abnormal resource objects are automatically filtered out on the cloud product monitoring page.
3. Click the ID of a specific object to access the monitoring details page of the object, where details are provided to rewind the exception history and help locate exceptions.
   - Exception timeline allows you to view the current and historical information of the abnormal object, and helps you troubleshoot current exceptions based on historical alarms and status change information.
   - Resource performance monitoring data provides you with the most comprehensive resource performance data. You can perform a year-over-year or month-over-month comparison between the current data and historical data of the same metric, or compare data changes of different metrics within the same period for troubleshooting.
![](https://main.qcloudimg.com/raw/2af63a2c548ae9eec8608f83145bfe0f.png)


### Locating exception objects through dashboards

Log into [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/overview). In the left sidebar, click **Dashboard** to access the dashboard management page.

1. When you identify an abnormal trend in the monitoring view, click the time period when the exception occurs. A sorting list of corresponding instances is displayed below the chart. You can locate the specific abnormal objects based on the sorting list.

3. Click the name of an object in the sorting list to access the monitoring details page of the object, where details are provided to rewind the exception history and help locate exceptions.
   - Exception timeline allows you to view the current and historical information of the abnormal object, and helps you troubleshoot current exceptions based on historical alarms and status change information.
   - Resource performance monitoring data provides you with the most comprehensive resource performance data. You can perform a year-over-year or month-over-month comparison between the current data and historical data of the same metric, or compare data changes of different metrics within the same period for troubleshooting.
![](https://main.qcloudimg.com/raw/ae7b2d1aacdf184d14d476eec8d0dd32.png)
