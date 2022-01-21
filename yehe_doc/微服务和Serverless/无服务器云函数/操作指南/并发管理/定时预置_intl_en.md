
## Overview

Scheduled provisioned concurrency is an elastic policy for [provisioned concurrency](https://intl.cloud.tencent.com/document/product/583/37704). You can reasonably configure provisioned concurrency based on the business conditions and upgrade/downgrade it at specified times to improve the utilization of provisioned concurrent instances and reduce the fees incurred by idle resources. If the number of concurrent instances actually required by a function exceeds that configured in scheduled provisioned concurrency, auto scaling will be performed as needed. This feature supports the following task types: one time, daily, Monday to Friday, Saturday and Sunday, and custom.

## Use Cases
- Functions with regularly fluctuating traffic, such as data processing functions.
- Functions whose business traffic peaks can be predicted, such as functions for events or other scheduled businesses.

## Features and Limits

The configured value in scheduled provisioned concurrency is the target number of concurrent instances during task execution; for example, if you need to configure four scheduled tasks for your business, i.e., starting 30 concurrent instances at 6:00, 80 at 10:00, 40 at 18:00, and 0 at 24:00, the final provisioned concurrency fluctuation will be as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/9f2a93405dc5ef2349d869cb49b77196.png)

#### Notes
- A cron expression for scheduled provisioned concurrency has seven required fields separated with spaces. For more information, see [Timer Trigger Description](https://intl.cloud.tencent.com/document/product/583/9708).
- There is a limit to the number of scheduled provisioned concurrency tasks under one user account on one function version. For more information, see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). To increase the maximum number of scheduled tasks (i.e., quota limit), you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.
- SCF will adjust the speed of starting provisioned concurrency based on your business, which is 100 concurrent instances per minute by default. You should reasonably configure the start time of scheduled provisioned concurrency. For more information, see [Concurrency Overview](https://intl.cloud.tencent.com/document/product/583/37040).
- If two scheduled provisioned concurrency tasks are scheduled for the same time, the new one will overwrite the old one.


## Example
To start a scheduled provisioned concurrency task at 12:00 on November 13, 2021 to sustain your business traffic peak and end the task at 16:00 on the same day, perform the following operations:

### Starting scheduled task
To start a provisioned concurrency task as scheduled, you need to add a scheduled task. Select the start time and configure the target number of concurrent instances as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/6ec9cc2c88a7101129444a0bce6c83db.png)


### Ending scheduled task
To end a provisioned concurrency task as scheduled, you need to **add another scheduled provisioned concurrency task**. Select the desired end time of the previous task as the start time of the new task and configure the target number of concurrent instances to 0 as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ce93d71695948a8c0bba632b8ad16eae.png)
