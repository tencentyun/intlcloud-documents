### CNAME Record
A CNAME (Canonical Name) record refers to the alias record in a domain name resolution.
For example, a server named `host.example.com` provides both WWW and MAIL services. To make it easier for users to access those services, two CNAME records (`www.example.com` and `mail.example.com`) can be added for this server at its DNS service provider, and all requests to access these two CNAME records will be forwarded to `host.example.com`.

### CNAME Domain Name
After a domain name is connected in the Tencent Cloud ECDN Console, the system will assign 	a CNAME domain name suffixed with ```.dsa.dnsv1.com``` to the acceleration domain name. Then you need to configure a CNAME record at your domain name service provider. After the record takes effect, the domain name resolution will be taken care of by ECDN and all requests made to this domain name will be forwarded to ECDN nodes.
The figure below shows the order in which **origin server domain name/IP**, **acceleration domain name**, **CNAME domain name** appear when a user sends a request to the origin server:
![](https://main.qcloudimg.com/raw/9eed5c5afbe750d7b46f1a27d04589f1.png)
First, a user accesses an acceleration domain name, then the domain name is resolved to its CNAME domain name on the cache node, and finally the user request arrives at the origin server after being accelerated through Tencent Cloud ECDN.

### Acceleration Domain Name
The acceleration domain name differs from the origin server domain name. It is a domain name you provide to the ECDN cache node to configure CNAME.
>! The origin server domain name must be different from the acceleration domain name.

### Origin Server Domain Name
It refers to the domain name of your business server.

### Origin Server IP
It refers to the IP address of your business server.

### Static Content
It refers to the returned content that stays the same each time users make requests for the same resource, such as HTML, CSS and JS files, images, videos, software installation packages, APK files, and compressed files.

### Dynamic Content
It refers to the returned content that changes each time users make requests for the same resource, such as APIs, JSP, ASP, PHP, PERL, and CGI files.

### Intermediate Server
It refers to the origin-pull server at the middle layer between a business server (origin server) and an edge server. It can cache origin-pull requests of multiple edge servers. For requests to the same content, the intermediate server only needs to perform origin-pull once to deliver the content to each edge server, reducing access pressure on the business server (origin server).
