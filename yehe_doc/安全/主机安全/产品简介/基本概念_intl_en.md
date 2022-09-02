This document describes the basic concepts of CWPP.

## Basic Concepts
Common concepts of CWPP are as follows.
### Security baseline
A security baseline is a specific set of standards and basic requirements that relevant system and service security configurations must meet to satisfy security needs. Projects of different configurations and policies, such as account configuration security, password configuration security, authorization configuration, log configuration, and network configuration, are used to evaluate whether a product has met the security baseline. The evaluation result reflects the server security to some extent.
### Trojan virus
A Trojan virus is a piece of malicious code or a backdoor program hidden in legitimate applications that has the capability to destroy and delete files, send passwords, record keystrokes, and launch DDoS attacks among others.
### WebShell
WebShell is a command execution environment that exists as webpage files such as .asp, .php, .jsp or .cgi files, and is a type of web backdoor. After gaining access to a website, hackers usually mix the backdoor files with the normal webpage files in the WEB directory of the website server, thus gaining access to the asp or php backdoor with the browser, and getting a command execution environment to control the website server.
### Vulnerability detection
Host vulnerability detection refers to the method of a CWPP agent to detect vulnerabilities on a server. The vulnerability detection module runs on the server and can directly verify or collect information to determine whether the server has vulnerabilities.
### System component
In a general sense, a component (or common component) at the server layer refers to a web container or software program corresponding to a service or application, such as Nginx and WordPress. A system component mainly refers to non-web system software.
### Common component vulnerability
A common component vulnerability (aka common vulnerability) mainly refers to a vulnerability in a common component instead of business code, such as SQL injection in WordPress and ShellShock in a component's Bash.
### Unauthorized access
Unauthorized access is a type of problems caused by failure to meet the security baseline and mainly refers to the lack of restrictions on the conditions for access to certain services, such as password setting and access source restriction. In this case, anyone can directly connect to the service and perform operations, resulting in security problems.
### Abnormal login
With RDP and SSH login logs collected from the server, information such as login source IP, login username, login time, and login location is reported to the cloud for risk assessment, so as to send alarms against illegal logins in real time.
### File isolation
The isolation technology is to isolate and store malicious Trojans and virus files to prevent them from spreading.