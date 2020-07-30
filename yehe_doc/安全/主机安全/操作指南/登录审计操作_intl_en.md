CWP collects RDP and SSH login logs on the host and features [login audit](https://console.cloud.tencent.com/cwp/manage/loginLog), which displays all login transactions on the host and marks suspicious login behaviors.
![](https://main.qcloudimg.com/raw/afa7af91421a7a0aebfbacaaebab86ac.png)
The included fields are described as follows:
- Server: the server currently logged in to.
- Source IP Address: IP address of the login source. Generally, it is an egress IP address of a network or a network proxy IP address.
- Source Location: the location where the source IP address locates.
- Login Username: the username used by the user who successfully logged in to the server.
- Login Time: the time at which login was successfully made (server's time with time zone information)
- Status:
 - Normal: CWP detects that the login request is from a common login location and marks it as a normal login.
 - Unusual login location: CWP detects that the login is performed at an unusual location. It may be caused by password leakage or an intended login by an admin at an unusual location.
- Operation:
 - Allowlist: if you think that a logged login is normal, you can click **Allowlist** to add it to the custom login allowlist and set it to normal login.
 - Delete: delete the log. A deleted log will not be displayed again.
