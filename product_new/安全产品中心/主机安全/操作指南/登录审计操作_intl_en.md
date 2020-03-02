CWP collects RDP and SSH login logs on the server and features login audit, which displays all login logs on the server and marks suspicious login behaviors.

## Configuring Common Login Locations

Setting up common login locations can effectively help detect login behaviors at unusual locations. On the **Overview** tab in the CWP Console, find the target server in the server list and click the server's IP address. On the pop-up page, find **Common Login Locations** in the login information and click to add a location.

## Login Audit Log Overview

In the CWP Console, click **Intrusion Detection** > **Login Auditing** on the left sidebar to view the login audit logs of the currently protected server, as shown below.

![Login mark](https://main.qcloudimg.com/raw/afa7af91421a7a0aebfbacaaebab86ac.png)
**Note:**

- Server: the server currently logged in to.

- Source IP Address: IP address of the login source. Generally, it is an egress IP address of a network or a network proxy IP address.

- Source Location: the location where the source IP address locates.

- Login Username: the username used by the user who successfully logged in to the server.

- Login Time: the time at which login was successfully made (server's time with time zone information) 

- Status:
   - Normal: CWP detects that the login request is from a common login location and marks it as a normal login.
   - Unusual login location: CWP detects that the login request is from an unusual login location. It may be caused by password leakage or an intended login from an unusual location.

- Operation:
   - False Positive: if the login is intended, you can click this button to set it to a normal login.
   - Delete: delete the log. A deleted log will not be displayed again.
