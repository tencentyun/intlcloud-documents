### What cipher suites are supported by HTTPS?
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK

### Which versions of SSL/TLS security protocols are supported by HTTPS?
CLB HTTPS currently supports the following SSL protocols: TLS 1, TLS 1.1, and TLS 1.2.

### Which port does an HTTPS listener use?
There is no mandatory requirement for this. Port 443 is recommended.

### Why HTTPS mutual authentication is needed?
Some users such as financial service providers have higher requirements for data security. They require HTTPS authentication on both the server and client. To meet their needs, HTTPS two-way authentication is provided.

### Why does the HTTPS protocol actually generate more traffic than the billed traffic?
If the HTTPS protocol is used, it actually generates more traffic than the billed traffic as some of the traffic is used for protocol handshake.

### Will requests from CLB instances to real servers still be transferred over HTTP after an HTTPS listener is added?
Yes. After an HTTPS listener is added, requests from the client to the CLB instance will be encrypted over HTTPS, but requests from the CLB instance to the real server will still be transferred over HTTP. Therefore, there is no need to configure SSL on the real server.

### What types of certificates does CLB currently support?
CLB currently supports server certificates and CA certificates. For a server certificate, both certificate content and private key need to be uploaded. For a CA certificate, only certificate content needs to be uploaded. For both types of certificates, only certificates in PEM encoding format can be uploaded.

### How many HTTPS certificates can be bound to a listener?
If HTTPS one-way authentication is used, only one server certificate can be bound to a listener. If HTTPS mutual authentication is used, one server certificate and one CA certificate need to be bound to a listener.

### How many CLB instances or listeners can a certificate be applied to?
A certificate can be applied to one or multiple CLB instances or listeners.

### How do I upload a certificate?
You can upload it by calling an API or through the CLB console.

### Is a certificate region-specific?
Yes. If a certificate needs to be used in multiple regions, it is necessary to upload it in all those regions separately to ensure security and performance.

### Does a certificate need to be uploaded to a backend CVM instance?
No. CLB HTTPS provides a certificate management system to manage and store user certificates. Certificates do not need to be uploaded to backend CVM instances, and all the private keys uploaded to the certificate management system are stored in an encrypted manner.

### What can I do after a certificate expires?
After the current certificate expires, you need to update the certificate manually.

### What can I do when a certificate error occurs?
This may be caused by wrong content of the private key. In this case, you need to replace it with a new certificate that meets the requirement.
