
This document introduces how to troubleshoot and resolve situations in which no alarms can be received.

## Reasons for this Problem

| Reason | Solution |
| ------------------------------ | --------------------------------------------------------- |
| The alarm policy has not been enabled | See [Step 1](#step1) to enable the alarm policy |
| **The alarm notification channel has not been configured or verified** | See [Step 2](#step2) to troubleshoot and enable or verify the alarm notification channel |
| No user has been added to the receiving group | See [Step 3](#step3) to troubleshoot and add users to the receiving group |
| The alarm trigger conditions have not been met | See [Step 4](#step4) to troubleshoot and check whether the alarm trigger conditions have been met |

## Troubleshooting

<span id="step1"></span>

### Step 1: Check whether the alarm policy is enabled

1. Access the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page in the Cloud Monitor console.
2. Check whether the alarm policy is enabled.
	- The alarm enable/disable button for policy 1 is gray in the figure below, indicating that the alarm policy has not been enabled yet. Click the gray button and then click **OK** to enable the policy.
	- The alarm enable/disable button for policy 2 is blue in the figure below, indicating that the alarm policy is enabled. Proceed to the steps below to continue troubleshooting.
![](https://main.qcloudimg.com/raw/dc74145f7bd40e64d22715f9b00bde9c.png)

<span id="step2"></span>

### Step 2: Check whether the alarm channel has been configured/verified

1. Log in to the [CAM console](https://console.cloud.tencent.com/cam).
2. Click the corresponding user name in the user list to go to the user details page.
	- The alarm channel has not been configured: if the case shown in the figure below occurs, the alarm channel has not been configured. In this case, click **![](https://main.qcloudimg.com/raw/e6ecaf9389ae90463b6acefca2f30cb7.png)** to configure a channel. After completing the configuration, verify the channel by referring to **The alarm channel has not been verified** below.
![](https://main.qcloudimg.com/raw/093bf3503c1760e7263c7c18c9cb3ab4.png)
	- The alarm channel has not been verified: if the case shown in the figure below occurs, the alarm channel has not been verified. In this case, click the verification button.
	![](https://main.qcloudimg.com/raw/75b6b6a123c3530bc8f306dc6160094b.png)
		 After the verification message or email is sent, go to the corresponding channel to complete the verification.
	- SMS verification: check the SMS inbox on your mobile phone and click the link in the received message to complete the verification.
	- Email verification: log in to your inbox and click the link in the received email to complete the verification.



 <span id="step3"></span>
### Step 3: Check whether you have added users to the alarm receiving group

1. Go to the [Alarm Policy](https://console.cloud.tencent.com/monitor/policylist) page in the Cloud Monitor console.
2. Find the target alarm policy and click its name to go to the alarm policy management page.
3. Check whether the alarm recipients contain the user who has not received alarm notifications. If the alarm receiving group is "not configured" or does not contain the user, see [Creating Alarm Recipient Groups](https://intl.cloud.tencent.com/zh/document/product/248/38908) to add the user to the alarm receiving group.
![](https://main.qcloudimg.com/raw/00155e489f2b870c94341cec6ca67839.png)


<span id="step4"></span>

### Step 4: Check whether the alarm trigger conditions have been met

#### Checking whether the metric alarm trigger conditions have been met

For example, if the metric is `CPU utilization`, the comparison operator is `>`, the threshold is `80%`, the measurement period is `5 minutes`, and the duration is `2 periods`, it means that the CPU utilization information is collected every 5 minutes. If the CPU utilization of a CVM is measured as above 80% **for 3 consecutive periods**, an alarm will be triggered. Likewise, if the duration is set to N, an alarm will be generated if the metric monitoring data reaches the threshold for the N+1 periods.

You can log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor), select the corresponding Tencent Cloud service, and click **![img](https://main.qcloudimg.com/raw/913709c7fa409d62518bf58e23c95446.png)** to view the metric monitoring data, and use the time filter to check whether the metric monitoring data has met the alarm trigger conditions. If no, no alarm notification will be sent.

View the CPU utilization of the CVM, as shown in the figure below: 
![img](https://main.qcloudimg.com/raw/e9d82c8be76f1c84bc8921a63f01813b.png)

#### Checking whether the event alarm trigger conditions have been met

1. Go to the [Product Events](https://console.cloud.tencent.com/monitor/event/product) page in the Cloud Monitor console.
2. Check for event alarm records. If no records are found, the event alarm trigger conditions are not met, and therefore no alarm notifications are sent.
 ![img](https://main.qcloudimg.com/raw/271f446c313ae08f29bb9491edd8f7fc.png)

If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category). 
