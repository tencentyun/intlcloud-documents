### When Will a TXT Record Be Used?
If you want to identify and describe a domain name, you can use a TXT record. Most TXT records are used as SPF records (for anti-spam).
### How to Add a TXT Record
1. Enter the subdomain name for the **Host** (for example, if you want to add a TXT record of `www.123.com`, you only need to enter www for the **Host**; if you want to add a TXT record of 123.com, the **Host** can be left blank and the system will automatically enter an "@" into the input box).
2. The **Record Type** is TXT.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved; intelligent resolution is not required for TXT records and the default can be used).
4. The **Record Value** doesn't have a fixed format, but in most cases, TXT records are used as SPF records for anti-spam. A typical SPF-format TXT record example is "v=spf1 a mx ~all", which means that only the IP addresses listed in the A and MX records of this domain name have the permission to use this domain name to send emails.
5. **MX Priority** needn't to be entered.
6. **TTL** needn't to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).
![](//mc.qcloudimg.com/static/img/77b55e2f5fb0263fc5ff1cb13fb442cb/image.png)
