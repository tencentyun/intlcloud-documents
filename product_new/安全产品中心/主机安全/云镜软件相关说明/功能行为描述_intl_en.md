### Web Shell Detection
Web shells are common tools used by hackers for intrusion. The CWP agent will scan new-added web program files on the server for suspicious risks. For a small number of files that are suspected to be web shells, CWP reports them to Tencent Cloud, which then conducts further detection through the machine learning-based detection engine module. After detection, the sample files will be deleted in real time. No private data will be extracted in this process. 

### Abnormal Login Reminder
The abnormal login reminder feature can help you detect abnormal admin login behaviors, which needs to collect the source IP address, time, login username, and login status into login logs and send them to the cloud for risk calculation. The login log data will be retained in the cloud for one month. 

### Password Cracking Reminder
Detect password cracking attacks against your server and show you the log and result of the attacks. It collects and analyzes information in the logs, including source IP address, attack time, login username, and login status. The login logs will be retained in the cloud for one month. 

#### Trojans and Virus Detection
Trojans and virus usually steal user data or launches attacks, which will consume a large amount of system resources and make your business unable to provide services normally. The CWP agent will collect the hash values of suspicious programs to the cloud, and the cloud-based scanning and blocking module will inspect the values. If a value is not found in the cloud-based hash value library, the corresponding executable file will be reported to the cloud and inspected by the cloud-based anti-virus engine. After inspection, the sample file will be deleted in real time. No private data will be extracted in this process. 

### Vulnerability reminder
The vulnerability reminder feature displays server vulnerability risks and provides repair solutions for your reference. This module will download the vulnerability policy library from the cloud, run detection locally, and report the application name, version number, path, and detection time with regard to vulnerability-affected servers. No private data will be extracted in this process. 

### Upgrade and maintenance
The upgrade and maintenance feature mainly informs you of agent upgrades, so that you can obtain the latest security protection services in time. The agent needs to collect the CWP version number, OS configuration information, security rule version number to the cloud for further judgment and prompt. No private data will be extracted in this process. 
