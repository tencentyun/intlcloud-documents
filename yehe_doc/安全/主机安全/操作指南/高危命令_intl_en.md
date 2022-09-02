This document describes how to use the High-Risk Command Detection feature.

## Overview
CWPP monitors the commands in the system in real time, and supports the configuration of rules to classify the commands in terms of risk level. If any high-risk command is detected, an alert will be sent to you in real time.

## Limits
You have at least one server bound with a CWPP Pro/Ultimate license.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **High-risk commands** on the left side bar. The fields and operations related to the feature are described as follows:

### Event List
In the **Event list**, you can view and handle the high-risk command risks detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/23f4ce136d8823439121319972984a8a.png)
Field description:
- **Server IP/Mame**: The server where a high-risk command was detected.
- **Rule type**: **Preset rules** and **Custom rules**
- **Rule name**: The name of the hit preset or custom rule.
- **Severity level**: **High**, **Medium**, and **Low**.
- **Command**: The content of the executed command.
- **Login user**: The user logged in to the server when the command was executed.
- **PID**: The unique ID of the process file.
- **Process**: The running state of the program after execution.
- **Data source**: Bash log and real-time monitoring.
- **Occurrence time**: The time when the high-risk command occurred.
- **Processed time**: The time when the high-risk command was handled on the CWPP console.
- **Status**: **Pending processed**, **Added to allowlist**, **Processed** and **Ignored**
- **Operation**
 - **Details**: You can view more information about high-risk commands, such as process information, command lines, and risk description.
 - **Actions**
   - **Mark as processed**: Please handle the risk manually by referring to **Fix Suggestion** in the event details, and then mark the event as **Processed**.
   - **Add to Allowlist**: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
   - **Ignore**: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
   - **Delete Log**: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Configuring Custom Rules
In **Custom Rules**, you can add/delete rules to/from the allowlist/blocklist of high-risk commands, and check and edit the allowlist/blocklist.
![](https://qcloudimg.tencent-cloud.cn/raw/f92d6f572365c7ce2d7fd6c1e2050329.png)
Field description:
- **Rule name**: The name of the rule for the blocklist/allowlist of high-risk commands.
- **Blocklist/Allowlist**: When a command matches the regular expression of the blocklist, an alert for the security event is generated. When a command matches the regular expression of the allowlist, no alert is generated to avoid false positives.
- **Regular expression**: A regular expression that determines whether a command matches the blocklist/allowlist.
- **Severity level**: High, Medium, Low, None.
- **Affected servers**: The range of servers on which a rule takes effect.
- **Update time**: The time when the rule was last updated.
- **Enabled/disabled**: Enable/Disable.
- **Operation**
  - **Edit**: Edit the range of servers on which a rule takes effect.
  - **Delete**: Delete rules.

