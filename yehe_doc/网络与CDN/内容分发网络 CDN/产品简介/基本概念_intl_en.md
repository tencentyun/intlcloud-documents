

### Origin server
This refers to your stably running business server. On the CDN Console, you can select an external server or COS as the origin server.

### External origin
This refers to a server where your own web service is deployed. When connecting to an acceleration domain name, you can enter the server's public IP address as the origin server.

### COS origin
If resources have already been stored in COS, a bucket can be selected as the origin server.

### Edge server
This refers to a network node that CDN uses to cache the content of your origin server in order to quickly respond to user requests from different regions.

### CNAME Record
A CNAME (Canonical Name) record refers to the alias record in a domain name resolution.
For example, a server named `host.example.com` provides both WWW and MAIL services. To make it easier for users to access those services, two CNAME records (`www.example.com` and `mail.example.com`) can be added for this server at its DNS service provider, and all requests to access these two CNAME records will be forwarded to `host.example.com`.

### CNAME Domain Name
This refers to a domain name suffixed with `.cdn.dnsv1.com` that is assigned by the system to the connected acceleration domain name configured on the CDN Console. You need to configure a CNAME record at your domain name service provider. After the record takes effect, CDN will take care of domain name resolution, and all requests made to this domain name will be forwarded to the edge servers of CDN.

### Static Content
This refers to content that stays the same in the responses to multiple requests for the same resource.
Examples include html, css and js files, images, videos, software installation packages, APK files, and compressed files.

### Dynamic Content
This refers to content that varies in the responses to multiple requests for the same resource.
Examples include APIs and .jsp, .asp, .php, .perl, and .cgi files.

### Origin-pull
In CDN, an origin-pull means that when a user sends a request from a browser, the server that responds to the request is the server of the source website rather than a cache server on a CDN node. Generally, if the content is not cached on the cache server or is modified on the origin server, it will be pulled from the origin server.

### Origin domain
This refers to the site domain name accessed on the origin server by a CDN node during origin-pull. For more information, please see [Origin Server Configuration](https://intl.cloud.tencent.com/document/product/228/6289).

### Domain name
This refers to a set of server addresses that users can easily remember and use, and can be a website, email, FTP, etc. It is used to identify a computer’s electronic location (sometimes referred to as geographic location) during data transfer.


### Bucket
In COS, a bucket is for storing a object or multiple objects. A bucket name is a user-defined string connecting a system-generated numeric string with dash, thus ensuring that this bucket name is unique. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
