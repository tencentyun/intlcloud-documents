Some attackers may record real server IP history, and the exposed IPs allow them to bypass Anti-DDoS Pro and directly attack your real server. In this case, you are recommended to change the actual real server IP.
You can refer to this document before changing the real server IP to check the risk factors and prevent the new IP from disclosure.

## Checklist
### Checking DNS resolution history
Check all the DNS resolution records of the attacked real server IP, including resolution records of sub-domain names, MX (mail exchanger) records of mail servers, and NS (name server) records. Make sure that all these records are configured to the protected IP so that the DNS will not resolve to the new real server IP.

### Checking for information disclosure and command execution vulnerabilities
- Check your websites or business systems for possible information disclosure vulnerabilities, such as phpinfo() disclosure and sensitive information leakage on GitHub.
- Check your websites or business systems for command execution vulnerabilities.

### Checking for trojans and backdoors
Check your real server for potential trojans, backdoors, and other hidden risks.

## Other Suggestions
- To prevent attackers from scanning C range or other similar IP range, you are not recommended to use the same IP or an IP similar to the old IP as the new real server IP.
- You are recommended to prepare the standby linkage and IP in advance.
- You are recommended to set the scope of access sources to prevent malicious scanning.
