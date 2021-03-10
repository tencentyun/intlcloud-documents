Log-based monitoring alarm use cases can be implemented by configuring alarm policies. This document describes how to configure an alarm policy in the CLS console.
## Prerequisites
- Logs have been uploaded to a certain [log topic](https://console.cloud.tencent.com/cls/logset/desc).
- [An index has been configured](https://intl.cloud.tencent.com/document/product/614/39594) for the log topic.

## Configuration Process

### Step 1. Create an alarm policy

Log in to the [CLS console](https://console.cloud.tencent.com/cls/alarm) and click **Monitoring Alarm** on the left sidebar to create an alarm policy.

### Step 2. Configure a monitoring rule

#### Monitoring object
Select the log topic to be monitored and configure the corresponding analysis statement and query time range as detailed below:

| Name         | Description                                      | Example                                                         |
| ------------ | ----------------------------------------- | ------------------------------------------------------------ |
| Log topic     | Target log topic for which to configure monitoring alarms            | Log topic `nginx`                                         |
| Analysis statement     | Analysis statement that acts on the log topic | Example 1. Get the number of logs in the `error` status<br>status:error | select count(*) as ErrCount<br>Example 2. Get the average request latency of the domain name (url:aaa.com)<br>url:"aaa.com" \| select avg(request_time) as Latency |
| Query time range | Data time range in which to run the analysis statement             | Example 1. Get the number of logs in the `error` status in the last 5 minutes<br>Example 2. Get the average latency of the requests made in the last 1 minute |

#### Monitoring period

The monitoring period indicates the frequency at which monitoring tasks are performed. CLS offers two ways to configure a period:

| Period Configuration Method | Description                                                         | Example                    |
| ------------ | ------------------------------------------------------------ | ----------------------- |
| Fixed frequency     | Monitoring tasks are performed at fixed intervals<br>Interval: 1–1440 minutes; granularity: minute | Monitoring tasks are performed once every 5 minutes   |
| Fixed time     | Monitoring tasks are performed at fixed time points<br>Time point range: 00:00–23:59; granularity: minute | Monitoring tasks are performed at 02:00 every day |

### Step 3. Configure the alarm policy

#### Trigger condition

A trigger condition expression is used to determine whether to trigger an alarm, and an alarm will be triggered when it is met.
CLS allows you to import analysis results by using `$N.keyname`.
- $N: it indicates the Nth monitoring object in the current alarm policy (for more information, please see [How do I view the number?](#number)).
- keyname: it indicates the corresponding field name; for example, `$1.status>500` indicates that an alarm will be triggered when the `status` field value of the monitoring object numbered 1 is greater than 500. For more information on the expression syntax, please see Trigger Condition Expression.

#### Alarm frequency

After the trigger condition is continuously met for a certain number of times (default value: 1; value range: 1–10), CLS will trigger a notification according to the alarm frequency. Unimportant occurrences can be avoided by configuring a threshold for the number of consecutive periods. For example, configuring meeting the trigger condition for 5 consecutive periods indicates that a notification will be triggered after the trigger condition is met 5 consecutive times. If the trigger condition expression is modified, or if the expression condition is not met during computation, the number of triggered times will be zeroed.

#### Notification convergence

You can set the interval between two notifications to avoid frequently sending alarm notifications. When the execution result of a certain monitoring task meets the trigger condition, the cumulative number of triggered periods reaches the threshold, and the requirement for the notification interval is met, a notification will be sent. For example, sending an alarm notification once every 15 minutes indicates that only one alarm notification will be received within 15 minutes.



### Step 4. Configure alarm notifications

The notification method and recipients can be set by associating a notification template. Notifications can be sent by email, SMS, phone, or WeChat. For more information, please see [Creating Notification Template](https://intl.cloud.tencent.com/document/product/614/39582).

## FAQs
<span id="number"></span>
### How do I view the number?

On the monitoring rule page, the number of a monitoring object is displayed on its left. The query number for the 1st object is 1, the query number for the 2nd object is 2, and so on.
