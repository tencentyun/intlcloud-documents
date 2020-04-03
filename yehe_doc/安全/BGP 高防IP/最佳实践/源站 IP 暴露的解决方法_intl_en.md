Some attackers may record real server IP history, and the exposed IPs allow them to bypass Anti-DDoS Advanced and directly attack your real server. In this case, you are recommended to change the actual real server IP.
If you don't want to change the IP of your real server or have already done so but the IP is still exposed, in order to prevent attacker from bypassing Anti-DDoS and directly attack your real server IP, please follow the steps below:
- To prevent attackers from scanning C range or other similar IP ranges, do not use the same IP or an IP similar to the old IP as the new real server IP.
- Prepare the standby linkage and standby IP in advance.
- Set the scope of access sources to prevent malicious scans.
- Follow the instructions in [Real Server-Based Defense Scheduling Solution](https://intl.cloud.tencent.com/document/product/297/15564) and apply the solution based on your actual needs.


> Before changing the real server IP, be sure to confirm that all factors that may expose the IP have been eliminated.


You can refer to the following steps before changing the real server IP to check the risk factors and prevent the new IP from disclosure.
## Checklist
### Checking DNS resolution history
Check all the DNS resolution records of the attacked real server IP, including resolution records of sub-domain names, MX (Mail Exchanger) records of mail servers, and NS (Name Server) records. Make sure that all those records are configured for protection by Anti-DDoS Advanced, so that none of them will be resolved to the new real server IP.
### Checking for information disclosure and command execution vulnerabilities
- Check your websites or business systems for possible information disclosure vulnerabilities, such as phpinfo() disclosure and sensitive information leakage on GitHub.
- Check your websites or business systems for command execution vulnerabilities.


### Checking for trojans and backdoors
Check your real server for potential trojans, backdoors, and other hidden risks.
