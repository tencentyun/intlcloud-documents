<span id="1"></span>
**About HTTPS**
- [What cipher suites are supported by HTTPS?](#1)
- [Which versions of SSL/TLS security protocols does HTTPS support?](#2)
- [What port can I use for HTTPS listening?](#3)
- [Why HTTPS mutual authentication is needed?](#4)
- [Why does the HTTPS actually generate more traffic than the billed traffic?](#5)
- [Will requests from CLB instances to real servers still be transferred over HTTP after an HTTPS listener is added?](#6)

**About Certificate**
- [What types of certificates does CLB currently support?](#7)
- [How many HTTPS certificates can a listener bind to?](#8)
- [How many cloud load balancers and listeners can one certificate be applied to?](#9)
- [How to upload a certificate?](#10)
- [Is a certificate region-specific?](#11)
- [Does a certificate need to be uploaded to a backend CVM instance?](#12)
- [What should I do after the certificate expires?](#13)
- [What can I do when a certificate error occurs?](#14)


### What cipher suites are supported by HTTPS?
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK

[[Back to Top]](#1)

[](id:2)
### What versions of SSL/TLS security protocols does HTTPS support?
The ssl_protocols supported by CLB HTTPS include TLSv1, TLSv1.1, TLSv1.2, and TLSv1.3.

[[Back to Top]](#1)


[](id:3)
### What port can I use for HTTPS listening?
Not mandatory. Port 443 is recommended.

[[Back to Top]](#1)

[](id:4)
### Why HTTPS mutual authentication is needed?
Some users such as financial service providers have higher requirements for data security. They require HTTPS authentication on both the server and client. To meet their needs, HTTPS two-way authentication is provided.

[[Back to Top]](#1)

[](id:5)
### Why does the HTTPS actually generate more traffic than the billed traffic?
If the HTTPS protocol is used, it actually generates more traffic than the billed traffic as some of the traffic is used for protocol handshake.

[[Back to Top]](#1)

[](id:6)
### Will requests from CLB instances to real servers still be transferred over HTTP after an HTTPS listener is added?
Yes. After an HTTPS listener is added, requests from the client to the CLB instance will be encrypted over HTTPS, but requests from the CLB instance to the real server will still be transferred over HTTP. Therefore, there is no need to configure SSL on the real server.

[[Back to Top]](#1)

[](id:7)
### What types of certificates does CLB currently support?
CLB supports uploading the server certificate and CA certificate. For server certificate, the certificate content and private key need to be uploaded; for CA certificate, only the certificate content needs to be uploaded. Both certificates can be uploaded in PEM encoding format only.

[[Back to Top]](#1)

[](id:8)
### How many HTTPS certificates can a listener bind to?
If HTTPS one-way authentication is used, only one server certificate can be bound to a listener. If HTTPS mutual authentication is used, one server certificate and one CA certificate need to be bound to a listener.

[[Back to Top]](#1)

[](id:9)
### How many cloud load balancers and listeners can one certificate be applied to?
A certificate can be applied to one or more cloud load balancers, or multiple listeners.

[[Back to Top]](#1)

[](id:10)
### How do I upload a certificate?
You can upload it by calling an API or through the CLB console.

[[Back to Top]](#1)

[](id:11)
### Is a certificate region-specific?
No. After the certificate is purchased and issued, its installation and deployment are not restricted by regions.

[[Back to Top]](#1)

[](id:12)
### Does a certificate need to be uploaded to a backend CVM instance?
No. CLB HTTPS provides a certificate management system to manage and store user certificates. Certificates do not need to be uploaded to backend CVM instances, and all the private keys uploaded to the certificate management system are stored in an encrypted manner.

[[Back to Top]](#1)

[](id:13)
### What should I do after the certificate expires?
You need to manually update the certificate.

[[Back to Top]](#1)

[](id:14)
### What can I do when a certificate error occurs?
The error may occur due to incorrect private key. You need to replace the certificate with a new one that meets business requirements.

[[Back to Top]](#1)
