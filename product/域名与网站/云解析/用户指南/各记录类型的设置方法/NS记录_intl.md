### When Will an NS Record Be Used?
If you need to delegate a subdomain name to another DNS service provider for resolution, you need to add an NS record.
### How to Add an NS Record
1. Enter the subdomain name for the **Host** (for example, if you want to delegate the resolution of `www.123.com` to another DNS server, you only need to enter www for the **Host**. An "@" **Host** cannot be used as an NS record. Delegating a subdomain doesn't affect the normal resolution of other subdomain names).
2. The **Record Type** is NS.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved).
4. The **Record Value** is the domain name of the DNS server to be delegated to. After the record is generated, a "." is automatically added after the domain name, which is normal.
5. **TTL** needn't to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).
6. **MX Priority** needn't to be entered.
![](//mc.qcloudimg.com/static/img/ade89d17313705d405470208397d3a2a/image.png)
