This document describes how to use the Malicious File Scan feature.

## Overview
Based on Tencent Cloud's tens of billions of samples, Malicious File Scan supports the detection of malicious files such as mining Trojans and Ransomware by using such engines as Cloud Security, Anti-Webshell, and TAV.

## Important Notes
The Malicious File Scan feature is available only if you have at least one server bound to a (CWPP Pro/Ultimate) license.
- Detection method.
  - Webshell detection: Detects common Webshells in languages such as ASP, PHP, JSP, and Python.
  - Binary detection: Detects binary executable viruses and Trojans, such as DDoS Trojans, remote control, and mining software for .exe, .dll, and .bin files, and sends alerts to users.


## Operation Guide
1. Log in to the [CWPP console](https://console.intl.cloud.tencent.com/cwp).
2. Click **Intrusion Detection** > **Malicious File Scan** on the left sidebar. The fields and operations related to the feature are described as follows.

### File Scan Settings
Click the **File Scan Settings** button in the upper right corner to set **Scheduled Check**, **Real-Time Monitoring**, and **Auto Isolation**.
- Scheduled Check: You can enable or disable scheduled checks, and set check mode, engine, check interval, and covered servers.
![](https://qcloudimg.tencent-cloud.cn/raw/0a45e64501e2d63f5f7ac062f9475957.png)

| Item | Description |
|---------|---------|
| Enable Scheduled Check | Enables or disables scheduled checks. You can regularly scan Trojan virus files on servers to enhance security. |
| Check Mode | Set check mode to define the check scope.<br> Quick Check: Checks running processes, key directories, drive loading, etc.<br> Overall Check: Checks all partitions of the system besides the scope of Quick Check. |
| Engine Mode | Increase detection rate by adjusting the engine mode.<br> Standard: Detects mainstream Trojans and virus files accurately and efficiently. |
| Check Interval | Performs a check daily, every 3 days, and every 7 days. |
| Covered Servers | Servers with CWPP Pro/Ultimate or Selected Servers. |

- Real-time Monitoring: Monitors Web directories and key system directories, and scans & removes Trojan virus files. You can set the monitoring mode.
![](https://qcloudimg.tencent-cloud.cn/raw/eb22cd00ff7680c5ed6e7a58d8980ded.png)

| Item | Description |
|---------|---------|
| Enable Real-time Monitoring | Enables/disables real-time monitoring of Web directories and key system directories, and scans & removes Trojan virus files. |
| Monitoring Mode | Set monitoring mode to define the scope of monitored files. <br>Standard (recommended): Monitors and scans incremental files in common directories.<br> Enhanced: Monitors and scans incremental files in all directories. |

- Auto Isolation: Automatically isolates detected malicious files. Some malicious files still need to be manually confirmed and isolated. We recommend that you check all the security events in the file scan list to ensure that all of the files are handled. You can de-isolate the files that are isolated by mistake in the list of isolated files.
![](https://qcloudimg.tencent-cloud.cn/raw/d8c8892711c00dd70b85454608f6de92.png)

| Item | Description |
|---------|---------|
|Enable Auto Isolation | Enables/disables auto isolation of detected malicious files. (It takes several minutes for the enabling or disabling of Auto Isolation to take effect) |
| Isolate and Kill Process | In the actual scenario, the file process may be still running after the file is isolated.<br> It is recommended to select this option to kill the process related to the malicious file while isolating the file automatically. |

### Risk Overview
The **Risk Overview** shows the statistics of servers with different CWPP editions, as well as the pending risk files and the number of affected servers.
![](https://qcloudimg.tencent-cloud.cn/raw/d0c8fd31ad57caa95fe3284a4821bd24.png)

### Quick Check
Click the **Quick Check** button to set the check mode, engine, covered servers, and timeout threshold.
![](https://qcloudimg.tencent-cloud.cn/raw/fede8bb9c27ba6f0062f617f842b1dd1.png)

<dx-alert infotype="explain" title="">
The possible reason for timeout: A long scan duration due to a large number of files and directories.
</dx-alert>

### Event List
The **Event List** section shows the servers protected by CWPP and the malicious files detected.
![](https://qcloudimg.tencent-cloud.cn/raw/3cc9fcf8edef9cc7c64ef3b734134762.png)

**Field description:**
 - Server IP/Name: The server where a suspicious file was detected.
 - Path: The path of the suspicious file, which can be copied for downloading the file.
 - Virus Name/Detection Engine: The name of the virus affecting the suspicious file, and the engine that detected the virus.
 - Threat Level: Critical, High, Medium, Low, and Warning.
 - First Detected: The time when the suspicious file was first detected.
 - Last detected: The time when the file risk was last detected.
 - Status
   - Pending: The status of the file and process when the file was last scanned.
   - Isolated: The file has been isolated automatically or manually.
   - Trusted: The file is trusted.
   - Cleared: The file and process no longer exist in the latest scan.
   - Isolating: The file is being isolated.
   - De-isolating: An isolated file is being de-isolated.
 - **Operation**
   - Isolate: Isolate the virus file to prevent hackers from launching it again. This allows you to locate and remove the virus file. In Windows, isolation may fail if this file is running. It is recommended to select the option of "Isolate and Kill Process".
   - Trust: If a file is confirmed to be non-malicious, you can select Trust so that the CWPP will no longer scan the file. You can filter and manage trusted files.
   - Delete Record: This action only deletes log records, rather than the file. Once deleted, the log information cannot be recovered. It is recommended to select "Isolate" or "Trust" first, or locate the file in the path and delete it manually.
   - Details: View event details, including virus file information, risk description, solutions, etc.




