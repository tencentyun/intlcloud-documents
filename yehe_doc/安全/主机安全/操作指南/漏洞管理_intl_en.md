This document describes how to use the Vulnerability Management feature to manage the vulnerabilities on your servers.

## Overview
Tencent Cloud CWPP allows you to perform periodic and on-demand checks on mainstream servers (Windows, Linux, etc.) for vulnerabilities. CWPP allows you to check specified servers for specified categories of vulnerabilities and ignore certain vulnerabilities. It presents information such as vulnerability risks, vulnerability characteristics, risk level, and solutions in a visualized form to help you better manage vulnerability risks on your servers.

## Important Notes
The Vulnerability Management feature is available only if you have at least one server bound to a (**CWPP Pro/Ultimate**) license.
- Vulnerabilities that can be detected: Linux software vulnerabilities, Windows system vulnerabilities, Web-CMS vulnerabilities, and application vulnerabilities.
- Vulnerabilities that can be fixed automatically: Linux software vulnerabilities (some) and Web-CMS vulnerabilities (some).

## Operation Guide
1. Log in to the [CWPP console](https://console.cloud.tencent.com/cwp).
2. Click **Vulnerability Management** on the left sidebar. The fields and operations related to the feature are described as follows.

### Vulnerability Scan
In the **Vulnerability Scan** section, you can perform a quick scan to obtain the results of the vulnerability scan, or set scheduled scans to identify and fix vulnerabilities in a timely manner.
![](https://qcloudimg.tencent-cloud.cn/raw/62e5cff0f4fb13513123f666d3527e61.png)
- Click **Quick Scan** to open the **Quick Scan Settings** pop-up window. You can perform a scan immediately after setting the vulnerability category, vulnerability level, scan timeout threshold, and servers covered by the scan. 
- Click the edit icon of **Scan Settings** or **Scheduled Scan** to open the **Vulnerability Settings** pop-up window and select **Scheduled Scan**. You can enable scheduled scan, and set scan interval, vulnerability level, and vulnerability categories, which will take effect immediately.
- Click **Details** to view the details of the last scan. You can download the scan reports in a PDF or Excel format.

### Vulnerability List
The vulnerabilities in the **Vulnerability List** are categorized as Urgent Vulnerabilities, Critical Vulnerabilities, and All Vulnerabilities. The three categories are not obviously different from each other in terms of functionality. The fields and operations related to Vulnerability List are described as follows using **All Vulnerabilities** as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/45a671b37113526de3089c109365dca5.png)
Field description:
- Vulnerability Name/Tag: The detected vulnerability and the tag for the vulnerability (remote exploit, service restart, EXP exists, etc.).
- Vulnerability Category: Linux software vulnerabilities, Windows system vulnerabilities, Web-CMS vulnerabilities, and application vulnerabilities.
- Threat Level: Critical, High, Medium, and Low.
- CVSS: The score given by the Common Vulnerability Scoring System. The score ranges from 0 to 10, with 0 indicating the lowest risk and 10 the highest risk.
- CVE No.: A unique number that identifies a vulnerability in the Common Vulnerabilities & Exposures library.
- Last Detected: The time when the vulnerability was last detected.
- **Affected Servers**: The number of servers where this vulnerability was detected.
- Status: Pending, Fixing, Scanning, Fixed, Ignored, and Fix failed.
- **Operation**
 - Solution: For the vulnerabilities that cannot be automatically fixed, you can click **Solution** to open the vulnerability details pop-up window, and manually fix the vulnerability as described in the solution.
 - Auto Fix: Some Linux software vulnerabilities and Web-CMS vulnerabilities can be automatically fixed. You can click "Auto Fix" to open the vulnerability details pop-up window, and select the server to be fixed. For details, see [Auto-Fixing of Vulnerabilities](https://intl.cloud.tencent.com/document/product/296/49376).
 - Rescan: Perform a scan again for this vulnerability.
 - Ignore: Ignore the vulnerability. This vulnerability will no longer be scanned on the server.
