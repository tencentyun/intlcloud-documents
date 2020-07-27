CLS uses Cloud Monitor (CM) alarms to guarantee the business reliability and availability for users.

This topic describes how to help you get promptly informed of the exceptions on your Loglistener by configuring CLS Loglistener heartbeat alarm policies.



## Step 1. Log in to CM Console


<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/monitor/overview" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to open the CM console</a></div>




## Step 2. Add an Alarm Policy

1. In the left sidebar, choose **Alarm Configuration** > **Alarm Policy** to open the alarm policy page.
2. Click **Add** to enter the Create Policy page where you should configure information including policy type, server group, condition, and recipient.
 - Policy Name: enter a policy name.
 - Remarks: add remarks to the policy.
 - Policy Type: select the monitoring metric.
 - Project: select a project as needed.
 - Trigger Condition
 As CLS reports the number of exceptional/normal heartbeats of server groups to CM, you should configure appropriate alarm trigger conditions based on the server group list you chose to monitor.
		- Example 1: configure the alarm policy so that an alarm is triggered every 5 minutes when the number of exceptional heartbeats is > =1 for 2 consecutive statistical periods (each period as 1 min).
	
		- Example 2: configure the alarm policy so that an alarm is triggered every 5 minutes when the number of normal heartbeats is < 100 for 2 consecutive statistical periods (each period as 1 min).
	
 - Alarm Channel
    Use the alarm channel to specify alarm recipients (or recipient group). Only recipients who have their mobile phone or email address verified can receive alarms.
3. Click **Complete**.




## Step 3. Receive Alarms

Tencent Cloud monitors your activity based on the alarm policy you set, and sends alarms through the alarm channel when the trigger condition is met.



## Step 4. View Alarm List

1. Log in to the [Cloud Monitor console](https://console.cloud.tencent.com/monitor/overview).
2. Click **Alarm List** in the left sidebar to view alarm records, including when an alarm is triggered and how long it lasts.
