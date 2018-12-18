### What Is Implicit/Explicit Forwarding?

Take the redirect from `http://a.com` to ` http://cloud.tencent.com/ ` as an example.

**Implicit forwarding** uses the iframe frame technology but not redirect technology. The effect is when `http://a.com` is entered in the address bar of the browser and Enter is hit, the website content opened is that of the destination address `http://cloud.tencent.com/`, but the address bar shows the current address `http://a.com`.
>**Note:**
>If the destination address doesn't allow to be nested (such as Qzone), implicit forwarding cannot be used. 
 
**Explicit forwarding** uses the 301 redirect technology. The effect is when `http://a.com` is entered in the address bar of the browser and Enter is hit, the website content opened is that of the destination address `http://cloud.tencent.com/`, and the address bar shows the destination address `http://cloud.tencent.com/ `.
### How to Add Implicit/explicit Forwarding Records?
1. Enter the subdomain name prefix for **Host**.
2. The **Record Type** is implicit URL/explicit URL.
3. **Line Type** (required by default; if left blank, some users may not be able to be resolved).
4. The **Record Value** must be a complete address (which must contain the protocol and domain name and can contain the port number and resource locator).
5. **MX Priority** needn't to be entered.
6. **TTL** needn't to be entered. The system will automatically generate it when adding the record. The default is 600 seconds (TTL is the cache time. The smaller the value, the faster the change to the record will take effect).

### When Will URL Forwarding Be Used?
To point a domain name to another existing website, you need to add a URL record.
