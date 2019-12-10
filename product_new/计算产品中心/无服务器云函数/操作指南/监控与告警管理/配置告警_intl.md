
## Operation Scenario
You can configure alarm policies for SCF through [Cloud Monitor](https://console.cloud.tencent.com/monitor/myalarm) to monitor the execution status of functions. Currently, the following monitoring metrics can be configured for SCF:
- Execution duration
- Number of calls
- Number of errors
In addition, you can select user groups that will receive alarms through email, SMS or WeChat.

## Steps

### Log in to the console

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/).
2. Select "Cloud Products > Administrative Tools > Cloud Monitor" to enter the Cloud Monitor page.

### Configure an alarm policy

1. In the navigation pane on the left, select "Alarm Management > Alarm configuration > Alarm policy" and click "Add" to add a new alarm. See the figure below:
![](https://main.qcloudimg.com/raw/e8dab83d39ddcbff59d1fbb026b633da.png)
2. On the "Create a policy" page, enter the policy name, select the policy type, and set the alarmed objects based on actual needs. See the figure below:
	- **Policy name**: Custom.
	- **Policy type**: Select "SCF".
	- **Alarmed object**: Set based on actual needs. If you select "Select certain objects", the region will be set to Guangzhou by default. In different regions, you can view the corresponding functions. Please select the functions to which to apply the alarm policy.
![](https://main.qcloudimg.com/raw/c9c878ca72b247e98c0e2e2ca447b88d.png)
3. Set the "Triggering condition" and "Alarming channel" based on actual needs, as shown below:
![](https://main.qcloudimg.com/raw/fcf6fd3b4002c03d15aa51278a049b89.png)
4. Click **Finish** and you can view the configured policy in "Alarm policies". Based on actual needs, you can start or stop the policy at any time.

>For more information about detailed alarm policy configuration, see [Cloud Monitor > Alarm Policy](https://intl.cloud.tencent.com/document/product/248/6215).




