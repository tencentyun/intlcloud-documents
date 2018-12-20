### When Will an AAAA Record Be Used?
If you want visitors to access your domain name through an IPv6 address, you can add an AAAA record.
### How to Add an AAAA Record
1. Enter the subdomain name for the **Host** (for example, if you want the resolution for `www.123.com`, you only need to enter www for the **Host**; if you want to add the resolution for 123.com, the **Host** can be left blank and the system will automatically enter an "@" into the input box).
2. The **Record Type** is AAAA.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved. In the figure below, the default value means that all users except those of China Unicom will be pointed to ff06:0:0:0:0:0:0:c3).
4. The **Record Value** is the IP address and only an IPv6 address can be entered.
5. **TTL** is the cache time. The smaller the value, the faster the change to the record will take effect in various regions. The default value is 600 seconds.
![](//mc.qcloudimg.com/static/img/2b1e91003b5241e47f7313a820189511/image.png)
![](//mc.qcloudimg.com/static/img/e0ee082c511e65e38c720b1339e6859c/image.png)
