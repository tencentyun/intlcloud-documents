## Overview

This document describes how to configure an alarm policy based on logs so that alarms can be sent when certain conditions are met, such as when there are too many error logs or the API response time is too long.

## Prerequisites

- You have uploaded the log to a log topic and [configured the index](https://intl.cloud.tencent.com/document/product/614/39594).
- The log topic is not in [STANDARD_IA](https://intl.cloud.tencent.com/document/product/614/42004) storage, which doesn't support alarm policy configuration. An alarm policy requires SQL statements. We recommend that you structure logs as instructed in [Collection Overview](https://intl.cloud.tencent.com/document/product/614/31652).
- You have logged in to the CLS console and entered the [Alarm Policy](https://console.cloud.tencent.com/cls/alarm/list) page.

## Directions

On the **Alarm Policy** page, click **Create** and configure the following items.


### Configuring the monitoring object and monitoring task

 - **Monitoring Object**: Select the target log topic(s). It can be determined whether the trigger conditions are met separately for each log topic. You can select up to 20 log topics in the same region. If multiple log topics meet the trigger conditions at the same time, multiple alarms will be generated at a time.
 - **Monitoring Task**
  - **Query Statement**: It is used for log topics and needs to contain the analysis statement (i.e., SQL statement as described in [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803)).
    - Example 1: To count logs with errors, use `status:error | select count(*) as ErrCount`.
    - Example 2: To calculate the average response time of the domain name "domain:aaa.com", enter `domain:"aaa.com" | select avg(request_time) as Latency`.
  - **Query Time Range**: It indicates the time range of data for query by the query statement, which can be up to the last 24 hours.
  - **Trigger Condition**: An alarm is triggered when the trigger condition is met. In the condition expression, `$N.keyname ` is used to reference the query statement result. Here, `$N` indicates the Nth query statement in the current alarm policy, and `keyname` indicates the corresponding field name. For more information on the expression syntax, see [Trigger Condition Expression](https://intl.cloud.tencent.com/document/product/614/39576).
    - Example 1: To trigger an alarm when the number of logs with errors exceeds 10, enter `$1.ErrCount > 10`. Here, `$1` indicates the first query statement, and `ErrCount` indicates the `ErrCount` field in the result.
    - Example 2: To trigger an alarm when the domain name "domain:aaa.com" takes more than 5 seconds on average to respond, enter `$2.Latency > 5`. Here, `$2` indicates the first query statement, and `Latency` indicates the `Latency` field in the result.
  - **Trigger by Group**: It specifies whether the trigger condition expression should trigger alarms by group. When it is enabled, if multiple results of the query statement meet the trigger condition, the results will be grouped based on the group field, and an alarm will be triggered for each group.
    For example, if the query statement 2 is `* | select avg(request_time) as Latency,domain group by domain order by Latency desc limit 5`, and multiple results are returned:
<table>
<thead>
<tr><th>Latency</th><th>Domain</th></tr>
</thead>
<tbody>
<tr><td>12.56</td><td>aaa.com</td></tr>
<tr><td>9.45</td><td>bbb.com</td></tr>
<tr><td>7.23</td><td>ccc.com</td></tr>
<tr><td>5.21</td><td>ddd.com</td></tr>
<tr><td>4.78</td><td>eee.com</td></tr>
</tbody>
</table>
If the trigger condition is `$2.Latency > 5`, then it is met by four results.
<ul>
<li>If triggering by group is not enabled, only one alarm will be triggered when the trigger condition is met by one of the above execution results.</li>
<li>If it is enabled and the results are grouped by the `domain` field, four alarms will be triggered separately for the above execution results.</li>
</ul>
>!  
> - When triggering by group is enabled, the trigger condition may be met by multiple results, and a large number of alarms will be triggered, leading to an alarm storm. Therefore, configure the group field and trigger condition appropriately.
> - When specifying the group field, you can divide execution results into up to 1,000 groups. No alarms will be triggered for excessive groups.
>
  - **Execution Cycle**: It indicates the execution frequency of the monitoring task, which can be configured in the following two ways:
 <table>
		<tr>
		<th>Period Configuration Method</th>
		<th>Description</th>
		<th>Example</th>
	</tr>
	<tr>
		<td>Fixed frequency</td>
		<td>Monitoring tasks are performed at fixed intervals<br>Interval: 1–1,440 minutes. Granularity: Minute</td>
		<td>Monitoring tasks are performed once every 5 minutes</td>
	</tr>
	<tr>
		<td>Fixed time</td>
		<td>Monitoring tasks are performed once at fixed points in time<br>Time point range: 00:00–23:59. Granularity: Minute</td>
		<td>Monitoring tasks are performed once at 02:00 every day</td>
	</tr>
 </table>

### Configuring multi-dimensional analysis

When an alarm is triggered, raw logs can be further analyzed through multi-dimensional analysis, and the analysis result can be added to the alarm notification to facilitate root cause discovery. The multi-dimensional analysis doesn't affect the alarm trigger condition.

| Multi-dimensional Analysis Type       | Description                                                         |
| ------------------ | ------------------------------------------------------------ |
| Related raw logs       | Get the raw logs that meet the search condition of the query statement. The log field, quantity, and display form can be configured.<br />For example, when an alarm is triggered by too many error logs, you can view the detailed logs in the alarm. |
| Top 5 field values by occurrence and their percentages | For all the logs within the time range when the alarm is triggered, group them based on the specified field and get the top 5 field values and their percentages.<br />For example, when an alarm is triggered by too many error logs, you can get the top 5 URLs and top 5 response status codes. |
| Custom search and analysis     | Execute the custom search and analysis statement for all the logs within the time range when the alarm is triggered.<br />Example 1: `* | select avg(timeCost) as time,URL group by URL` gets the request duration of each API.<br />Example 2: `status:>499` gets error logs. |

>? The "related raw logs" and "top 5 field values by occurrence and their percentages" options support the automatic association with the search condition of the specified query statement (excluding the analysis statement, i.e., SQL filter condition), so as to indicate to perform multi-dimensional analysis on raw logs that meet what conditions.
>

### Configuring an alarm notification

- **Alarm Frequency**:
 - Duration: A notification will be sent only after the trigger condition is met constantly a certain number of times (which can be 1–10 and is 1 by default).
 - Interval: No notifications will be sent within the specified interval after the last notification. For example, the **an alarm will be triggered every 15 minutes** option indicates that only one alarm will be sent within 15 minutes.
- **Notification Group**:
The notification channels and objects can be set by associating a notification channel group. Notifications can be sent by SMS, email, phone call, Weixin, WeCom, and custom callback API (webhook). For more information, please see [Managing Notification Groups](https://intl.cloud.tencent.com/document/product/614/41987).
- **Notification Content**:
By adding preset variables to the notification content, you can add specified information to the alarm notification. For more information on variables, see [Alarm Notification Variable](https://intl.cloud.tencent.com/document/product/614/41984).
- **Custom Webhook Configuration**:
If the selected notification group contains a custom webhook, the custom webhook input box will be displayed. You can customize the request header and request body there, which will be used by CLS to call the specified API when an alarm is triggered. In the request header and body, you can use [notification content variables](https://intl.cloud.tencent.com/document/product/614/41984) to send relevant data to the specified API.


## Best Practices

[Setting Alarm Trigger Conditions by Time Period](https://www.tencentcloud.com/document/product/614/54948)
[Setting Interval-Valued Comparison and Periodically-Valued Comparison as Alarm Trigger Conditions](https://www.tencentcloud.com/document/product/614/54949)
