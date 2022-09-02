This document describes how to use the Anti-Password Cracking feature.

## Overview
CWPP's Anti-Password Cracking feature monitors brute force cracking of passwords for servers in real time and blocks the attacks automatically based on Tencent Cloud's network security defense and server intrusion detection capabilities.

## Limits
- Anti-Password Cracking is available for the servers on which the CWPP Agent is installed and online (except for automatic blocking).
- Global blocking only takes effect on the servers bound to a (CWPP Pro/Ultimate) license.
- The CWPP console only retains the password cracking events for the last 6 months, and the event data generated 6 months ago is not displayed.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Anti-Password Cracking** on the left sidebar. The fields and operations related to the feature are described as follows.

### Event List
In the **Event List**, you can view and handle the password cracking risks detected by CWPP.
![](https://qcloudimg.tencent-cloud.cn/raw/1ef1bf6721a02fc432a8dcb3de2391b6.png)
You can enable **Auto Blocking**, which has two modes.

| Blocking Mode | Description |
|---------|---------|
| Standard | Intelligently identifies brute-force cracking based on the brute force rules you set, and automatically blocks the source IP of brute-force cracking not in the allowlist. |
| Enhanced | Automatically blocks the source IP not in the allowlist based on the "Allowlist - Allowlist only" policy (only ports 22 and 3389 are supported). Enhanced blocking covers standard blocking. |

Field description:
- Server IP/Name: The server where password cracking was detected.
- Source IP: Source IP address of the attack.
- Origin: The region where the source IP of the attack is located.
- Protocol: The protocol used by the attacker, including SSH/RDP, FTP, MsSQL, MySQL, SMB, MongoDB, Kafka, and RabbitMQ.
- **Login username**: The username used by the attacker for login.
- **Port**: The port used by the attacker for login.
- **First attack**: The time when the password cracking behavior was first detected by CWPP.
- **Latest attack**: The time when the event last occurred.
- **Number of attempts**: The number of password cracking attempts made by the attacker IP.
- **Cracking Status**: Whether password cracking on the current server is successful.
- Blocking Status: Whether the auto blocking of the attack is successful.
- Event Status: Pending, Allowlisted, Handled, or Ignored
 - **Operation**
   - **Mark as processed**: If the event has been handled manually, mark the event as "Handled".
   - **Add to Allowlist**: Once an event is added to the allowlist, no alert will be sent if the same event occurs again.  
   - Ignore: Only ignore this alert event. If the same event occurs again, an alert will be sent again.
   - Delete Record: Once deleted, the event record will no longer be displayed on the console and cannot be recovered.  

### Allowlist Management
In **Allowlist management**, you can add/delete items to/from the allowlist of unusual logins, or check and edit the allowlist.
![](https://qcloudimg.tencent-cloud.cn/raw/62bf5660bd72ab199c03c5fa8d97dd45.png)
Field description:
- Server IP/Name: The server on which the allowlist takes effect.
- Source IP: The source IP added to the allowlist.
- Usual Login Location: The login location added to the allowlist.
- Login Username: The username added to the allowlist.
- Login Time: The login time added to the allowlist.
- **Creation time**: The time when the allowlist was created.
- **Update time**: The time when the allowlist was last updated.
- **Operation**
  - Edit: Edit the source IP, covered servers, and remarks.
  - Delete: Delete items from the allowlist.
