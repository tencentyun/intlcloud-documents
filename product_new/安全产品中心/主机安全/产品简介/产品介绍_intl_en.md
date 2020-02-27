## What Is Cloud Workload Protection (CWP)?

Tencent Cloud Workload Protection leverages the massive amount of threat data accumulated by Tencent Security and uses machine learning algorithms to provide security services such as intrusion detection and vulnerability alerts. Features offered includes password cracking prevention, suspicious login alerts, trojan detection, and high-risk vulnerability detection. It helps enterprises build a security protection system to deal with major network security risks.

## Why Do You Need CWP?

Once your server is intruded by hackers, you will face the following security risks:
- **Business interruption**: the databases and files are tampered with or deleted, end users cannot access your services, and your system crashes.
- **Data theft**: hackers steal your data and sell it publicly. Your users' private data is leaked, resulting in damaged enterprise brand image and customer loss.
- **File encryption by ransomware**: hackers intrude your server and implant irreversible encrypted ransomware to encrypt your data for ransom.
- **Unstable service**: hackers run cryptomining malware or DDoS trojan programs on your server, consuming a large amount of system resources and making the server unable to provide normal service.

CWP can effectively prevent the above problems and guarantee security for your servers.

## CWP's Main Features

### Trojan detecting and killing
A website backdoor trojan (also known as “web shell”) is a dynamic script in ASP, PHP, JSP, or other language implanted by hackers after they intrude a website through a vulnerability. Hackers can continuously control a server using a backdoor trojan and do harms such as file upload and download and command execution, which is extremely detrimental to website security.
Featuring the machine learning-based website backdoor detection technology and harnessing Tencent Cloud security platform's capability of collecting malicious file samples from the entire network, CWP can accurately detect and kill various trojan files. In addition, it provides features such as malicious file detection and quick quarantine to protect your server security.

### Password cracking reminder

Your servers can be logged in to through the internet, which leaves opportunities for hackers to intrude them using brute force attacks. CWP uses various methods to detect whether your CVM instance passwords have been cracked by brute force. Once an exception is detected, CWP will inform you of it through internal message and SMS.

### Login audit

Based on common login locations and malicious login sources, CWP analyzes server login logs, identifies login in unusual locations and abnormal logins in the server login transactions, and reports them in real time. Plus, it can analyze server account login behaviors and alert you to suspicious login behaviors in real time.
With CVM's log query feature, you can compare your login activities against the records in the logs to identify abnormal login attempts and take security measures.

### Vulnerability management

CWP provides real-time alerts and solutions for high-risk system and web vulnerabilities on your server. This enables you to quickly respond to the issues.

### Asset management

CWP manages your assets in a unified manner, where you can tag and group CVM instances for easier management and gain insights into the distribution of software processes and ports on the instances through the component identification technology.
