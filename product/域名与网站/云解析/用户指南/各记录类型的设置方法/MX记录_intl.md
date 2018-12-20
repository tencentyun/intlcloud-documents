### When Will an MX Record Be Used?
If you need to set up your mailbox so that it can receive mail, you need to add an MX record.
### How to Add an MX Record
1. Enter the subdomain name for the **Host** (usually, email addresses are in the format of `xxx@123.com`, so the **Host** can be generally left blank; if "mail" is entered for the **Host**, the email address format will become `xxx@mail.123.com`).
2. The **Record Type** is MX.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved or receive emails; intelligent resolution is not required for MX records and the default can be used).
4. The **Record Value** can be either a domain name or an IP address. If it is a domain name, the domain name pointed to must have an A record (for example, `mail.123.com` as shown in the figure below), and after the record is generated, a "." is automatically added after the domain name, which is normal. If it is an IP address, directly enter the mail server IP, and after the record is generated, a "." is automatically added too.
5. **TTL** needn't to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).
6. The lower the **MX Priority** value, the higher the priority level (as shown in the figure below, an email will first be sent to 1.1.1.1 with MX priority level 5 and to `mail.123.com` with MX priority 10 if the attempt fails).
![](//mc.qcloudimg.com/static/img/db9bb92dc335c2a23c51c31f132d522f/image.png)
![](//mc.qcloudimg.com/static/img/fc0f0d8798999188d2aeabfea71d7fbd/image.png)
![](//mc.qcloudimg.com/static/img/69782527860e469c637c62fdedf378a7/image.png)
