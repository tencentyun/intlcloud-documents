## TCP/UDP Protocol
You can access the acceleration connection by the following methods:
- The client directly accesses the "VIP + port" of the acceleration connection.
- The client accesses the "domain name + port" of the acceleration connection. 
- If the client originally accesses a domain name, configure CNAME to resolve this domain name to that of the acceleration connection, or modify the local host of the client to resolve the original domain name to the VIP of the acceleration connection.
If the origin server needs the real client IP (TCP protocol only), TOA module should be installed. For more information, see [Obtaining the Real IPs of Access Users (TCP protocol only)](/document/product/608/14427).

## HTTP/HTTPS Protocol
Configure CNAME to resolve the domain name accessed by the client to the domain name of the acceleration connection, or modify the local host of the client to resolve the domain name to be accessed by the client to the VIP of the acceleration connection, so that the client can access the connection with `protocol + URL` to achieve acceleration.
The origin server can get the real client IP directly from the x-forward-for field in HTTP request header.
