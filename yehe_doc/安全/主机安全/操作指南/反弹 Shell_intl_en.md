This document describes how to use the reverse shell detection feature.

## Overview
Reverse shell detection identifies and records reverse shell connections from.

## Limits
- You have at least one server bound to a CWPP Pro/Ultimate license.
- Alerts are only triggered for reverse shell connected to a server is detected in a public network.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Reverse Shell** on the left side bar. The fields and operations related to the feature are described as follows.

### Event List
In the **Event list**, you can view and handle the reverse shell risks detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/61d1d26ebccfb4253abda462cd737eeb.png)
Field description:
- **Server IP/Name**: The server where a reverse shell was detected.
- **Connection Process**: The process for the reverse connection.
- **Command**: The command executed for the reverse shell.
- **Parent Process**: The parent process for the connection process.
- **Target Server**: The target server of the reverse shell.
- **Target Port**: The target port of the reverse shell.
- **Detected Time**: The time when the reverse shell action was first detected.
- **Check Method**: Behavior analysis, command feature detection.
- **Status**: **Pending processed**, **Added to allowlist**, **Processed** and **Ignored**
- **Operation**
 - **Details**: You can view more information about reverse shells, such as process information, command lines, and risk description.
 - **Actions**
   - **Mark as processed**: Please handle the risk manually by referring to **Fix Suggestions** in the event details, and then mark the event as "Handled".
   - **Add to Allowlist**: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
   - **Ignore**: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
   - **Delete Log**: Once deleted, the event record will no longer be displayed on the console and cannot be recovered. 

### Allowlist Management
In **Allowlist Management**, you can add/delete items to/from the allowlist, or edit and check the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/d4dcae733b3cd048e36d945b2bc81eca.png)
Field description:
- **Servers**: The range of servers on which the allowlist takes effect.
- **Connection Process**: The connection process in the allowlist.
- **Target Server**: The target server in the allowlist.
- **Target Port**: The target port in the allowlist.
- **Creation time**: The time when the allowlist was created.
- **Update time**: The time when the allowlist was last updated.
- **Operation**
  - **Edit**: Edit the conditions of reverse shells in the allowlist.
  - **Delete**: Delete items from the allowlist.
