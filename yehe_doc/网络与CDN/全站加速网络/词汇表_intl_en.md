### CNAME Domain Name
A CNAME domain name is a domain name (suffixed with ```.ecdn.dnsv1.com```) that is assigned by the system to the connected acceleration domain name configured in the ECDN Console. You need to add a CNAME record at your domain name service provider. After the record takes effect, domain name resolution will be taken care of by ECDN, and all requests made to this domain name will be forwarded to ECDN nodes.
Below displays the order in which the **origin domain/IP**, **acceleration domain name**, and **CNAME domain name** appear in the process from request initiation to request arrival at the origin server:
![](https://main.qcloudimg.com/raw/333d3a43e95f272787bd45332cca21fd.jpg)
When a user accesses an acceleration domain name, the domain name will be resolved to the CNAME domain name on the cache node, and then the request will be forwarded to the origin server, which will be accelerated by ECDN.

### Acceleration Domain Name
Different from an origin server domain name, an acceleration domain name is the domain name you provide to an ECDN cache node for CNAME resolution.

>The origin server domain name must be different from the acceleration domain name.

### Origin Domain
An origin domain is the domain name of your business server.
### Origin IP
An origin IP is the IP address of your business server.




