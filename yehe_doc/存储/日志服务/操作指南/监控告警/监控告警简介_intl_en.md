## Overview

CLS supports setting alarm policies for one or more log topics. An alarm policy periodically performs monitoring tasks and sends alarm notifications when the query and analysis results meet the trigger condition, so that you can find exceptions in time.

### Related concepts

| Name | Description |
| -------- | ------------------------------------------------------------ |
| Alarm policy | It is the management unit for monitoring alarms. An alarm policy contains various information such as monitoring object, monitoring period, trigger condition, alarm frequency, and notification template. |
| Monitoring object | A log topic can be used as the monitoring object, an analysis statement can be executed on the log topic, and then the analysis result can be checked. |
| Monitoring period | It is the policy execution period. Fixed period (such as every 5 minutes) and fixed time (such as 12:00 every day) are supported. |
| Trigger condition | The query and analysis result is checked, and if the trigger condition expression is true, an alarm will be triggered. |
| Alarm frequency | It is the alarm frequency after the trigger condition is met, which helps avoid frequent alarm notifications. |
| Notification template | It defines the type, recipient, and channel of notifications. The notification channel can be SMS, WeChat, phone, or email. |

>? For more information on the configuration process, please see [Configuring Alarm Policy](https://intl.cloud.tencent.com/document/product/614/50922).

### How it works

The monitoring alarm feature of CLS is based on the extended capability of [log analysis](https://intl.cloud.tencent.com/document/product/614/37803). It can extract important fields from log analysis results as monitoring metrics, and when a metric meets the trigger condition, it will trigger an alarm. For example, an analysis statement that counts the number of error logs at the `error` level is `level:error | select count(*) as ErrCount`, the number of items counted in the period `ErrCount` is used as the monitoring metric, and when `ErrCount` is greater than 10, an alarm will be triggered. As can be seen, the execution process of monitoring alarm mainly includes monitoring, determining, and alarming as detailed below:
- Monitoring: CLS periodically executes an analysis statement on the monitored log topic according to the **monitoring period** in the **alarm policy**; if there are multiple **monitoring objects** in the **alarm policy**, then multiple analysis statements will be executed at the same time when monitoring is performed.
- Determining: the analysis result is imported into the trigger condition expression. If the expression is determined to be true, the trigger condition is met, and an alarm will be triggered; if the expression is determined to be false, the trigger condition is not met, and no alarm will be triggered.
When the **trigger condition** is met, convergence will be determined based on the **alarm frequency**. An alarm notification will be sent only when the **alarm frequency** condition is also met.
- Alarming: according to the **notification template** in the **alarm policy**, the alarm notification will be sent to the corresponding recipients.



