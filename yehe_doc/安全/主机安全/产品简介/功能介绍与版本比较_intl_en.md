This document describes the features of different CWPP editions.

## Features 
The features of different CWPP editions are listed below.    
<table>
<thead>
<th width="10%">Category</th>
<th width="10%">Feature</th>
<th width="30%">Description</th>
<th width="13%">CWPP Basic<br>Free of charge</th>
<th width="13%">CWPP Pro<br>Monthly subscription: 12 USD/month</th>
<th width="13%">CWPP Ultimate<br>Monthly subscription: 27 USD/month</th>
</tr>
</tr>
</thead>
<tbody>
<tr>
<td>Security Dashboard</td>
<td>Security Dashboard</td>
<td>Displays the health score, protection status, pending risks, risk trend, and new security incidents in real time.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td rowspan="3">Asset Management</td>
<td>Asset Dashboard</td>
<td>Displays the statistics of all servers and asset fingerprints, as well as top 5 accounts, ports, processes, software applications, databases, Web applications, Web services, Web frameworks, and Web sites.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Server List</td>
<td>Displays the information of all servers connected to CWPP, helping you get a full picture of the security status of your assets.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Asset Fingerprint</td>
<td>Provides detailed asset inventory data about server resource monitoring, accounts, ports, and processes and helps you quickly investigate the risks of security events that have occurred.</td>
<td>×</td>
<td>&#10003;<br>Supports 10 kinds of fingerprints</td>
<td>&#10003;<br>Supports 15 kinds of fingerprints</td>
</tr>
<td rowspan="8">Intrusion Detection</td>
<tr>
<td>Malicious File Scan</td>
<td><ul><li>Webshell detection: Detects common web script Trojans and backdoors, covering various script languages such as ASP, PHP, JSP, and Python.</li>
<li>Binary virus and Trojan detection: Detects binary executable viruses and Trojans such as DDoS Trojans, remote control, and mining software on .exe, .ddl, and .bin files, and sends alarms.</li></ul></td>
<td>&#10003;<br>Detects at most 5 risks for free</td>
<td>&#10003;<br>Supports detection (no auto isolation)</td>
<td>&#10003;<br>Supports detection, and auto isolation</td>
</tr>
<tr>
<td>Password Cracking</td>
<td><ul><li>Supports real-time detection, alarm, and blocking of brute force attacks on SSH and RDP, and login allowlist configuration. </li><li>Supports user-defined blocking rules for brute force attacks, such as rules to detect brute force attacks 5 times within 1 minute and block the attacks detected for 15 minutes. </li><li>Records events, including the cracking status, server, attacker IP, attack source, login username, attack time, number of attack attempts and blocking status.</li></ul></td>
<td>&#10003;<br>Supports detection only (no blocking)</td>
<td>&#10003;<br>Supports detection and auto blocking</td>
<td>&#10003;<br>Supports detection and auto blocking</td>
</tr>
<tr>
<td>Unusual Login</td>
<td><ul><li>Detects logins in real time, and automatically identifies non-allowlist IP logins and malicious logins. </li><li>Supports allowlist configuration in terms of login source, source IP, server, login username and login time.</li></ul></td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Malicious Requests</td>
<td>Detects the server's internal or external connection requests with malicious domain names in real time, provides threat source information and event records, and sends alarms automatically to users.</td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Local Privilege Escalation</td>
<td><ul><li>Supports real-time alarms for local privilege escalation, and allowlist configuration. </li><li>Records events, including the server name, privilege escalation user, privilege escalation process, parent process, parent process user, discovery time, file path and process tree.</li></ul></td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Reverse Shell</td>
<td><ul><li>Supports real-time alarms for reverse shells, and allowlist configuration. </li><li>Records events, including the server name, connection process, parent process, target server, target port, discovery time, file path, process tree and execution commands.</li></ul></td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>High-risk Commands</td>
<td><ul><li>Records the bash command executed on the CVM, and monitors potentially dangerous operations aligning with the audit rules in real time.
</li><li>Provides default rules and user-defined rules. </li><li>Records events, including the server name, matched rule name, threat level, command content, login user and operation time.</li></ul></td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td rowspan="5">Vulnerability Management</td>
<td>Urgent Vulnerability</td>
<td><ul><li>Detects recent urgent vulnerabilities (such as zero-day attacks).
</li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, fix scheme, reference link, disclosure event, CVE number, CVSS score, and radar chart.</li></ul></td>
<td rowspan="5">&#10003;<br>Detects at most 5 risks for free</td>
<td rowspan="5">&#10003;<br>Supports detection (no fixing)</td>
<td rowspan="5">&#10003;<br>Supports detection and partial fixing</td>
</tr>
<tr>
<td>Linux Software Vulnerability</td>
<td><ul><li>Detects gnutls resource management errors and other common Linux software vulnerabilities and provides fix schemes.
</li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, fix scheme, reference link, disclosure event, CVE number, CVSS score, and radar chart.</li></ul></td>
</tr>
<tr>
<td>Windows System Vulnerability</td>
<td><ul><li>Detects and provides fix schemes for Windows system vulnerabilities by syncing the patch sources on Microsoft's official website in real time, to prevent hackers from attacking or threatening your server through the vulnerabilities.</li><li> Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, fix scheme, reference link, disclosure event, CVE number, CVSS score, and radar chart.</li></ul></td>
</tr>
<tr>
<td>Web-CMS Vulnerability</td>
<td><ul><li>Checks phpMyAdmin, WordPress and other web components for common Web vulnerabilities and provides fix schemes.</li><li> Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, fix scheme, reference link, disclosure event, CVE number, CVSS score, and radar chart.</li></ul></td>
</tr>
<tr>
<td>Application Vulnerability</td>
<td><ul><li>Provides weak password detection for system services, as well as vulnerability detection for system and application services.
</li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, fix scheme, reference link, disclosure event, CVE number, CVSS score, and radar chart.</li></ul></td>
</tr>
<tr>
<td rowspan="3">Security Baseline</td>
<td>CIS Baseline Standard</td>
<td rowspan="3"><ul><li>Supports baseline checks against CIS and weak passwords, and provides fix schemes. </li><li>Displays check results, including the check server, check items, baseline pass rate, top 5 baseline check items and top 5 server risks, and supports periodic and quick checks.</li></ul></td>
<td rowspan="3">&#10003;<br>Detects at most 5 risks for free</td>
<td rowspan="3">&#10003;<br>Supports detection (no customization)</td>
<td rowspan="3">&#10003;<br>Supports detection and customization</td>
</tr>
<tr>
<td>Tencent Cloud Baseline Standard</td>
</tr>
<tr>
<td>Weak Password Baseline</td>
</tr>
<tr>
<td rowspan="1">Advanced Defense</td>
<td>Core File Monitoring</td>
<td>You can configure monitoring rules for core files and view and process monitoring events. You can also configure the allowlist to allow permitted access to files. (Only operating systems with Linux kernel 3.10 or above are supported.)</td>
<td>×</td>
<td>×</td>
<td>&#10003;</td>
</tr>
<tr>
<td rowspan="2">Settings</td>
<td>Alarm Notification</td>
<td>Supports alarm notifications via SMS and email, and lists of alarm events.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>License Management</td>
<td>If you have purchased the CWPP Pro or CWPP Ultimate, you can bind the server to upgrade its protection level on the License Management page. You can also unbind an upgraded server.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td rowspan="3">Performance</td>
<td>Resource Consumption</td>
<td>Each agent requires low resource usage with CPU usage below 5% and memory below 30 MB, which does not affect the system performance.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>High Stability</td>
<td>With a high-reliability and high-stability system, CVM can implement mechanisms such as downgrade or suicide to ensure the availability of your business.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr>
<td>Multi-Operating System Support</td>
<td>Compatible with major operating systems such as Windows, CentOS, Debian, and RedHat.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
</tbody></table>
