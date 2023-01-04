Main features available in different editions are as compared below:

<table>
<thead>
<tr>
<th>Category</th>
<th colspan=2>Subcategory</th>
<th>Description</th>
<th>Pro</th>
<th>Value-Added Feature</th>
</tr>
</thead>
<tbody><tr>
<td>Security overview</td>
<td colspan=2>Security overview</td>
<td>This feature displays asset (container, image, and server) information, the number of security incidents to be handled, new trends of runtime security incidents, as well as new risk trends and details of local images in real time in visual graphs and charts.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Asset center</td>
<td colspan=2>Asset management</td>
<td>This feature automatically collects the basic information of assets such as containers, images, servers, processes, ports, applications, web services, running applications, and database applications.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan=6>Security enhancement</td>
<td colspan=2>Vulnerability detection</td>
<td>This feature allows quick detection of vulnerabilities in the container environment to facilitate vulnerability emergency response and vulnerability operations. Vulnerabilities are categorized into two types based on the actual handling and response type: system vulnerabilities and web application vulnerabilities.<br>It quickly filters vulnerabilities based on the urgency of their impact on the assets and their priorities. For example, it can display only vulnerabilities that affect the container, vulnerabilities that affect the latest image version, high-priority vulnerabilities, high-risk and extreme vulnerabilities, and remote EXP. In addition, it associates the data of assets affected by vulnerabilities such as local images, repository images, and containers.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan=2>Image risk management</td>
<td>Local image</td>
<td><li>This feature can scan local images quickly or on a scheduled basis to get the basic image asset information and image security risk details.</li><li>It aggregates the total number of risky images, security vulnerabilities, viruses, trojans, and sensitive information in the business environment.</li></td>
<td>-</td>
<td>Supported</td>
</tr>
<tr>
<td>Repository image</td>
<td><li>This feature can scan repository images quickly or on a scheduled basis to get the basic image asset information and image security risk details.</li><li>It aggregates the total number of risky images, security vulnerabilities, viruses, trojans, and sensitive information in the business environment.</li></td>
<td>-</td>
<td>Supported</td>
</tr>
<tr>
<td rowspan=2>Cluster risk management</td>
<td>Cluster check</td>
<td>This feature supports automatic and manual checks to get the basic information and configuration and vulnerability risks of cluster assets, and aggregates the data of risky clusters in the business environment and risks in each cluster. Two cluster check modes are available: general mode and proactive mode.<li>The general mode is the default mode, which doesn't change or affect the cluster status. It is a conventional check method.</li><li>The proactive mode leverages known vulnerabilities for penetration or exploitation and <strong>may change the cluster status, which means it should be enabled with caution in certain scenarios.</strong></li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Risk analysis</td>
<td>This feature organizes risky cluster nodes by extreme, high, medium, and low risk levels and displays the number of affected clusters and nodes by check item.</td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td colspan=2>Baseline management</td>
<td><li>This feature uses CIS Benchmarks to check the security baselines of Docker and Kubernetes and collects the proportion of compliant containers in the business environment as well as the number of extreme-risk, high-risk, medium-risk, and low-risk check items.</li><li>The baseline check result contains the baseline check item, type, baseline standard, severity, check result, and check item details. Check objects include containers, images, servers, and Kubernetes.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan=6>Intrusion protection</td>
<td rowspan=3>Runtime security</td>
<td>Container escape</td>
<td><li>This feature detects sensitive path mounting in the container, privileged containers, privilege escalation events, escape vulnerability exploitation, Docker API access escape, sensitive file tampering escape, and escape with the cgroup mechanism in real time. Detection rules can be enabled/disabled as needed.</li><li>It categorizes alarm events into risky container, program privilege escalation, and container escape to identify risky containers and container escapes.</li><li>Alarm information includes the escape event type, first generation time, last generation time, event count, container name/ID, image name/ID, server name, and Pod name. Alarm details include the event description, solution, and information of the process, parent process, and grandparent process.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
 <td>Reverse shell</td>
<td><li>This feature detects reverse shells in the container in real time and generates alarms. Alarm information includes the process name, parent process name, destination address, process path, first generation time, last generation time, event count, container name/ID, and image name/ID. Alarm details include the risk description, solution, and information of the process, parent process, and grandparent process.</li><li>It allows you to add alarm events to the allowlist or customize a new allowlist by destination address (IP and port), connection process, and affected images.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Virus scanning</td>
<td><li>This feature detects viruses and trojans during container running in real time and generates alarms. Alarm information includes the filename, file path, virus name, first generation time, last generation time, container name/ID, image name/ID, and container status. Alarm details include the malicious file details, event details, solution, and information of the process, parent process, and grandparent process.</li><li>It monitors in real time and scans for malicious files in the container quickly or on a scheduled basis, and allows you to enable automatic isolation of malicious files as needed.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td rowspan=3>Advanced defense</td>
<td>Abnormal process</td>
<td><li>This feature detects abnormal process startups in the container in real time and generates alarms or blocks them. Alarm information includes the process path, hit rule, severity, first generation time, last generation time, event count, container name/ID, image name/ID, and action execution result. Alarm details include the risk description, solution, and information of the process, parent process, and grandparent process.</li><li>The preset policy for abnormal process detection covers at least proxy software, horizontal penetration, malicious commands, reverse shells, fileless program execution, high-risk commands, and abnormal subprocess startups in sensitive services.</li><li>It allows you to add alarm events to the allowlist or customize new process allow rules by process path and affected images.</li><li>It enables you to customize new process detection rules by configuring the rule name, process path, action (block, alarm, allow), and affected images.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
 <td>File tampering</td>
<td><li>This feature detects abnormal file access behaviors in the container in real time and generates alarms or blocks them. Alarm information includes the filename, process path, hit rule, first generation time, last generation time, event count, container name/ID, image name/ID, and action execution result. Alarm details include the risk description, solution, and information of the process, parent process, and grandparent process.</li><li>The preset policy for file tampering covers at least rules about tampering with scheduled tasks, system programs, and user configurations.</li><li>It allows you to add alarm events to the allowlist or customize new allow rules by process path, accessed file path, and affected images.</li><li>It enables you to customize new access control rules, with configurable content such as rule name, process path, accessed file path, action (block, alarm, allow), and affected images.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>High-risk syscall</td>
<td><li>This feature detects high-risk syscalls in the container in real time and generates alarms. Alarm information includes the process path, syscall name, first generation time, last generation time, event count, container name/ID, image name/ID, server name, and Pod name. Alarm details include the risk description, solution, and information of the process, parent process, and grandparent process.</li><li>It allows you to add alarm events to the allowlist or customize a new allowlist by process path, syscall name, and affected images.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Security operations</td>
<td colspan=2>Log analysis</td>
<td><li>This feature allows you to search for container bash logs, container startup audit logs, and Kubernetes API audit logs by time, log type, and log content, and displays the log trend based on the search results. You can customize the displayed and hidden fields of logs, view logs in JSON format, and export logs.</li><li>Log configuration: You can specify whether to enable audit for container bash logs, container startup audit logs, and Kubernetes API audit logs, and whether to enable audit for nodes by log type. You can clear logs by percentage and storage period.</li><li>Log shipping: You can configure CKafka and CLS log shipping as needed. The CKafka log shipping feature can be connected by a public network domain name, and you can select the target message queue instance, public network domain name for connection, and the ID and name of the target topic for each type of log, and specify whether to enable shipping. For CLS log shipping, you can customize logsets and log topics and specify whether to enable shipping.</li></td>
<td>Supported</td>
<td>-</td>
</tr>
<tr>
<td>Settings center</td>
<td colspan=2>Alarm settings</td>
<td>This feature allows you to customize alarm notifications for local images (vulnerabilities, viruses, trojans, and sensitive information), repository images (vulnerabilities, viruses, trojans, and sensitive information), as well as runtime security and advanced defense (container escape, reverse shell, virus scanning, abnormal process, and file tampering) by configuring the alarm status, alarm time, alarm item, and receiving channel (Message Center, email, or SMS).</td>
<td>Supported</td>
<td>-</td>
</tr>
</tbody></table>