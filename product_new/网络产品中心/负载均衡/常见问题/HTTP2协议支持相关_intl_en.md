## Product Introduction
### What is HTTP/2?
- HTTP/2 (Hypertext Transfer Protocol Version 2) is a major revision of the HTTP network protocol used by the World Wide Web.
- HTTP/2 is designed to address the performance issues in HTTP1.X to make better use of network resources and reduce network application latency.
- HTTP/2 is backward compatible with HTTP1.X.

### Why should HTTP/2 be used?
Compared with HTTP1.X, HTTP/2 can make a response faster and more efficiently. It features the following advantages:
- Multiplex: concurrent processing brings a faster response.
- Server push: the server proactively pushes desired resources to the client, reducing the number of requests.
- More features include bandwidth limit, request priority, header compression, and binary framing.

## Product Purchase
### How is HTTP/2 billed?
CLB supports the HTTP/2 protocol with no extra fees charged.

## Product Implementation
### How do I enable HTTP/2 on CLB?
1. Enable HTTP/2 on HTTPS listeners
 + CLB instance: a CLB instance supports enabling or disabling the HTTP/2 protocol. For more information, see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
 + Classic CLB instance: HTTPS listeners created for Classic CLB before April 2018 do not support the HTTP/2 protocol. HTTPS listeners created after April 2018 support but cannot disable the HTTP/2 protocol.
2. Agree on the protocol at the client access
When the client accesses an HTTP/2-enabled listener, the protocol version will be negotiated during the handshake process of HTTPS. The client uses ALPN (Application-Layer Protocol Negotiation) to inform the server of a list of supported protocols. The server selects HTTP/2 or HTTP1.X according to the protocol list. If the client does not support HTTP/2, the server will be automatically backward compatible without additional configuration required.

>!
> 1. HTTP listener does not support HTTP/2. Mainstream browsers and web servers only support TLS-based HTTP/2 protocol.
> 2. The HTTP1.X protocol is still used between CLB and real server.

### Which regions support HTTP/2?
All regions.


