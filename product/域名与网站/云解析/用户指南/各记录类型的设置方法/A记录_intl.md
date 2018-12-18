### When Will an A Record Be Used?
If you need to point a domain name to an IP address, you need to add an A record.
### How to Add an A Record
1. Enter the subdomain name for the **Host** (for example, if you want the resolution for `www.123.com`, you only need to enter www for the **Host**; if you want to add the resolution for 123.com, the **Host** can be left blank and the system will automatically enter an "@" into the input box).
2. The **Record Type** is A.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved. In the figure below, the default value means that all users except those of China Unicom will be pointed to 10.10.10.10).
4. The **Record Value** is the IP address and only an IPv4 address can be entered.
5. **TTL** is the cache time. The smaller the value, the faster the change to the record will take effect in various regions. The default value is 10 minutes (600 seconds).
![1](//mc.qcloudimg.com/static/img/82400afe3c333b11ec5c35058fda4d61/image.png)
![2](//mc.qcloudimg.com/static/img/14c8e2c1fb2ae27ab803393b478053b6/image.png)
