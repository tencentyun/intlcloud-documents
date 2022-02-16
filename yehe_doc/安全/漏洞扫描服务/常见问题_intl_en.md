### How long does it take to complete a vulnerability scan?
The duration of a vulnerability scan is subject to the number of added assets and the complexity of webpages. Generally, it takes tens of minutes to scan a 100-page website for vulnerabilities.

### Will VSS affect business operations?
No. VSS simulates access requests of real users with precise rate control and won't affect the normal business operations.

### How many IT assets can be scanned by VSS?
VSS relies on the computing power of Tencent Cloud to implement rapid scaling. It can scan tens of millions of IT assets.

### Can I customize keywords for website tampering detection?
Yes. You can customize keywords in the console for monitoring.

### Does VSS only support web vulnerability scan?
VSS can detect weak passwords, webpage compliance issues, as well as vulnerabilities in web services, web middleware, databases, operating systems, software services, IoT devices, routers, cameras, and industrial control devices.

### Does VSS support modern JS frameworks?
Yes. VSS simulates user behaviors by using real browsers and supports modern JS frameworks, including Vue, React, and AngularJS.

### What scanning IPs does VSS have?
VSS performs security scan by simulating hacker intrusions (harmless attacks) over the public network. If your server has protection measures or restricts accessing IPs, in order to ensure normal scanning, we recommend you add the following IP addresses to the allowlist.
The scan node IPs of VSS are as follows:
129.211.162.110
129.211.162.87
129.211.163.253
129.211.164.19
129.211.166.123
129.211.167.182
129.211.167.200
129.211.167.70
129.211.162.158
129.211.162.23
129.211.166.134
129.211.167.108
129.211.167.181
129.211.166.142
129.211.166.163
129.211.167.128
129.211.167.166

### Do I need to repeat verification and authorization when adding multiple subdomains under the same root domain name?
No. For example, if you have already authorized `bb.com`, you don't need to authorize `v.bb.com` and `123.bb.com`.

### How do I get a scan report?
Log in to the [VSS console](https://console.cloud.tencent.com/narms/task-current), click the target task name in the task management section to enter the task details page, click **Download Report**, and the report will be exported.
