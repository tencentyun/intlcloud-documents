## Overview
Cloud Monitor provides a complete set of monitoring capabilities such as monitoring data collection, data computation and aggregation, visualized data display, alarm convergence, alarm distribution, alarm notification, etc.
The custom notification feature of Cloud Monitor now provides alarm channel as an independent application to help you implement alarm distribution and notification for your own businesses and self-built monitoring system in different monitoring and alarm scenarios. You can thus quickly build alarm notification push channels.

## Features
Custom notification provides the following features for business alarm scenarios:
- Alarm distribution: you can push alarm notifications of different modules and resources to the corresponding notification policies by configuring and managing such policies.
- Alarm subscription: you can configure recipient groups for notification policies to implement subscription to corresponding alarm notifications.
- Alarm channel: you can configure alarm channels for notification policies, so recipients in the alarm recipient group can receive notifications pushed via corresponding channels.
- Alarm history view and search: you can view previously pushed alarm notifications under a notification policy and search for alarm content by keywords.

## Scenarios
- Custom business alarm push: alarms can be pushed to corresponding recipients through specific alarm channels in a self-built monitoring system.
- Prompt delivery of important service information: notifications about specific service status and exceptions will be pushed to developers promptly, with no need to configure monitoring, log system integration, and alarm policies.


## Principle and call methods
Cloud Monitor custom notifications uses a **notification policy** with a globally unique ID as the hub for receiving and distributing alarm notifications. An alarm notification can be distributed to a notification policy by specifying its ID, and then the policy will send the notification to recipients based on the configured subscription and alarm channel.

Cloud Monitor custom notification supports two call methods to provide the alarm channel service.
- API: the API for sending custom notifications can be called to push an alarm notification to the corresponding notification policy by passing in the specified policy ID and alarm content. 
- Agent: on a CVM instance where Cloud Monitor [Agent](https://intl.cloud.tencent.com/document/product/248/6211) has been installed, you can directly use the provided command line tool **cagent_tools** to run relevant commands to specify the policy ID and content and send them when an alarm is triggered.


## Operation Guide
### Creating and managing notification policy
You can create, configure, edit, and delete a notification policy.
1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor).
2. On the left sidebar, click **Alarm Configuration** > **[Custom Notifications](https://console.cloud.tencent.com/monitor/message)** to enter the custom notification page.
3. (Optional) Click **Add Notification Policy**, enter the policy name, select the recipient group, check the corresponding alarm channel, and click **Complete** to complete policy creation.
4. (Optional) Click **Edit** in the "Operation" column of the specified notification policy, modify the policy name, recipient group, and alarm channel, and click **Complete** to complete policy modification.
5. (Optional) Click **Delete** in the "Operation" column of the specified notification policy and click **OK** in the pop-up box to delete the policy.

### Pushing alarm notification through call
You can call the relevant API or use the agent command line tool to send notifications to the custom notification service.
1. Enter the [Custom Notifications](https://console.cloud.tencent.com/monitor/message) page in Cloud Monitoring Console to get the ID of the specified policy for alarm distribution.
2. (Optional) **Method 1**: call the API for sending custom notifications to pass in the specified policy ID and alarm content to the corresponding notification policy. 
3. (Optional) **Method 2**: use the command line tool **cogent_tools** provided by Agent to run relevant commands to specify the policy ID and content and push the alarm notification to the corresponding notification policy.
>cagent_tools is applicable only to CVM instances created with system images in Tencent Cloud.

#### Example 1. Using cagent_tools on Linux
1. Install Agent on Linux. For more information on installation, please see [Installing Agent](/doc/product/248/6211).
2. Run the following command to view the tool's help information:
```
cagent_tools
```
The result is as shown below:
![](https://main.qcloudimg.com/raw/6e862979c582ccf10906b7928f3641e5.png)
3. Run the following command to specify the policy ID and alarm content to be pushed:
```
cagent_tools alarm '$alarm content' cm-xxxxxxxx (policy ID)
```
![](https://main.qcloudimg.com/raw/d74215af871b8ea404f16288688e2986.png)
>
>- Currently, only the UTF-8 encoding format is supported for alarm content in Chinese.
>- The maximum length of an alarm notification is 256 bytes, and the excessive part will be truncated.
>- If an alarm notification is sent successfully, "send alarm OK!" will be displayed on the command line, and the return code will be 0. If an alarm notification fails to be sent, the relevant error will be displayed on the command line, and the return code will not be 0. 
4. Below are use cases.
 - PHP sample:
```
$link = mysql_connect('192.168.0.2', 'mysql_user', 'mysql_password');
if (!$link) {
 //alarm content
  $alarmContent = " Connection failed ";
  $cmd = “cagent_tools alarm $alarmContent cm-xxxxxxxx(policyId)”; 
  system($cmd);
  die('Could not connect: ' . mysql_error());
}
```
 - Shell sample:
```
#!/bin/sh
PATH=/usr/local/sbin:/usr/sbin:/sbin:/usr/local/bin:/usr/bin:/bin:$PATH
CAGENT_CMD = /usr/bin/cagent_tools
cnt=$(ps -ef | grep mysqld | grep -v grep | wc -l)
if [ $cnt -eq 0 ] ; then
    # alarm content 
    cagent_tools alarm "the process mysqld died." cm-xxxxxxxx(policyId)
fi
```

#### Example 2. Using cagent_tools on Windows
1. Install Agent on Windows. For more information on installation, please see [Installing Agent](/doc/product/248/6211).
2. Run the following command on the command line to view the tool's help information:
```
cagent_tools
```
The result is as shown below:
![](https://main.qcloudimg.com/raw/9bfa9ae0ca7c8d73b257eefa83616579.png)
3. Run the following command to specify the policy ID and alarm content to be pushed:
```
cagent_tools alarm "$alarm content" cm-xxxxxxxx (policy ID)
```
![](https://main.qcloudimg.com/raw/e866da3600b965c9c5fd0cadcd834365.png)
4. Below are use cases.
 - DOS sample:
```
@echo off
set service_name=StargateSvc
sc query %service_name% > nul
if not %errorlevel% == 0 (
    cagent_tools alarm "service %service_name% didn't exist" cm-xxxxxxxx(policyId)
)
```

>
>- Currently, both UTF-8 and GBK encoding formats are supported for alarm content in Chinese.
>- The maximum length of an alarm notification is 256 bytes, and the excessive part will be truncated.
>- If an alarm notification is sent successfully, "send alarm OK!" will be displayed on the command line, and the return code will be 0. If an alarm notification fails to be sent, the relevant error will be displayed on the command line, and the return code will not be 0.


### Viewing and searching for alarm history
1. Log in to the [Cloud Monitoring Console](https://console.cloud.tencent.com/monitor/).
2. On the left sidebar, click **Alarm Configuration** > **Custom Notifications** to enter the custom notification page.
3. Click on the number of alarms triggered in the last 24 hours under the specified policy as shown below:
![](https://main.qcloudimg.com/raw/2c6c9160b23b9f8576100e360b3653c9.png)
4. A floating window will pop up to display the content, time, and call method of all alarm notifications sent by the policy.
![](https://main.qcloudimg.com/raw/7282bdd952bab77f8387fb09c8fcf168.png)
5. (Optional) You can enter alarm notification content keywords or the private IP of the CVM that calls cagent_tools in the search box on the top-right corner to search for corresponding alarms.




