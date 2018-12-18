### When Will a CNAME Record Be Used?
If you need to point a domain name to another one which will be used to provide the IP address, you need to add a CNAME record. The most common scenarios for CNAME include CDN and corporate email.
### How to Add a CNAME Record
1. Enter the subdomain name for the **Host** (for example, if you want to add the resolution for `www.123.com`, you only need to enter www for the **Host**; if you want to add the resolution for 123.com, the **Host** can be left blank and the system will automatically enter an "@" into the input box. A CNAME record with @ will affect the proper resolution of the MX record, so please be cautious when adding it).
2. The **Record Type** is CNAME.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved. In the figure below, the default value means that all users except those of China Unicom will be pointed to 1.com).
4. The **Record Value** is the domain name pointed to by CNAME and only a domain name can be entered.
![3](//mc.qcloudimg.com/static/img/30a2b97454e0efa21a4ad03be1020043/image.png)
![4](//mc.qcloudimg.com/static/img/a6138bdfbe3ff7401f67140a7853a401/image.png)
