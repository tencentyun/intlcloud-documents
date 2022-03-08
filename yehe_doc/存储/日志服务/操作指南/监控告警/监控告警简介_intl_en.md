## Overview

CLS supports setting alarm policies for one or more log topics. An alarm policy periodically performs monitoring tasks and sends alarm notifications when the query and analysis results meet the trigger condition, so that you can find exceptions in time.

### Relevant concepts

| Name | Description |
|--------|------|
| Alarm policy | It is the management unit for monitoring alarms. An alarm policy contains various information such as monitoring object, monitoring period, trigger condition, alarm frequency, and notification template. |
| Monitoring object | A log topic can be used as the monitoring object, a query or analysis statement can be executed on the log topic, and then the query or analysis result can be checked. |
| Trigger condition | The query and analysis result is checked, and if the trigger condition expression is true, an alarm will be triggered. |
| Monitoring period | It is the policy execution period. A fixed period (such as every 5 minutes) and a fixed time (such as 12:00 every day) are supported. |
| Alarm frequency | It is the alarm frequency after the trigger condition is met, which helps avoid frequent alarm notifications. |
| Notification group | Supported notification channels include SMS, WeChat, phone calls, email, and webhook. |


### Flowchart

![image-20201230144652106](https://qcloudimg.tencent-cloud.cn/raw/9e338c05e4c15c75759a0dd04adf297a.png)

