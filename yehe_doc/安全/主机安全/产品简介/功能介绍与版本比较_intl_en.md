Main features in different CWP editions are compared in the table below:    
<table>
<thead>
<th><strong>Category</strong></th>
<th><strong>Feature</strong></th>
<th><strong>Description</strong></th>
<th><strong>Basic<br><nobr>(Free)</strong></th>
<th><strong>Pro<br><nobr>(3 CNY/Day Per CWP Pro)</strong></th>
<th><strong>Value-added Service<br><nobr>(Billed Separately)</strong></th>
</tr>
</tr>
</thead>
<tbody>
<tr>
<td>Security overview</td>
<td>Security overview</td>
<td>Displays the health score, protection status, pending risks, risk trends, and dynamics of your server in real time.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan="5">Asset management</td>
<td>Server list</td>
<td>Supports fuzzy search, screening, enabling protection, and checking server asset information and security risks, facilitating server management.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Port list</td>
<td>Displays the monitoring port, number of servers, IP, process name, process ID, creation time and update time.</td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Account list</td>
<td>Displays the account name, number of servers, IP, type, last login time, and permission change records.</td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Component list</td>
<td>Manages system components and web components, including name, description, path, number of servers, and related details pages.</td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<td>Process list</td>
<td>Displays the process name, process path, number of servers, UUID, server IP, parent process path, process ID, parent process ID, username, operating system, and data collection time.</td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan="7">Intrusion detection</td>
<tr>
<td>Trojans file</td>
<td><ul><li>Web shell detection: detects common web script trojans and backdoors, covering various script languages such as ASP, PHP, JSP, and Python.</li>
<li>Binary virus and trojan detection: detects binary executable viruses and trojans such as DDoS trojans, remote control, mining software, covering .exe, .ddl, and .bin files, and supports alerting.</li></ul></td>
<td>Detects at most 5 risks for free.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Brute force attack</td>
<td><ul><li>Supports real-time detection, warning, and blocking  of brute force attacks such as SSH and RDP, and whitelist configuration for login.</li><li>Supports user-defined blocking rules for brute force attacks, for example, you can set a rule to detect brute force attacks 5 times within 1 minute and block the attacks detected for 15 minutes.</li><li>Records events, including the cracking status, server, attacker IP, attack source, login username, attack time, number of attack attempts and blocking status.</li></ul></td>
<td>CWP Basic only runs detection on brute force attacks.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Suspicious login</td>
<td><ul><li>Detects logins in real time, and automatically identifies non-whitelist IP logins and malicious logins.</li><li>Supports whitelist configuration in terms of login source, source IP, server, login username and login time.</li></ul></td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Local privilege escalation</td>
<td><ul><li>Supports real-time alerts for local privilege escalation, and whitelist configuration.</li><li>Records events, including the server name, privilege escalation user, privilege escalation process, parent process, parent process user, discovery time, file path and process tree.</li></ul></td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Revers shell</td>
<td><ul><li>Supports real-time alerts for reverse shells, and whitelist configuration.</li><li>Records events, including the server name, connection process, parent process, target server, target port, discovery time, file path, process tree and execution commands.</li></ul></td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>High-risk command</td>
<td><ul><li>Records the bash command executed on the CVM, and monitors potentially dangerous operations aligning with the audit rules in real time.
</li><li>Provides default rules and user-defined rules.</li><li>Records events, including the server name, name of the hit rule, danger level, command content, login user and operation time.</li></ul></td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan="4">Vulnerability management</td>
<td>Vulnerability overview and setting</td>
<td><ul><li>Displays the number of protected servers, number of unfixed vulnerabilities, number of affected servers, distribution of vulnerability risk levels, top 5 vulnerabilities, top 5 server risks and vulnerability detection result.</li><li>Supports one-click detection and regular detection, with settings of the scan type, vulnerability level, machine range and scan time, and checking the list of ignored vulnerabilities.</li><li>Supports checking vulnerability details and affected servers by pining the zero-day vulnerability reminder.</li></ul></td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>System component vulnerability detection</td>
<td><ul><li>Detects system-level vulnerabilities and common component vulnerabilities and provides repair solutions for Apache, Nginx, Structs, Redis and other common components. For details, see <a href="https://intl.cloud.tencent.com/document/product/296/34246">System Component Vulnerabilities</a>.</li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, repair plan, reference link, disclosure event, CVE number, CVSS score and radar chart.</li></ul></td>
<td rowspan="2">Detects at most 5 risks for free.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Web application vulnerability detection</td>
<td><ul><li>Detects common web vulnerabilities, and provides repair solutions for phpMyAdmin and WordPress and other web components. For details, see <a href="https://intl.cloud.tencent.com/document/product/296/34245">Web Application Vulnerabilities</a>.</li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, repair plan, reference link, disclosure event, CVE number, CVSS score and radar chart.</li></ul></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Emergency vulnerability</td>
<td><ul><li>Detects recent emergency vulnerabilities (such as zero-day attacks). </li><li>Displays vulnerability details, including the vulnerability description, vulnerability type, threat level, repair plan, reference link, disclosure event, CVE number, CVSS score and radar chart.</li></ul></td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Baseline management</td>
<td>Security baseline</td>
<td><ul><li>Supports baseline inspections such as MLPS level 2 and level 3, CIS, and weak passwords, and provides repair solutions.</li><li>Displays detection result, including the detection server, detection items, baseline pass rate, top 5 baseline detection items and top 5 server risks, and supports one-click detection and regular detection.
For details, see <a href="https://intl.cloud.tencent.com/document/product/296/34243">Security Baseline Checklist</a>.</li></ul></td>
<td>Detects at most 5 risks for free.</td>
<td>Supported</td>
<td>-</td>
</tr>
<td rowspan="2">Advanced defense</td>
<td>Cyber attack</td>
<td>Monitors cyber attacks and supports detecting threats types, including web shell, Struts vulnerability exploitation, code injection, command injection, and batch control and utilization of bots.</td>
<td>None</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Tamper-proof webpage</td>
<td>Supports real-time monitoring of webpage directories, file tamper-proofing, automatic recovery of tampered files, and alarm notifications.</td>
<td>None</td>
<td>None</td>
<td>Billed separately:<br><nobr>1518.02 USD/year per agent</td>
</tr>
<tr>
<td>Sycurity operation</td>
<td>Log analysis</td>
<td>Supports viewing details of all stored traffic logs, log search and query based on statements, and statistical reports and analyses.</td>
<td>None</td>
<td>None</td>
<td>Billed separately:<br><nobr>0.1549 USD/GB/month</td>
</tr>
<tr>
<td rowspan="3">Expert service</td>
<td>Security manager</td>
<td>Provides services such as security consultation, inspection, evaluation and advice service, and an 8/5 expert support via WeChat groups, which is recommended for daily security operations.</td>
<td>None</td>
<td>None</td>
<td>Billed separately:<br><nobr>46.47 USD/month per agent</td>
</tr>
<tr>
<td>Emergency response</td>
<td>Provides comprehensive investigation and emergency response processing. We recommend using this service if your server is invaded and your business is disrupted.</td>
<td>None</td>
<td>None</td>
<td>Billed separately:<br><nobr>929.4 USD per emergency response for one agent</td>
</tr>
<tr>
<td>Network Protection</td>
<td>Allows 24/7 monitoring, and delivers network protection and key protection services in special periods, and provides one-to-one expert support.</td>
<td>None</td>
<td>None</td>
<td>Billed separately:<br><nobr>3,098 USD/day</td>
</tr>
<tr>
<td rowspan="2">Setting</td>
<td>Alarm notification</td>
<td>Supports alarm notifications via SMS and email, and lists of alarm events.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Upgrading</td>
<td>Supports upgrading versions, anti-virus engines, virus databases, and vulnerability databases, and implements functional enhancements.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan="3">Performance</td>
<td>Resource consumption</td>
<td>Each agent requires low resource usage with CPU usage below 5% and memory below 30 MB, which does not affect the system performance.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>High stability</td>
<td>With a high reliability and stability system, CVM can implement mechanisms such as downgrade or suicide to ensure the availability of your business.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Multi-operating system support</td>
<td>Compatible with major operating systems such as Windows, CentOS, Debian, and RedHat.</td>
<td>Supported</td>
<td>Supported</td>
<td>-</td>
</tr>
</tbody></table>
