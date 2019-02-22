[//]: # (chinagitpath:XXXXX)

As some attackers may record the IPs used by the real server, there can be such a circumstance that attackers bypass the protective IP and directly attack the real server IP. In this case, it is recommended to change the real server IP.
You can check the factors that may lead to exposure of the real server IP by referring to this document before changing the real server IP, so as to avoid exposure of the new real server IP.

## Checking Methods
### Check DNS resolution records
Check all the DNS resolution records on the previously attacked real server IP, such as resolution records of sub-domain names, MX (Mail Exchanger) records of mail servers and NS (Name Server) records, and make sure that all of them are configured to the protective IP, so as to avoid some resolution records being directly resolved into the new real server IP.

### Check for information disclosure and command execution vulnerabilities
- Check websites or business systems for information disclosure vulnerabilities, such as phpinfo() disclosure and GitHub disclosure.
- Check websites or business systems for command execution vulnerabilities.

### Check for Trojans and backdoors
Check the real server for Trojans, backdoors and other hidden dangers.

## Other Suggestions
- It is suggested not to use an IP in an IP address range the same as or similar to that of the previous real server IP as the new real server IP, so as to avoid attackers from guessing and scanning Class C or similar IP address ranges.
- It is suggested that backup linkage and backup IP be prepared in advance.
- It is suggested to set the scope of access sources to avoid malicious scanning by attackers.
- It is suggested that you apply this product by referring to [Real Server-based Defense Scheduling Solution](https://cloud.tencent.com/document/product/1014/31125) based on your actual demands.

