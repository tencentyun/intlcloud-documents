<span id="1"></span>
**HTTPS**
- [What cipher suites are supported by HTTPS?](#1)
- [What types of SSL/TLS protocols are supported by HTTPS?](#2)
- [Which port should be used for HTTPS listeners?](#3)
- [Why HTTPS mutual authentication is needed?](#4)
- [Why does HTTPS protocol actually generate more traffic than the billed traffic?](#5)
- [Will the requests from CLB instances to real servers still be transferred over HTTP after an HTTPS listener is added?](#6)

**Certificates**
- [What types of certificates does CLB currently support?](#7)
- [How many HTTPS certificates can be bound to a listener?](#8)
- [How many CLB instances or listeners can a certificate be applied to?](#9)
- [How to upload certificates?](#10)
- [Are certificates region-specific?](#11)
- [Does a certificate need to be uploaded to a backend CVM instance?](#12)
- [What to do after a certificate expires?](#13)
- [What can I do if an error occurs when adding a certificate?](#14)


### What cipher suites are supported by HTTPS?
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK

[[Back to Top]](#1)

<span id="2"></span>
### What types of SSL/TLS protocols are supported by HTTPS?
CLB HTTPS currently supports the following SSL protocols: TLSv1, TLSv1.1,TLSv1.2,and TLSv1.3.

[[Back to Top]](#1)

<span id="3"></span>
### Which port should be used for HTTPS listeners?
There is no mandatory requirement for this. Port 443 is recommended.

[[Back to Top]](#1)

<span id="4"></span>
### Why HTTPS mutual authentication is needed?
Some users such as financial service providers have higher requirements for data security. They require HTTPS authentication on both the server and client. To meet their needs, HTTPS mutual authentication is provided.

[[Back to Top]](#1)

<span id="5"></span>
### Why does HTTPS protocol actually generate more traffic than the billed traffic?
If the HTTPS protocol is used, it actually generates more traffic than the billed traffic as some of the traffic is used for protocol handshake.

[[Back to Top]](#1)

<span id="6"></span>
### Will the requests from CLB instances to real servers still be transferred over HTTP after an HTTPS listener is added?
Yes. After an HTTPS listener is added, the requests from the client to the CLB instance will be encrypted over HTTPS, but the requests from the CLB instance to the real server will still be transferred over HTTP. Therefore, there is no need to configure SSL on the real server.

[[Back to Top]](#1)

<span id="7"></span>
### What types of certificates does CLB currently support?
It currently supports the upload of server certificates and CA certificates. For server certificates, both certificate content and private key are required to be uploaded. For CA certificates, only certificate content is required to be uploaded. Both types of certificates only support upload in PEM encoding format.

[[Back to Top]](#1)

<span id="8"></span>
### How many HTTPS certificates can be bound to a listener?
If HTTPS one-way authentication is used, only one server certificate can be bound to a listener. If HTTPS mutual authentication is used, one server certificate and one CA certificate need to be bound to a listener.

[[Back to Top]](#1)

<span id="9"></span>
### How many CLB instances or listeners can a certificate be applied to?
A certificate can be applied to one or multiple CLB instances or listeners.

[[Back to Top]](#1)

<span id="10"></span>
### How to upload certificates?
You can upload certificates by calling an API or through the CLB console.

[[Back to Top]](#1)

<span id="11"></span>
### Are certificates region-specific?
Yes. If a user's certificate needs to be used in multiple regions, it is necessary to upload the certificate in multiple regions to ensure the security and performance.

[[Back to Top]](#1)

<span id="12"></span>
### Does a certificate need to be uploaded to a backend CVM instance?
No. CLB HTTPS provides a certificate management system to manage and store user certificates. Certificates do not need to be uploaded to backend CVM instances, and all the private keys uploaded to the certificate management system are stored in an encrypted manner.

[[Back to Top]](#1)

<span id="13"></span>
### What to do after a certificate expires?
If the current certificate expires, you need to update the certificate manually.

[[Back to Top]](#1)

<span id="14"></span>
### What can I do if an error occurs when adding a certificate?
This may be caused by the wrong content of the private key. In this case, you need to replace it with a new certificate that meets the requirements.

[[Back to Top]](#1)
