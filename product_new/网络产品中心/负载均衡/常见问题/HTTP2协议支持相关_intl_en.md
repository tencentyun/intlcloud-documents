## Product Content
### What is HTTP/2?
- HTTP/2 (Hypertext Transfer Protocol Version 2) is a major revision of the HTTP network protocol used by the World Wide Web.
- HTTP/2 is designed to address the performance issues in HTTP1.X to make better use of network resources and reduce network application latency.
- HTTP/2 is backward compatible with HTTP1.X.

### Why should HTTP/2 be used?
Compared with HTTP1.X, HTTP/2 can make a response faster and more efficiently. It features the following advantages:
- Multiplex: Concurrent processing leads to a faster response.
- Server push: The server proactively pushes resources needed by the client, reducing the number of requests.
- More features include traffic control, request priority, header compression, and binary framing.

## Product Purchase
### How does the billing work?
CLB supports the HTTP/2 protocol by default with no extra fees charged.

## Product Implementation
### How to enable HTTP/2 on CLB?
**The listener supports HTTP/2 on HTTPS by default with no additional configuration required**.
During the handshake process of HTTPS, the protocol version will be negotiated. The client uses ALPN (Application-Layer Protocol Negotiation) to inform the server of a list of supported protocols. The server selects HTTP/2 or HTTP1.X according to the protocol list. It is automatically backward compatible with no additional configuration required.
>
> 1. Plaintext HTTP/2 is not supported. Mainstream browsers and web servers only support TLS-based HTTP/2 protocol.
> 2. The HTTP1.X protocol is still used between CLB and real server.

### Which regions support HTTP/2?
HTTP/2 is supported in regions such as Beijing, Shanghai, Guangzhou, Hong Kong (China), Silicon Valley, and Frankfurt.
