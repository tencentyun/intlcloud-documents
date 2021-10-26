## Overview

Log-based monitoring alarm use cases can be implemented by configuring alarm policies. This document describes how to configure an alarm policy in the CLS console.


## Prerequisites

- You have uploaded logs to a log topic.
- You have [configured an index](https://intl.cloud.tencent.com/document/product/614/39594) for the log topic.

## Directions

### Step 1. Create an alarm policy

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor).
2. On the left sidebar, choose **Monitoring Alarm*** > **Alarm Policy** to go to the alarm policy management page.
3. Click **Create** to create an alarm policy.

### Step 2. Configure a monitoring object and task

 - Monitoring object
Select the log topic to be monitored and configure the corresponding analysis statement and query time range as detailed below:
 <table>
	<tr><th>Name</th><th>Description</th><th>Example</th></tr>
	<tr>
		<td>Log topic</td>
		<td>Target log topic for which monitoring alarms are to be configured</td>
		<td>Log topic `nginx`</td>
	</tr>
	<tr>
		<td>Analysis statement</td>
		<td>Analysis statement that acts on the log topic</td>
		<td>Example 1. Get the number of logs in the `error` state<br>status:error ｜ select count(*) as ErrCount<br>Example 2. Get the average request latency of the domain name (url:aaa.com)<br>url:"aaa.com" | select avg(request_time) as Latency</td>
	</tr>
	<tr>
		<td>Query time range</td>
		<td>Data time range where the analysis statement is to be run each time</td>
		<td>Example 1. Get the number of logs in the error status in the last 5 minutes<br>Example 2. Get the average latency of the requests made in the last 1 minute</td>
	</tr>
	</table>
 - Monitoring period
The monitoring period indicates the frequency at which monitoring tasks are performed. CLS offers two ways to configure a period:
 <table>
		<tr>
		<th>Period Configuration Method</th>
		<th>Description</th>
		<th>Example</th>
	</tr>
	<tr>
		<td>Fixed frequency</td>
		<td>Monitoring tasks are performed at fixed intervals<br>Interval: 1-1440 minutes; granularity: minute</td>
		<td>Monitoring tasks are performed once every 5 minutes</td>
	</tr>
	<tr>
		<td>Fixed time</td>
		<td>Monitoring tasks are performed once at fixed points in time<br>Time point range: 00:00-23:59; granularity: minute</td>
		<td>Monitoring tasks are performed once at 02:00 every day</td>
	</tr>
 </table>

### Step 3. Configure the alarm policy

 - Trigger condition: a trigger condition expression is used to determine whether to trigger an alarm, and an alarm will be triggered when it is met.
 CLS allows you to import analysis results by using `$N.keyname`. `$N` indicates the Nth monitoring object in the current alarm policy (for more information, please see [How do I view the number?](#number)). `keyname` indicates the name of the corresponding field. For example, `$1.status>500` indicates triggering the alarm for the 1st monitoring object if the `status` field carries a value greater than 500. For more expression syntax, please see Trigger Condition Expression Syntax.
 - Alarm frequency: after the trigger condition is continuously met for a certain number of times (default value: 1; value range: 1–10), CLS will trigger a notification according to the alarm frequency. Unimportant occurrences can be avoided by configuring a threshold for the number of consecutive periods. For example, configuring meeting the trigger condition for 5 consecutive periods indicates that a notification will be triggered after the trigger condition is met 5 consecutive times. If the trigger condition expression is modified, or if the expression condition is not met during computation, the number of triggered times will be zeroed.
 - Notification convergence: you can set the interval between two notifications to avoid frequently sending alarm notifications. When the execution result of a certain monitoring task meets the trigger condition, the cumulative number of triggered periods reaches the threshold, and the requirement for the notification interval is met, a notification will be sent. For example, sending an alarm notification once every 15 minutes indicates that only one alarm notification will be received within 15 minutes.

### Step 4. Test the monitoring task

After the alarm policy is configured, click **Test Monitoring Task** to verify the analysis statement and trigger condition syntax.


If the syntax is correct, results similar to the following are displayed:



### Step 5. Configure alarm notifications

- Notification channel group
The notification channels and objects can be set by associating a notification channel group. Notifications can be sent by SMS, email, phone call, WeChat, WeCom, and custom callback API (webhook). For more information, please see Manging Notification Channel Groups.
- Notification content
By adding preset variables to notification content, you can easily understand alarm content. For the variable list and descriptions, see Notification Content Variables.

- Custom API callback configuration
If the selected notification channel group contains a custom callback API, an input box for the custom API callback configuration is displayed. For the variable list and descriptions, see [Custom API Callback Variables](https://intl.cloud.tencent.com/document/product/614/41985). There are some duplicate parts between these custom API callback variables and notification content variables, but they are not exactly the same. The variables listed in the document shall prevail when used.

- Multi-dimensional analysis
You can click **Add Item** to add the multi-dimensional analysis content of `Top 5 field values by occurrence and their percentages` or `Custom search and analysis statement` to alarm notifications. Currently, a single alarm supports up to 3 multi-dimensional analysis configurations.

Multi-dimensional analysis applies only to the logs within the query time range specified in the alarm query statement. If an alarm policy contains multiple query statements, the largest query time range prevails. For example, if the alarm policy in the following figure is triggered, multi-dimensional analysis applies only to the query time range **Last 15 Minutes** specified in the second query statement.

If you select `Top 5 field values by occurrence and their percentages`, you need to select an analysis field (only a field with indexing enabled under the current log topic can be selected).

Multi-dimensional analysis displays the top 5 content occurrences under the target field in all logs within the query time range.

If you need more flexible content configuration, select `Custom search and analysis statement`, and enter an analysis statement in the same format as that of an alarm analysis statement.

The following figure shows the final display effect of the notification on a web page.

After the configuration is completed, click **Preview** to preview the display effect of all channels.


## FAQs

<span id="number"></span>
### How do I view the number?

The number of a monitoring object is displayed on its left. The query number for the 1st object is 1, the query number for the 2nd object is 2, and so on.
