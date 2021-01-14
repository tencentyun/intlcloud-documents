<span id="1"></span>
**Product Introduction**
- [What is HTTP/2?](#2)
- [Why should I use HTTP/2?](#3)

**Product Purchase**
- [How does the billing work?](#4)

**Product Implementation**
- [How do I enable HTTP/2 on CLB?](#5)
- [Which regions support HTTP/2?](#6)

<span id="2"></span>
### What is HTTP/2?
- HTTP/2 (Hypertext Transfer Protocol Version 2) is a major revision of the HTTP network protocol used by the World Wide Web.
- HTTP/2 is designed to address the performance issues in HTTP1.X to better use network resources and reduce network application latency.
- HTTP/2 is backward compatible with HTTP1.X.

[[Back to Top]](#1)
<span id="3"></span>
### Why should I use HTTP/2?
Compared with HTTP1.X, HTTP/2 can make the response be more fast and efficient. HTTP/2 has the following advantages:
- Multiplex: concurrent processing brings a faster response.
- Server push: the server proactively pushes resources needed by the client, reducing the number of requests.
- More features include bandwidth limit, request priority, header compression, and binary framing.

[[Back to Top]](#1)
<span id="4"></span>
### How does the billing work?
CLB supports the HTTP/2 protocol without charging extra fees.

[[Back to Top]](#1)
<span id="5"></span>
### How do I enable HTTP/2 on CLB?
1. Enable HTTP/2 on HTTPS listeners
 + CLB instance: you can enable or disable the HTTP/2 protocol in a CLB instance. For more information, please see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
 + Classic CLB instance: HTTPS listeners created for a classic CLB instance before April 2018 do not support HTTP/2. HTTPS listeners created after April 2018 support but cannot disable HTTP/2.
2. Agree on the protocol at client access
When the client accesses an HTTP/2-enabled listener, the protocol version will be negotiated during the handshake process of HTTPS. The client uses ALPN (Application-Layer Protocol Negotiation) to inform the server of a list of supported protocols. The server selects HTTP/2 or HTTP1.X according to the protocol list. If the client does not support HTTP/2, the server will be automatically backward compatible without requiring additional configuration.

>!
> 1. The HTTP listener does not support HTTP/2. Mainstream browsers and web servers only support the TLS-based HTTP/2 protocol.
> 2. The HTTP1.X protocol is still used between the CLB instance and the real server.
> 
[[Back to Top]](#1)
<span id="6"></span>
### Which regions support HTTP/2?
Currently, all regions support HTTP/2.

[[Back to Top]](#1)

