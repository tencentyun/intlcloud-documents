[//]: # (chinagitpath:XXXXX)

Some attackers may record real server IP history, and the exposed IPs allow them to directly attack your real server. Therefore, we recommend you hide the actual real server IP.  Before changing the real server IP, you can refer to this document and check the risk factors, which may lead to the exposure of the real server IP,  to avoid new IP disclosure.

## Methods
### Check DNS resolution historical records
Check all the DNS resolution history of the attacked real server IP, including resolution records of sub-domain names, MX (Mail Exchanger) records of mail servers and NS (Name Server) records. Make sure all of these records are configured to the Anti-DDoS Advanced IP so that the DNS is not resolving to the new real server IP.

### Check for information disclosure and command execution vulnerabilities
- Check websites or business systems for possible information disclosure vulnerabilities, such as phpinfo() disclosure and sensitive information leakage on Github.
- Check websites or business systems for command execution vulnerabilities.

### Check for Trojans and backdoors
Check the real server for potential Trojans, backdoors and other hidden dangers.

## Other Suggestions
- To prevent attackers scanning C range or other similar IP range, we recommend you use a range for the new real server IP different from the one for the old real server IP. 
- We recommend that you prepare the backup linkage and the backup IP in advance.
- We recommend that you set the scope of access sources to prevent malicious scanning.
- We recommend that you refer to [Real Server-based Defense Scheduling Solution](https://cloud.tencent.com/document/product/1014/31125) and apply the solution based on your actual demands.
