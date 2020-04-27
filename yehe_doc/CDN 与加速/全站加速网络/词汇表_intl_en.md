### CNAME Domain Name
A CNAME domain name is a domain name (suffixed with ```.ecdn.dnsv1.com```) that is assigned by the system to the connected acceleration domain name configured in the ECDN Console. You need to add a CNAME record at your domain name service provider. After the record takes effect, domain name resolution will be taken care of by ECDN, and all requests made to this domain name will be forwarded to ECDN nodes.
The order that the **origin server domain name/IP**, **acceleration domain name**, and **CNAME domain name** arrive at the origin server when a user sends a request is as shown below:
![](https://main.qcloudimg.com/raw/229c51a8a73a2038fa8eb0d3f29667bc.png)
When a user accesses an acceleration domain name, the domain name will be resolved to the CNAME domain name on the cache node, and then the request will be forwarded to the origin server, which will be accelerated by ECDN.

### Acceleration Domain Name
Different from an origin server domain name, an acceleration domain name is one that you provide to an ECDN cache node for CNAME resolution.

>The origin server domain name must be different from the acceleration domain name.

### Origin Server Domain Name
An origin server domain name is the domain name of your business server.
### Origin Server IP
An origin server IP is the IP address of your business server.




