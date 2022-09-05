This document describes how to use the Anti-Local Privilege Escalation feature.

## Overview
Local privilege escalation happens when a user with a low privilege or an unprivileged user has access to a compromised machine and gains administrator or SYSTEM level privileges to fully control the machine. The Anti-Local Privilege Escalation feature monitors privilege escalation events on your servers in real time, and allows you to view the event details, handle the events, and create allowlist of permitted privilege escalation events.

## Limits
The Anti-Local Privilege Escalation feature is available only if you have at least one server bound to a (CWPP Pro/Ultimate) license.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Local Privilege Escalation** on the left sidebar. The fields and operations related to the feature are described as follows.

### Event List
In the **Event List**, you can view and handle the local privilege escalation risks detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/5f20bea22e847b0d145198f1df3396f1.png)
Field description:
- Server IP/Name: The server where local privilege escalation was detected.
- Privilege Elevation User: The user with a low privilege who gains control of the server by obtaining a high privilege.
- Parent Process: The parent process for privilege escalation.
- Parent Process User: The user who can execute the parent process.
- Detected At: The time when the local privilege escalation was detected.
- Status: Pending, Allowlisted, Handled, or Ignored
- **Operation**
  - **Details**: You can view more information about high-risk commands, such as process information, command lines, and risk description.
  - **Actions**
    - **Mark as processed**: Please handle the risk manually by referring to "Solutions" in the event details, and then mark the event as "Handled".
    - Add to Allowlist: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
    - Ignore: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
    - Delete Record: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Allowlist Management
In **Allowlist Management**, you can add/delete items to/from the allowlist, or edit and check the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/eab5b624be6b37a1fd389d36a1203580.png)
Field description:
- Servers: The range of servers on which the allowlist takes effect.
- Privilege Escalation Process: The process for privilege escalation.
- With S Permission: Whether the user executing a file has the ownership of the file (whether the user is the temporary owner of the file).
- **Creation time**: The time when the allowlist was created.
- **Update time**: The time when the allowlist was last updated.
- **Operation**
   - Edit: Edit the conditions of privilege escalation.
   - Delete: Delete items from the allowlist.
