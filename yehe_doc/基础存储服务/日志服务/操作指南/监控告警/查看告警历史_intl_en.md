This document shows how to view alarm records in the CLS console.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/monitor/notice/create).
2. On the left sidebar, click **Monitoring Alarm** > **Alarm Records** to enter the alarm records page.



## Notes

CLS allows you to view the alarm records in the last 30 days.

### Alarm statistics

**Alarm Statistics** displays important information on alarms in the current region, such as alarm policy statistics and monitoring task execution. The metrics are as detailed below:

| Metric             | Description                                                         |
| -------------------- | ------------------------------------------------------------ |
| Total Alarm Policy Executions     | Number of alarm policies executed over the statistical time range                         |
| Alarm Policy Executions     | Number of times the query and analysis statement in the alarm policy is executed over the statistical time range          |
| Failed Alarm Policy Executions | Number of alarm policy execution failures over the statistical time range. Execution failures include AlarmConfigNotFound, QuerySyntaxError, QueryError, QueryResultParseError, ConditionSyntaxError, ConditionEvaluateError, and ConditionValueTypeError. For more information, please see [Execution Result Status Codes](#result) |
| Times of Trigger Conditions Met     | Number of times the query and analysis statement in the alarm policy is executed successfully and the result returned meets the trigger condition over the statistical time range |
| Notifications Triggered by the Alarm Policy | Number of times notifications are triggered by the execution of the alarm policy over the statistical time range             |
| Top 10 Alarm Policies by Number of Notifications | Top 10 alarm policies in terms of the number of times notifications are triggered over the statistical time range            |


### Historical records

Once an alarm policy takes effect, it will periodically perform monitoring tasks, and the details of executions of each monitoring task will be recorded in **Historical Records**, including the result of each execution. By viewing the records of alarm policy execution, you can easily trace back historical alarming tasks.

>? CLS allows you to view the records in the last 30 days.
>


<span id="result"></span>
Policy execution results are described as follows.

| Execution Result                | Description                                                         |
| ----------------------- | ------------------------------------------------------------ |
| AlarmConfigNotFound     | The alarm policy configuration is missing. Please check whether the alarm policy and monitoring object have been configured correctly.     |
| QuerySyntaxError        | The analysis statement of the monitoring object has a syntax error. Please check whether the statement is correct. For more information on the syntax, please see [Overview](https://intl.cloud.tencent.com/document/product/614/37803). |
| QueryError              | The analysis statement is not executed properly. Please check the analysis statement and the index configuration of the log topic.         |
| QueryResultParseError   | Failed to parse the analysis result format.                                         |
| ConditionSyntaxError    | The trigger condition expression has a syntax error. Please check [the syntax format of the expression](https://www.tencentcloud.com/document/product/614/39576). |
| ConditionEvaluateError  | An error occurred while computing the trigger condition. Please check whether the imported variable exists in the analysis result     |
| ConditionValueTypeError | The evaluation result of the trigger condition is not a Boolean value. Please check whether the trigger condition expression is correct.       |
| EvalTimesLimited        | The trigger condition hasn't been met even after it has been computed more than 1,000 times.                 |
| QueryResultUnmatch      | The analysis result for the current monitoring period doesn't meet the alarm trigger condition.                   |
| UnreachedThreshold      | The alarm trigger condition is met, but the alarm convergence threshold has not been reached, so no alarm notification is sent.<li>HappenThreshold Unreached: the period convergence condition is not met; for example, an alarm is triggered only if the trigger condition is met in 5 consecutive monitoring periods.</li><li>AlertThreshold Unreached: the alarm interval condition is not met; for example, an alarm will be triggered once every 15 minutes.</li> |
| TemplateUnmatched       | The alarm configuration information doesn't match the notification template. Specific causes include:<li>TypeUnmatched: the alarm notification type (alarm triggered or alarm cleared) doesn't match the notification template, so no alarm notification is sent.</li><li>TimeUnmatched: the alarm notification time period doesn't match the notification template, so no alarm notification is sent.</li><li>SendFail: the notification failed to be sent.</li> |
| Matched                 | The alarm condition is met, and the alarm notification is sent successfully.                                 |

**Policy alarm states are described as follows.**

| Alarm State | Description   |
|-----------|---|
| Uncleared | The system continuously meets the trigger condition and triggers an alarm. |
| Cleared | The current monitoring period does not meet the trigger condition. |
| Invalid | The alarm policy is deleted or modified. |

