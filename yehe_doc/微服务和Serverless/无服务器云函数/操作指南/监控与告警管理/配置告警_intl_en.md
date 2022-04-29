

## Overview
You can configure alarm policies for SCF through [CM](https://console.cloud.tencent.com/monitor/myalarm) to monitor the execution status of functions. Currently, the following monitoring metrics are supported for this:
- Execution duration
- Number of invocations
- Number of errors

For the full list of supported metrics, see [Descriptions of monitoring metrics](https://intl.cloud.tencent.com/document/product/583/32739). In addition, you can select user groups that will receive alarms through email, SMS, or WeChat.

## Directions

### Logging in to Console

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Select "Cloud Products > Monitoring and Ops > Cloud Monitor" to enter the Cloud Monitor page.

### Configuring alarm policy

1. On the left sidebar, select "Alarm Management > Alarm Configuration > Alarm Policy" and click **Create** to add a new alarm as shown below:
![](https://main.qcloudimg.com/raw/e14e7a494774e736d53d0ab7627e3b19.png)
2. On the "Create a Policy" page, enter the policy name, select the policy type, and set the alarm objects based on your needs, as shown below:
	- **Policy name**: Custom.
	- **Policy type**: Select "SCF".
	- **Alarm Object**: Set based on your needs. If you select "Select certain objects", the region will be set to Guangzhou by default. In different regions, you can view the corresponding functions. Please select the function to which you will apply the alarm policy.
	![](https://main.qcloudimg.com/raw/c9c878ca72b247e98c0e2e2ca447b88d.png)
3. Set "Trigger" and "Alarming Channel" based on your needs, as shown below:
![](https://main.qcloudimg.com/raw/fcf6fd3b4002c03d15aa51278a049b89.png)
4. Click **Complete**, and you can see the configured policy in **Alarm Policy** and choose to enable/disable it at any time.

>! For more information on detailed alarm policy configuration, see [Cloud Monitor > Alarm Policy](https://intl.cloud.tencent.com/zh/document/product/248).



