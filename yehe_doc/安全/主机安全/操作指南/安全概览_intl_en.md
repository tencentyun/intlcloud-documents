This document describes how to use Security Dashboard.

## Overview
As the homepage of Cloud Workload Protection Platform (CWPP), Security Dashboard displays security score, pending risks, security protection status, risk trend, and new security events; pushes security notices to keep you updated with the latest threat intelligence of CWPP; provides documentation and suggestions to help you defend against intrusion and attacks and ensure your server security.


## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Security Dashboard** on the left sidebar. The fields and operations related to the feature are described as follows.

### Security Status
The **Security Status** section presents the security score and risk information, and provides quick access to risk handling pages.
![](https://qcloudimg.tencent-cloud.cn/raw/4c76d82895341c04addf71256f1cb37a.png)
- **Security score**: The score is calculated based on the number of security events and their threat level. For more information about the scoring rules, see [Security Score Overview](https://intl.cloud.tencent.com/document/product/296/49373).
- **Risk information**: It contains three categories of information: detected intrusions, vulnerability risks, and baseline risks, and shows the number of pending risks and the number of affected servers.
 - Intrusion Detection: Malicious File Scan, Unusual Login, Password Cracking, Malicious Requests, Reverse Shell, Local Privilege Escalation, and High-Risk Commands.
 - Vulnerability Risks: Linux software vulnerabilities, Windows system vulnerabilities, Web-CMS vulnerabilities, and application vulnerabilities in Vulnerability Management.
 - Baseline Risks: Only risks in Baseline Management.

### Security Intelligence
The **Security intelligence** section shows the feature updates, news about honors and awards, urgent notifications, and version release information.
![](https://qcloudimg.tencent-cloud.cn/raw/87208bf8d2cec4e4f7cd57a59b3fb28d.png)
Click the intelligence title to check details. Click **More** to view all the security intelligence.


## Security Protection
The **Security Protection** section displays the complete anti-intrusion solution (prevention-defense-detection-response) of CWPP, and the security protection items required for each process.
![](https://qcloudimg.tencent-cloud.cn/raw/feb95d665d94d19c591209257a3c05aa.png)
If all the protection items are enabled, you can get a clear picture of the security of your servers and get quick access to the risk handling pages.


### Protection Details
The **Protection Details** section shows the usage data of various CWPP services.
![](https://qcloudimg.tencent-cloud.cn/raw/2c4779ec905e77cbe8506c7f685635eb.png)
- Days of Protection: The total time the CWPP Agent has been installed on the server.
- **Total servers**: The total number of Tencent Cloud servers (CVMs, Lighthouse servers, CPM 1.0, ECMs) and non-Tencent Cloud servers.
- **Protected servers**: The total number of the servers protected by CWPP Pro/Ultimate.
- **Engines**: If you have purchased the CWPP Pro/Ultimate licenses, six protection engines are automatically activated: Cloud Security Engine, BinaryAI Engine, TAV Engine, Unusual Behavior Engine, Threat Intelligence Engine, and Anti-Attack Engine.
- **Virus database update time**: The virus library is automatically updated at 0:00 every day.
- **Server update time**: Click **Update now** in the upper right corner to manually update the server list.
- Vulnerability Library Update Time: From time to time.

### Risk Trend
On the **Risk Trend** section, the statistics of various risks are displayed in a line graph, which visually presents the risk trend of servers.
![](https://qcloudimg.tencent-cloud.cn/raw/8294b70a6f45b2e1d19c933b91446844.png)
You can view the risk statistics for the last 7 days, the last 14 days, the last 30 days, or a custom date range. Click **Download** to export the risk statistics for the selected date range.

<dx-alert infotype="explain" title="">
The number of risks is the number of new pending events on the current day and is updated every hour.
</dx-alert>

### Real-time monitoring
The **Real-time monitoring** section displays the newly discovered security events in real time.
![](https://qcloudimg.tencent-cloud.cn/raw/8555ee6f4dd0fe12649cb733af911f65.png)
Click **Server IP** or **View Details** to go to the risk item on the server details page.
