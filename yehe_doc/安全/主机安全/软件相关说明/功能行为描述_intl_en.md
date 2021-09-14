### Web shell detection
Web shells are common in hackers’ attacks. The CWP agent will scan newly created web program files on the server for suspicious risks. For a small number of files that are suspected to be web shells, CWP reports them to Tencent Cloud, which then conducts further detection through the machine learning detection engine. After detection, the sample files will be deleted in real time. CWP runs a full scan every day by default. No private data will be extracted in this process. 

### Abnormal login reminder
The abnormal login reminder allows you to identify abnormal admin logins. The source IP, time, login user name and login status data in the login log need to be collected for computing risks. The login log data is retained on cloud for one month. 

### Password cracking reminder
Detect password cracking attacks against your server and show you the log and result of the attacks. It collects and analyzes information in the logs, including source IP address, attack time, login username, and login status. The login logs will be retained in the cloud for one month. 

### Malicious Trojans and virus detection
Malicious Trojans and virus programs usually steal user data or launches attacks, which will consume a large amount of system resources and make your business unable to provide services normally. The CWP agent will collect the [hash values](https://intl.cloud.tencent.com/document/product/296/34241) of suspicious programs to the cloud, and the cloud-based scanning and blocking module will inspect the values. If a value is not found in the cloud-based hash value library, the corresponding executable file will be reported to the cloud and inspected by the cloud-based anti-virus engine. After inspection, the sample file will be deleted in real time. CWP runs a full scan every day by default. No private data will be extracted in this process. 

### Vulnerability alert
The current CWP supports detecting Linux and Windows vulnerabilities and security baselines complying with Tencent Cloud requirements.
The vulnerability management feature presents the vulnerability risks on the current server and provides a repair solution to you for reference. This module downloads vulnerability policy library from the cloud to perform detection locally, and reports the name, version number, path, and discovery time of application for a server with vulnerability risk. No data related to user privacy is fetched during the process. 

### Upgrade and maintenance
The upgrade and maintenance feature mainly informs you of agent upgrades, so that you can obtain the latest security protection services in time. The agent needs to collect the CWP version number, OS configuration information, security rule version number to the cloud for further judgment and prompt. No private data will be extracted in this process. 
