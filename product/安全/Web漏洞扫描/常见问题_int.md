## Product Content
### Does the scan affect website business?
CWS uses non-destructive vulnerability scanning technology. The scan task can be paused at any time and support speed adjustment, enabling you to select the most appropriate scan speed and avoiding the impact on the health of website business.

### What scan IPs are available to CWS?
CWS performs security scanning by means of stimulated hacking on the Internet (with harmless attacks). If your servers have related protection measures in place or restrict the access IPs, it is recommended that you add the following IP addresses to the whitelist in order to ensure normal scanning.
The scanning node IPs of CWS include:
193.112.70.224
193.112.71.109
193.112.70.227
193.112.71.33
193.112.72.165
## Product Implementation
### How do I add a website?
Website is the smallest unit of vulnerability scanning, which can be scanned individually or added to a detection task for scheduled scan.
You can add websites on the website management page. Currently, CWS support adding all regular websites accessed through domain names (websites accessed through IPs will be supported soon), including HTTP and HTTPS, multi-level sub-domain name, ported and multi-level sub-directory websites.
For details, see [Adding a Website](https://intl.cloud.tencent.com/document/product/1001/30022).

### Do I need to repeat the authentication and authorization step when adding multiple sub-domain names under the same root domain name?
No. For example, after qq.com is authorized, v.qq.com and 123.qq.com do not need to be authorized again.

### How do I get a scan report? 
You can go to the monitoring task page, click the number of vulnerabilities corresponding to the target task and then click **Export report** in the upper right corner to export the scan report. 
