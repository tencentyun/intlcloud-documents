This document describes how to use the Anti-Unusual Login feature.

## Overview
When unusual login attempts such as login from an unusual location, login with an unusual user name, login at an unusual time, login from an unusual IP are detected, CWPP will mark the login records as "Suspicious" or "High-risk" based on intelligent algorithms, and send alerts to you in real time.

## Important Notes
- The Anti-Unusual Login feature is available for the servers on which the CWPP Agent is installed and is online.
- The CWPP console only retains the unusual login events for the last 6 months, and the event data generated 6 months ago is not displayed.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Unusual Login** on the left sidebar. The fields and operations related to the feature are described as follows.

### Event List
In the **Event List**, you can view and handle unusual login risks detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/2e913ad2862ac39f18b5611e1c0ed6f9.png)
**Field description:**
- Server IP/Name: The target server of the unusual login attempt.
- Source IP: Source IP of the unusual login attempt, which generally is an egress IP of a company's network or a proxy IP.
- Source Location: The location where the login source IP is located.
- Login Username: The username used by the user who successfully logged in to the server.
- Login Time: The time when the user successfully logged in to the server (The time shown on the server).
- Threat Level: Suspicious/High.
- Status
 - Unusual Login: A login attempt from an unusual location, with an unusual user name, at an unusual time, or from an unusual IP.
 - Allowlisted: The login source has been added to the allowlist (login source IP, login username, login time, and usual login location).
 - Handled: The event has been handled manually and marked as Handled.
 - Ignored: This alert event has been ignored.
- **Operation**
 - **Actions**
   - **Mark as processed**: If the event has been handled manually, mark the event as "Handled".
   - Add to Allowlist: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
   - Ignore: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
   - Delete Record: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Allowlist Management
In **Allowlist Management**, you can add/delete items to/from the allowlist of unusual logins, or check and edit the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/0ebc346662503b301c1b2fce64c80613.png)
Field description:
- Server IP/Name: The server on which the allowlist takes effect.
- Source IP: The source IP added to the allowlist.
- Usual Login Location: The login location added to the allowlist.
- Login Username: The username added to the allowlist.
- Login Time: The login time added to the allowlist.
- **Creation time**: The time when the allowlist was created.
- **Update time**: The time when the allowlist was last updated.
- **Operation**
  - Edit: Re-edit the login source IP, login username, login time, usual login location, covered servers, etc.
  - Delete: Delete items from the allowlist.
