### When Will an SRV Record Be Used?
An SRV record is used to identify what server uses what service, which is common to directory management in Windows.
### How to Add an SRV Record
1. The format of the **Host** is name of the service.type of the protocol.
Example: _sip._tcp
2. The **Record Type** is SRV.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved).
4. The **Record Value** format is priority weight port hostname.
Example: 0 5 5060 sipserver.example.com.
After the record is generated, a "." is automatically added after the domain name, which is normal.
5. **MX Priority** needn't to be entered.
6. **TTL** needn't to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect in various regions).
![](//mc.qcloudimg.com/static/img/afcb502b0484cd24b71229c01b27af02/image.png)

