## Prerequisites
The new version of the security overview feature is currently in beta test and can be used only by accounts randomly chosen by the beta test system.
## Overview
As the server security information display and processing center, the [Security Overview](https://console.cloud.tencent.com/cwp) page of CWP can display the server health check score, protection status, risks to be processed, risk trend, and overall server security status in real time. In addition, it provides CWP help documentation and suggestions on CWP upgrade service, helping you defend against intrusions and attack threats to protect your workload security.
## Feature Overview
Log in to the [CWP Console](https://console.cloud.tencent.com/cwp) and click **Security Overview** on the left sidebar to enter the security overview page which provides security overview information and relevant operations. The features of its modules are as described below:
### Server security health check
 The server security health check feature can score your servers through security health checks and provide the numbers of servers and security risks. Click **Process Now** to enter the risk processing page where you can directly process detected intrusions and network defense risks and manage vulnerabilities.
![](https://main.qcloudimg.com/raw/a9c17f0741d5467c80f7b3221451500d.png)
 The server security status has the following three levels:

| Risk Level | Health Check Score | Font Color | Description |
|---------|---------|---------|---|
| Low	|90–100|	Green	| Your asset security status is excellent. Please maintain the status and perform routine inspection. |
| Medium|	60–89|	Orange| Your asset has many security risks. You are recommended to solve them promptly. |
| High|	20–59|	Red	| Your asset has severe security risks. Please solve them as soon as possible. |

> The lowest health check score for server security is 20.

The score penalties are calculated by security event category. The security event levels and penalty rules are as follows:

| Level | Security Event (Counted by Event Quantity) | Penalty Per Event | Maximum Total Penalty |
|---------|---------|---------|-|
|Severe	| Trojan, virus, and successful intrusion. |	-50|	-80|
|High	| High-risk vulnerability, high-risk baseline risk, and unusual login location.	|-10|	-60|
|Medium	| Medium-risk vulnerability and baseline risk. |-3	|-30|
|Low	| Low-risk vulnerability and baseline risk. 	|-2	|-20|
|Other	| CWP Basic (unprotected status). |-1	|-10|

#### Protection status
The protection status section displays the total number of currently online severs, number of CWP Pro-protected online servers, and number of CWP Basic-protected servers as well as virus library date, vulnerability library date, and security engine protection information.
- In the detection module of CWP Basic, click **Upgrade to Pro** to enter the CWP upgrade page. You can make a payment to upgrade from CWP Basic to CWP Pro for those servers for more powerful risk and threat defense capabilities.
- Security engine protection will display 6 engine icons, which represent engines of cloud-based antivirus, AI, virtual machine detection, exception analysis, threat intelligence, and attack protection, respectively. If you have not activated CWP Pro, these icons are grayed out, and after you activate CWP Pro, they will be available.

### Pending risks
The pending risks section displays the number of server risks to be processed and the number of affected servers. You can click a risk event or its occurrence quantity to enter the corresponding risk processing page.
The data of pending risks is synced in real time and can be divided into the following 4 categories:

- **Intrusions**: this module provides detection and auditing for 7 types of intrusions, namely, trojans, unauthorized logins, brute force attacks, malicious requests, reverse shells, local privilege escalation, and high-risk commands. It also displays the numbers of risks and affected servers.
- **Vulnerabilities**: this module detects vulnerabilities in web applications and system components and display the numbers of vulnerabilities and affected servers.
- **Security baseline**: this module only displays the numbers of baseline risks and affected servers.
- **Network attacks**: this module displays the numbers of attacks and affected servers.

### Risk trend
The risk trend section displays a line chart of the trend in security risks and threats in the last 7, 14, or 30 days and allows you to view the trend by time period. You can hover your mouse on the trend chart to view the numbers of risks and threats such as trojans, viruses, brute force attacks, suspicious logins, vulnerabilities, and baseline risks on the corresponding date.
### Real-Time updates
The real-time updates section displays real-time server risks and threat events in reverse chronological order.
- Click **Server IP** to enter the corresponding tab on the "Server Details" page.
- Hover your mouse on an update and click **Process Now** on the right to enter the corresponding event processing page.

