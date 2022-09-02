This document describes how to use Server List.

## Overview
Server List presents the information of all servers on which CWPP is installed to give you a full picture of the security of your assets.

## Important Notes
- Server List is available to all Tencent Cloud users.
- Servers running in a hybrid cloud environment are supported.
 - Tencent Cloud: CVMs, Lighthouse servers, and ECMs.
 - Non-Tencent Cloud: Third-party cloud servers and IDC servers.

## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Server List** on the left sidebar. The fields and operations related to the feature are described as follows.

### Server Status
The **Host Status** section shows the total number of servers, the number of protected servers, the number of servers at risk, the number of unprotected servers, and the number of servers with licenses that are about to expire.
![](https://qcloudimg.tencent-cloud.cn/raw/c0aa4c18e30f2a4f1aebb70583b119ed.png)
Click **Connect to Multiple Servers** or **Install CWPP Agent** to open the CWPP Agent installation guide pop-up window. For more information, see [Installing Agent]().
Click **Purchase License** to go to the [CWPP Purchase Page](https://buy.intl.cloud.tencent.com/yunjing) to purchase licenses.

### Server List
*Server List** shows the servers on which CWPP is installed, as well as the statistics of the servers by risk and tag.
![](https://qcloudimg.tencent-cloud.cn/raw/e060da123495b0bb820edb7357f1caef.png)
Click **Install CWPP Agent** to open the CWPP agent installation guide pop-up window. For more information, see [Installing Agent](https://intl.cloud.tencent.com/document/product/296/49374).
Click **Upgrade Edition** to go to [License Management](https://console.tencentcloud.com/cwp/setting/authorize), where you can bind the purchased licenses to your servers and upgrade CWPP edition for the servers.
Click **the navigation pane on the right** to filter servers by risk and tag:

| Dimension | Description |
|---------|---------|
| Risk | <li>All Servers: All servers on which CWPP is installed.</li><li> Servers at Risk: The servers where intrusion risks, vulnerability risks, baseline risks, or network risks were detected.</li><li> Servers with CWPP Ultimate: The servers bound to a CWPP Ultimate license.</li><li> Servers with CWPP Pro: The servers bound to a CWPP Pro license.</li><li> Servers with CWPP Basic: The servers that have CWPP Agent installed but are not bound to a license.</li><li> Server Without CWPP Agent (unprotected): The servers on which CWPP Agent is not installed.</li><li> Offline: The servers where CWPP is offline.</li><li> Shutdown: The servers that have been shut down (only applicable to Tencent Cloud servers). |
| Tag | You can set tags to be associated with servers. The servers are listed by tag here. |

You can filter servers by availability zone, region, server IP, and server name.
Click **Refresh** to get the latest server list.
Click **Download** to export the list of filtered servers.
**Field description:**

- Server IP/Name: Private IP and name of the server.
- Operating System: Windows, Linux (CentOS, Debian, Gentoo, RedHat, Ubuntu, TencentOS, CoreOS, FreeBSD, SUSE)
- Risk Status: Safe, Risky, and Unknown.
- Protection Status
 - Unprotected: CWPP agent is not installed on the server.
 - Protected: CWPP agent is installed on the server and is online.
 - Offline: CWPP agent is installed on the server but is offline.
 - Shutdown: The server is shut down (only applicable to Tencent Cloud servers). 
- Risk Count
 - Intrusion Detection: The total of risks detected in Malicious File Scan, Anti-Unusual Login, Anti-Password Cracking, Anti-Malicious Requests, High-risk Command Detection, Anti-Local Privilege Escalation, and Anti-Reverse Shell.
 - Vulnerability Risks: The total number of Linux software vulnerabilities, Windows system vulnerabilities, Web-CMS vulnerabilities, and application vulnerabilities.
 - Baseline Risks: The total number of failed baseline check items.
 - Network Risks: The total number of attack events detected.
- Tags: The tags to be associated with servers (a tag can be associated with multiple servers).
- **Operation**
 - License Management: Click to go to [License Management](https://console.tencentcloud.com/cwp/setting/authorize).
 - Reinstall: Click to open the CWPP Agent installation guide pop-up window. For more information, see [Installing Agent](https://intl.cloud.tencent.com/document/product/296/49374).
 - Uninstall: Open a confirmation pop-up window. It takes about 10 minutes to synchronize CWPP agent status after you confirm uninstallation. (For a server bound to a CWPP license, it must be unbound from the license before CWPP can be uninstalled.)

### Server Details
**Server Details** shows the risk information of the server.
![](https://qcloudimg.tencent-cloud.cn/raw/da64264868a22a1cd7fb491b9433bdc0.png)


