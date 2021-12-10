## TCP/UDP Protocol
You can access the accelerated connection by the following methods:
- The client directly accesses the "VIP + port" of the accelerated connection.
- The client accesses the "domain name + port" of the accelerated connection. 
- If the client originally accesses a domain name, configure CNAME to resolve this domain name to that of the accelerated connection, or modify the local host of the client to resolve the original domain name to the VIP of the accelerated connection.
If the origin server needs the real client IP (TCP protocol only), TOA module should be installed. For more information, please see [Basic Principle](https://intl.cloud.tencent.com/document/product/608/14429)

## HTTP/HTTPS Protocol
Configure CNAME to resolve the domain name accessed by the client to the domain name of the accelerated connection, or modify the local host of the client to resolve the domain name to be accessed by the client to the VIP of the accelerated connection, so that the client can access the connection with protocol + URL to achieve acceleration.
The origin server can get the real client IP directly from the x-forwarded-for field in HTTP request header.
